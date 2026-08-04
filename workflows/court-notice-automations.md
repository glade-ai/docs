# Court Notice Automations

## Overview

Court notice automations act automatically when classified PACER court notices arrive on a case — sending emails and creating tasks. Your firm sets up rules that match incoming notice types, and Glade fires the configured actions to the right recipients with the right context — without anyone on your team having to watch the inbox. Automations are managed under **Workflow Reports → Court Notices → Automations**.

## Key Behaviors

- Each automation is owned by a creator (your firm) and listens for PACER notices that match its rules.
- An automation has a **name**, an **enabled/disabled** toggle, a **match type** (the notice type to match — for example "Notice of Hearing"), optional **chapter** and **judge** filters, and a list of **recipients**.
- When a matching notice is processed, the system loads case context, resolves recipients, fills in the email tokens, and sends the email.
- **Sender identity**: automation emails are sent from your firm owner's email address, and the sender name shown to recipients is your firm's name. Replies go to the firm owner.
- Each fire is recorded as a run on the automation, so you can see when each automation last ran and whether it succeeded. The automation's **last run** time and **last run status** appear on the list view.
- **Idempotency**: the same incoming court notice never triggers the same automation twice. If the same upstream event is processed again (for example after a retry), the duplicate fire is ignored.
- **Failure isolation**: if one automation fails — for example because a recipient email is invalid — other automations matching the same notice still run.

### Triggers and filters

A trigger has three parts. All must match for the automation to fire:

- **Notice type** (required) — exact match against the classified PACER notice type. For example, an automation with match type "Notice of Hearing" fires only on notices classified as "Notice of Hearing".
- **Chapter** (optional) — restricts the automation to a specific chapter (Chapter 7 or Chapter 13). When left blank, the automation matches any chapter.
- **Judge** (optional) — restricts the automation to a specific judge (matched by judge initials, case-insensitive). When left blank, the automation matches any judge.

The judge picker is populated from the judges who have actually appeared on PACER notices for your firm in the last 12 months, sorted by how often they appear so the most common judges are at the top.

### Creating a task from an automation

As well as sending an email, an automation can create a task on the case when it fires. Who that task is assigned to can depend on the notice, using **assignment rules**.

Each rule combines up to three conditions with a list of the people to assign:

| Condition | Matches on |
|-----------|-----------|
| **Chapter** | Chapter 7 or Chapter 13, compared the same way as the automation's own chapter filter |
| **Judge** | The judge on the notice, compared by initials and case-insensitive, the same way as the automation's judge filter |
| **Trustee** | The trustee named on the notice. Trustee names are free text, so they are compared ignoring capitalization and surrounding spaces |

This lets one automation route work the way your firm actually divides it — Chapter 13 notices to the Chapter 13 paralegal, notices in front of one judge to the person who covers that judge, anything from a particular trustee to both.

**How the conditions combine:**

- Each condition is joined to the next by **and** or **or**, and the rule is read strictly left to right: chapter, then judge, then trustee. There is no precedence between **and** and **or** — "chapter **and** judge **or** trustee" means "(chapter and judge) or trustee", never "chapter and (judge or trustee)". Order your conditions with that in mind.
- A condition you leave blank drops out of the rule entirely, along with the operator that joined it. It is not treated as a match. A rule with a chapter and a trustee joined by **or**, and no judge, matches a notice that is either in that chapter or from that trustee.
- A rule with all three conditions blank always matches. Use one as a catch-all so notices that fit none of your specific rules still land with someone.

**How assignees are worked out when the automation fires:**

- Every rule is evaluated against the notice, and **one task** is created — not one per rule and not one per person.
- The assignees from every rule that matched are combined. Someone named by two matching rules is assigned to the task once.
- If no rule matches the notice, no task is created and the run is recorded as skipped.
- If rules matched but none of their assignees can be resolved — for example every one of them was a team member who has since been removed — no task is created and the run is recorded as skipped.
- An automation with two separate task actions still creates two tasks, as before.

The trustee picker is populated from the trustees who have actually appeared on PACER notices for your firm in the last 12 months, most frequent first — the same way the judge picker works.

Automations set up before assignment rules existed keep working unchanged. Their single list of assignees reads as one rule with no conditions, so the same people are assigned on every firing until you add conditions.

### Recipients

Recipients are the people who receive the email when the automation fires. Three recipient kinds are supported and can be combined on a single automation:

- **Case-party token** — automatically resolves to the email address of a person on the case. Supported tokens are `debtor1`, `debtor2`, and `attorney`.
- **Team member** — a specific Glade team member at your firm. The system verifies the team member still belongs to your firm at fire time; soft-deleted team members are skipped.
- **Literal email** — a fixed email address you type in.

If an automation has no resolvable recipients at fire time (for example because every recipient was a team member who was removed), the run is logged as skipped and no email is sent.

### Tokens in the email

The email subject and body support a set of tokens that are filled in at fire time:

- `{{caseNumber}}` — the PACER case number on the matched notice.
- `{{noticeType}}` — the classified notice type that matched the automation.
- `{{clientName}}` — the primary debtor's name on the case.
- `{{judgeInitials}}` — the judge initials on the matched notice.
- `{{firmName}}` — your firm's display name.

In addition, automations can pull case-party and hearing details so the email reads like a personalized notice:

- The **first debtor's name** and, for joint cases, the **second debtor's name**, taken from the people on the case.
- The **341 meeting of creditors date and time**, taken from the linked court calendar entry for the case.
- The **video hearing join details** (for example, the meeting link and dial-in information) when the notice is for a remote 341 meeting.

> TODO: Confirm the exact token spellings for the debtor names, 341 meeting date/time, and video hearing join details once they are finalized in the email editor.

Tokens are case-insensitive and tolerant of extra whitespace inside the braces. Unknown tokens render as empty strings — the email still sends, with the unknown token replaced by nothing.

## Configuration

| Setting | Description |
|---------|-------------|
| Name | Display name shown on the automations list. |
| Enabled | Whether the automation runs. Disabled automations are ignored. |
| Match type | Notice type to match (exact). |
| Chapter | Chapter 7, Chapter 13, or any. |
| Judge | Specific judge or any. |
| Recipients | Combination of case-party tokens, team members, and literal email addresses. |
| Assignment rules | For an automation that creates a task: a list of rules, each with an optional chapter, judge, and trustee condition joined by **and**/**or**, plus the people to assign. At least one assignee per rule. |
| Subject and body | Email content with optional tokens for case number, notice type, client name, judge initials, firm name, debtor names, the 341 meeting date and time, and video hearing join details. |

Edits are tracked: each save records who made the change and when, alongside who originally created the automation.

## Edge Cases & Limitations

- The match type is exact. Notices with a slightly different classification do not match — set up additional automations for related notice types if needed.
- Only the supported tokens listed above are recognized. Unknown tokens render as empty strings.
- Hearing tokens depend on the linked court calendar entry. If a case has no 341 meeting scheduled or no video hearing details on file, those tokens render as empty strings.
- If a recipient is a soft-deleted team member, that recipient is skipped at fire time. The automation still fires for any remaining recipients.
- Run history (every individual fire of an automation) is not yet surfaced in the UI. The automation list shows the most recent run time and status only.
- Failed runs are not retried automatically. The failure shows as the automation's last run status.
- Conditional logic inside a single automation is limited to assignment rules on a task action — they decide *who* a task goes to, not whether the automation fires or what the email says. The automation's own trigger has no branching; use separate automations for separate scenarios.
- Assignment-rule conditions cover chapter, judge, and trustee only. There is no condition on other notice details.
- Assignment-rule conditions are evaluated strictly left to right with no operator precedence. A rule that mixes **and** and **or** may not mean what it reads like at a glance — check the grouping described above.
- A rule whose conditions are all blank matches every notice. Leaving a rule empty by accident assigns its people to every firing.

## Related Features

- [Automation Rules](./automation-rules.md) — general workflow automations driven by client actions.
- [PACER Integration](../integrations/pacer.md) — the source of court notices that drive these automations.
