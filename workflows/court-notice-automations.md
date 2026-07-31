# Court Notice Automations

## Overview

Court notice automations act automatically when classified PACER court notices arrive on a case. Your firm sets up rules that match incoming notice types, and Glade runs the configured actions — sending emails and creating tasks — with the right recipients and the right context, without anyone on your team having to watch the inbox. Automations are managed under **Workflow Reports → Court Notices → Automations**.

## Key Behaviors

- Each automation is owned by a creator (your firm) and listens for PACER notices that match its rules.
- An automation has a **name**, an **enabled/disabled** toggle, a **match type** (the notice type to match — for example "Notice of Hearing"), optional **chapter** and **judge** filters, and a list of **actions**.
- When a matching notice is processed, the system loads case context, resolves who each action applies to, fills in the tokens, and runs the actions in order.
- **Sender identity**: automation emails are sent from your firm owner's email address, and the sender name shown to recipients is your firm's name. Replies go to the firm owner.
- Each fire is recorded as a run on the automation, so you can see when each automation last ran and whether it succeeded. The automation's **last run** time and **last run status** appear on the list view. A run also records an outcome for each individual action it ran.
- **Idempotency**: the same incoming court notice never triggers the same automation twice. If the same upstream event is processed again (for example after a retry), the duplicate fire is ignored. This applies per action, so a reprocessed notice does not send a second email or create a second copy of a task.
- **Failure isolation**: if one automation fails — for example because a recipient email is invalid — other automations matching the same notice still run. The same holds between actions on a single automation: if one action fails, the remaining actions still run, and the run is recorded as **partial** rather than failed.

### Actions

An automation runs a list of actions rather than a single email. Each action has its own type, its own settings, and its own enabled/disabled state, and actions run in the order they are listed. Two action types are available:

- **Send email** — sends the configured email to the resolved recipients.
- **Create task** — creates a task on the case so the work lands in someone's queue instead of only in an inbox.

Automations that existed before actions were introduced continue to work unchanged: each one now shows a single **Send email** action carrying the subject, body, and recipients it already had. There is nothing to re-create.

#### Create task

- The task's **assignees** are chosen the same way as email recipients — case-party tokens (`debtor1`, `debtor2`, `attorney`) and team members at your firm. At least one assignee is required.
- **Due in** sets the task's due date as a number of days after the notice date, calculated in your firm's timezone. Leave it blank for no due date.
- The task carries a title and description, which support the same tokens as the email subject and body.
- Assignees are notified through the normal task notifications and the task appears in their inbox, exactly as a task created any other way.
- A create-task action is **skipped** when the notice is not linked to a workflow, or when none of its assignees resolve at fire time (for example because every assignee was a team member who has since been removed). Glade never creates a task with no assignee.
- Team member assignees are checked against your firm at fire time; anyone no longer at the firm is dropped.
- Two create-task actions on one automation produce two separate tasks.

### Per-action run results

Every run records a result for each action it ran, so you can tell which part of an automation worked and which did not — for example, that the email went out but the task was not created. Run status rolls up across the actions:

| Run status | Meaning |
|------------|---------|
| Ran | Every action that was supposed to run succeeded. |
| Partial | At least one action succeeded and at least one failed. |
| Failed | Every action failed. |
| Skipped | Nothing ran — for example, no recipients or assignees resolved. |

The recipients an email was actually sent to are recorded on the run, so the history shows who was contacted at the time rather than who would be contacted today.

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
- The **341 meeting of creditors date and time**, taken from the linked court calendar entry for the case, or read directly from the notice when the court calendar entry for the case has not been created yet. A 341 notice and the calendar entry it produces are handled at the same moment, so the automation often used to run a fraction of a second before the calendar entry existed — which left the meeting date and time blank on the email even though the notice itself stated them. Those details now fill in either way, and the case number is no longer the only token that reliably renders on a 341 notice.
- The **video hearing join details** (for example, the meeting link, meeting ID, and dial-in information) when the notice is for a remote 341 meeting. Glade reads the Zoom details out of the notice text, including formats that name the trustee's meeting room without a colon before the meeting ID — the style used in the Western District of Pennsylvania, for example. Notices written that way previously produced no video hearing details at all.

The same case-party and hearing details are available to **Create task** actions, so a task raised from a 341 notice can state the meeting date, time, and join details in its description.

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
| Actions | One or more actions to run when the automation fires — **Send email**, **Create task**, or several of each. Each action can be enabled or disabled on its own and the actions run in listed order. |
| Recipients | Combination of case-party tokens, team members, and literal email addresses. |
| Subject and body | Email content with optional tokens for case number, notice type, client name, judge initials, firm name, debtor names, the 341 meeting date and time, and video hearing join details. |
| Task assignees | For a **Create task** action: case-party tokens and team members. At least one is required; literal email addresses are not available here. |
| Task due in | For a **Create task** action: the number of days after the notice date that the task is due, in your firm's timezone. Optional. |

Edits are tracked: each save records who made the change and when, alongside who originally created the automation.

## Edge Cases & Limitations

- The match type is exact. Notices with a slightly different classification do not match — set up additional automations for related notice types if needed.
- Only the supported tokens listed above are recognized. Unknown tokens render as empty strings.
- Hearing tokens are filled from the linked court calendar entry or from the notice itself. If neither states a 341 meeting time, or the notice carries no video hearing details, those tokens render as empty strings.
- Emails sent before the 341 meeting details fix went out with the meeting date, time, and join details blank. Those emails are not resent — if clients were sent a 341 notice missing its meeting details, follow up manually.
- If a recipient is a soft-deleted team member, that recipient is skipped at fire time. The automation still fires for any remaining recipients.
- Tasks created by an automation appear in the inbox and in the newer task views. They may not yet appear in the older dashboard task lists, which show only a fixed set of task kinds.
- A **Create task** action needs the notice to be linked to a workflow. Court notices that never matched a workflow — the majority of notices for many firms — cannot raise a task, so an automation whose only action is Create task will show runs as skipped on those notices. Pair it with a **Send email** action if someone should still be told.
- Failed runs are not retried automatically. The failure shows as the automation's last run status, and the run's per-action results show which action failed.
- Branching or conditional logic inside a single automation is not supported. Use separate automations for separate scenarios.

## Related Features

- [Automation Rules](./automation-rules.md) — general workflow automations driven by client actions.
- [PACER Integration](../integrations/pacer.md) — the source of court notices that drive these automations.
