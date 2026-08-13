# Court Notice Automations

## Overview

Court notice automations send emails automatically when classified PACER court notices arrive on a case. Your firm sets up rules that match incoming notice types, and Glade fires the configured emails to the right recipients with the right context — without anyone on your team having to watch the inbox. Automations are managed under **Workflow Reports → Court Notices → Automations**.

## Key Behaviors

- Each automation is owned by a creator (your firm) and listens for PACER notices that match its rules.
- An automation has a **name**, an **enabled/disabled** toggle, a **match type** (the notice type to match — for example "Notice of Hearing"), optional **chapter** and **judge** filters, and a list of **recipients**.
- When a matching notice is processed, the system loads case context, resolves recipients, fills in the email tokens, and sends the email.
- **Sender identity**: automation emails are sent from your firm owner's email address, and the sender name shown to recipients is your firm's name. Replies go to the firm owner.
- Each fire is recorded as a run on the automation, so you can see when each automation last ran and whether it succeeded. The automation's **last run** time and **last run status** appear on the list view.
- **Idempotency**: the same incoming court notice never triggers the same automation twice. If the same upstream event is processed again (for example after a retry), the duplicate fire is ignored.
- **Failure isolation**: if one automation fails — for example because a recipient email is invalid — other automations matching the same notice still run.

### Naming an individual action

An automation can carry more than one action — several emails, or an email alongside a task. Each action can be given its own **action title**, so a list of three emails reads as "Chase trustee", "Notify debtor", and "Flag for review" instead of three identical "Send email" cards you have to open one at a time to tell apart.

- The title is a label for your team only. It is not shown to recipients and does not appear in the email.
- Titles are optional. An action left untitled continues to show its action type.
- A title can be up to 200 characters. Leaving it blank, or entering only spaces, clears it.
- An action's title is separate from the title of any task the action creates — naming an action does not change the task your clients or team see.

> TODO: Confirm the label and location of the action title field in the automation editor.

### Finding an automation

The find bar on the automations list matches on whole words in any order, across the automation's name, its match type, and its actions' titles.

- Searching `trustee email` finds an automation named "Email trustee" — word order does not matter, and the words do not have to be next to each other.
- All the words you type must appear in the same place: `chase trustee` matches an action titled "Chase trustee", but not an automation named "Chase" with an unrelated action titled "Trustee".
- Titles on disabled or deleted actions are not matched.
- The result count reflects the filtered list.

Previously the find bar matched only against the whole automation name and match type, start to finish, so searching `trustee email` returned nothing for an automation named "Email trustee".

### Triggers and filters

A trigger has three parts. All must match for the automation to fire:

- **Notice type** (required) — exact match against the classified PACER notice type. For example, an automation with match type "Notice of Hearing" fires only on notices classified as "Notice of Hearing".
- **Chapter** (optional) — restricts the automation to a specific chapter (Chapter 7 or Chapter 13). When left blank, the automation matches any chapter.
- **Judge** (optional) — restricts the automation to a specific judge (matched by judge initials, case-insensitive). When left blank, the automation matches any judge.

The judge picker is populated from the judges who have actually appeared on PACER notices for your firm in the last 12 months, sorted by how often they appear so the most common judges are at the top.

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

#### Debtor names on notices that are not linked to a case

Not every incoming court notice is matched to a case in Glade. When a notice is unlinked, the debtor and client name tokens have no client record to read from, and the email previously went out addressed to nobody — a discharge congratulations message opening "Dear ," is the case firms reported.

- When the notice is linked to a case, the client's name on that case is used, exactly as before. A linked name always wins.
- When the notice is not linked, or the linked client has no name on file, Glade falls back to the debtor name in the case caption carried on the court notice itself, and strips the trailing case-number text so only the name is inserted.
- If neither source has a name, the token still renders as empty and the email still sends.

#### Hearing tokens when a notice carries more than one hearing

A single court notice can schedule more than one hearing — a confirmation hearing and a 341 meeting in the same docket entry, for example. When that happens, the hearing tokens use the **341 meeting**, so an email written for the meeting of creditors quotes the meeting date rather than whichever hearing happened to be listed first.

> TODO: Confirm the exact token spellings for the debtor names, 341 meeting date/time, and video hearing join details once they are finalized in the email editor.

Tokens are case-insensitive and tolerant of extra whitespace inside the braces. Unknown tokens render as empty strings — the email still sends, with the unknown token replaced by nothing.

## Configuration

| Setting | Description |
|---------|-------------|
| Name | Display name shown on the automations list. |
| Action title | Optional label for an individual action within the automation, up to 200 characters. Internal only — not shown to recipients. |
| Enabled | Whether the automation runs. Disabled automations are ignored. |
| Match type | Notice type to match (exact). |
| Chapter | Chapter 7, Chapter 13, or any. |
| Judge | Specific judge or any. |
| Recipients | Combination of case-party tokens, team members, and literal email addresses. |
| Subject and body | Email content with optional tokens for case number, notice type, client name, judge initials, firm name, debtor names, the 341 meeting date and time, and video hearing join details. |

Edits are tracked: each save records who made the change and when, alongside who originally created the automation.

## Edge Cases & Limitations

- The match type is exact. Notices with a slightly different classification do not match — set up additional automations for related notice types if needed.
- Only the supported tokens listed above are recognized. Unknown tokens render as empty strings.
- Hearing tokens depend on the linked court calendar entry. If a case has no 341 meeting scheduled or no video hearing details on file, those tokens render as empty strings.
- The case-caption fallback for debtor names only supplies a name. It does not link the notice to a case, so the other case-context tokens on an unlinked notice stay empty.
- If a recipient is a soft-deleted team member, that recipient is skipped at fire time. The automation still fires for any remaining recipients.
- Run history (every individual fire of an automation) is not yet surfaced in the UI. The automation list shows the most recent run time and status only.
- Failed runs are not retried automatically. The failure shows as the automation's last run status.
- Branching or conditional logic inside a single automation is not supported. Use separate automations for separate scenarios.
- Action titles are not recorded on a run's history. A run identifies which action fired, but if you rename an action later, past runs reflect the current title rather than the one in place when they ran.
- The find bar searches automation names, match types, and action titles. It does not search email subject or body text, recipients, or judge filters.

## Related Features

- [Automation Rules](./automation-rules.md) — general workflow automations driven by client actions.
- [PACER Integration](../integrations/pacer.md) — the source of court notices that drive these automations.
