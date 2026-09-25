# Automations and Actions

## Overview

A court notice automation is a rule your firm owns that listens for matching PACER notices and runs a list of actions when one arrives. This doc covers how an automation is structured, how it runs, how each run and action is recorded, and how to name actions and find automations on the list.

## Key Behaviors

- Each automation is owned by a creator (your firm) and listens for PACER notices that match its rules.
- An automation has a **name**, an **enabled/disabled** toggle, a **match type** (the notice type to match — for example "Notice of Hearing"), optional **chapter** and **judge** filters, and a list of **actions**.
- When a matching notice is processed, the system loads case context, resolves who each action applies to, fills in the tokens, and runs the actions in order.
- Each fire is recorded as a run on the automation, so you can see when each automation last ran and whether it succeeded. The automation's **last run** time and **last run status** appear on the list view. A run also records an outcome for each individual action it ran.
- **Idempotency**: the same incoming court notice never triggers the same automation twice. If the same upstream event is processed again (for example after a retry), the duplicate fire is ignored. This applies per action, so a reprocessed notice does not send a second email or create a second copy of a task.
- **Failure isolation**: if one automation fails — for example because a recipient email is invalid — other automations matching the same notice still run. The same holds between actions on a single automation: if one action fails, the remaining actions still run, and the run is recorded as **partial** rather than failed.

### Actions

An automation runs a list of actions rather than a single email. Each action has its own type, its own settings, and its own enabled/disabled state, and actions run in the order they are listed. Two action types are available:

- **Send email** — sends the configured email to the resolved recipients. See [Email Actions](./email-actions.md).
- **Create task** — creates a task on the case so the work lands in someone's queue instead of only in an inbox. See [Create Task Actions](./create-task-actions.md).

Automations that existed before actions were introduced continue to work unchanged: each one now shows a single **Send email** action carrying the subject, body, and recipients it already had. There is nothing to re-create.

### Per-action run results

Every run records a result for each action it ran, so you can tell which part of an automation worked and which did not — for example, that the email went out but the task was not created. Run status rolls up across the actions:

| Run status | Meaning |
|------------|---------|
| Ran | Every action that was supposed to run succeeded. |
| Partial | At least one action succeeded and at least one failed. |
| Failed | Every action failed. |
| Skipped | Nothing ran — for example, no recipients or assignees resolved. |

The recipients an email was actually sent to are recorded on the run, so the history shows who was contacted at the time rather than who would be contacted today.

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

## Configuration

| Setting | Description |
|---------|-------------|
| Name | Display name shown on the automations list. |
| Action title | Optional label for an individual action within the automation, up to 200 characters. Internal only — not shown to recipients. |
| Enabled | Whether the automation runs. Disabled automations are ignored. |
| Actions | One or more actions to run when the automation fires — **Send email**, **Create task**, or several of each. Each action can be enabled or disabled on its own and the actions run in listed order. |

Edits are tracked: each save records who made the change and when, alongside who originally created the automation.

## Edge Cases & Limitations

- The automation list itself shows the most recent run time and status only. Individual fires are read from the automation's run history.
- Failed runs are not retried automatically. The failure shows as the automation's last run status, and the run's per-action results show which action failed. Re-sending the email from the run history is the manual equivalent for a send that did not land.
- Action titles are not recorded on a run's history. A run identifies which action fired, but if you rename an action later, past runs reflect the current title rather than the one in place when they ran.
- The find bar searches automation names, match types, and action titles. It does not search email subject or body text, recipients, or judge filters.

## Related Features

- [Court Notice Automations](./README.md)
- [Triggers and Filters](./triggers-and-filters.md)
- [Email Actions](./email-actions.md)
- [Create Task Actions](./create-task-actions.md)
