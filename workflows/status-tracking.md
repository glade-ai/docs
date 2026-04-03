# Status Tracking

## Overview

Status tracking governs how a case's status and progress change over its lifecycle. Each case (an active workflow for a specific client) has a status, a progress percentage, and counters for steps and tasks. Status transitions happen automatically as workflow steps complete, and your team can also change status manually at any time. The system supports both built-in statuses and custom statuses that your firm defines.

## Key Behaviors

- Each case tracks:
  - **Status** — the current lifecycle phase (e.g., "Data Collection", "Processing", "Completed")
  - **Progress** — a percentage representing overall completion
  - **Steps completed** — how many workflow steps are done out of the total
  - **Tasks completed** — how many client/team tasks are done out of the total
  - **Last activity** — when the most recent action occurred on the case
  - **Last status change** — when the case's status was most recently updated
- **Automatic status updates**: When a workflow trigger completes, the case status can automatically update to a specific value. This is configured per workflow step, so workflow designers control exactly when status transitions happen.
- **Automatic progress calculation**: After each trigger completes, the system recalculates the case's progress, step counts, and task counts based on what has been completed so far.
- **Automatic completion**: When all workflow steps are done, the system automatically transitions the case to "Completed" status. Attorney-case type workflows may have specialized completion logic for certain case types.
- **Manual status changes**: Your team can manually change a case's status at any time.
- **Built-in default statuses** (available to every firm):
  - Data Collection — initial phase where client information is gathered
  - Processing — case is being prepared
  - Filed and Pending — case has been filed, awaiting resolution
  - Completed — case is done
  - Archived — case is inactive
  - Additional built-in statuses include: Initiated, Retained, Triage, Document Collection, Credit Report Pulled, Questionnaire Collection, Petition Prep, Final Review, Ready to File, Signed & Paid, Post-Filing, Retaining, Bankruptcy Forms
- **Custom statuses**: Your firm can create custom statuses with a title, icon, and color. Custom statuses also support two optional behaviors:
  - **Archive behavior** — moving a case to this status completes all pending tasks and promotes any related workflows, just like archiving
  - **Disable followups** — suppresses automated reminder emails and messages for cases in this status
- **What happens when status changes**:
  - Moving to Completed, Filed and Pending, or any status with archive behavior completes all pending tasks for the case.
  - Archiving a case preserves the previous status so it can be restored later. Archiving also promotes any associated workflows to primary.
  - Unarchiving a case restores the previous status. If there was no previous status, it defaults to Data Collection.
  - Moving to Filed and Pending records the filing date. Moving back to Data Collection or Processing clears the filing date.
  - Moving to Completed records the completion date.
- **Sortable workflow list**: In the workflow list view, cases can be sorted by when their status last changed. This lets you surface cases that have been stuck in a status for a long time or prioritize recently updated ones.
- **Activity log**: All status changes are recorded in the case's activity history alongside other events like document uploads, questionnaire completions, payments, and comments.
- **Pause and resume**: Cases can be paused until a specific date. Pausing and resuming are tracked as separate events.
- **Tasks**: Tasks are actionable items created during a case — things like "complete questionnaire", "pay invoice", or "upload document". Each task is assigned to a person (client or team member) and tracks whether it has been completed.
- **Automated reminders**: Tasks can have automated reminder emails and text messages attached to them. These reminders are scheduled, sent, and tracked automatically.
- **Task performance tracking**: The system tracks how long tasks take from creation to completion, how many times they are reopened, and the last completion time. This data is used for performance reporting.

## Configuration

- **Custom statuses**: Created and managed per firm. Each status has a unique identifier, display title, icon, color, and optional behavioral flags (archive behavior, disable followups).
- **Status per workflow step**: Individual workflow steps can specify a status that the case automatically transitions to when that step's trigger completes.
- **Workflow type**: The workflow type ("basic" or "attorney case") affects how automatic status progression and completion logic behave.

## Edge Cases & Limitations

- Any string can technically be set as a status, though the system expects it to match either a built-in or custom status.
- When a case is archived and later unarchived, it restores to the previous status. If there is no previous status, it defaults to Data Collection.
- Custom statuses with archive behavior trigger the same task completion logic as the built-in Archived status, but the case retains the custom status rather than switching to Archived.
- The completion date is preserved when archiving a case, so it remains accurate if the case is later unarchived.

## Related Features

- [Automation Rules](./automation-rules.md) — the workflows whose execution drives status changes
- [Triggers](./triggers.md) — trigger completion drives automatic status updates
- [Task Templates](./task-templates.md) — templates that define the initial workflow structure and steps
