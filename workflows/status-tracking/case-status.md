# Case Status

## Overview

Each case (an active workflow for a specific client) has a status, a progress percentage, and counters for steps and tasks. This page covers what a case tracks, the built-in statuses, manual status changes, and what happens to a case when its status changes — including archiving, unarchiving, filing, and pausing — and how those changes are recorded in the case's activity history.

## Key Behaviors

- Each case tracks:
  - **Status** — the current lifecycle phase (e.g., "Data Collection", "Processing", "Completed")
  - **Progress** — a percentage representing overall completion
  - **Steps completed** — how many workflow steps are done out of the total
  - **Tasks completed** — how many client/team tasks are done out of the total
  - **Last activity** — when the most recent action occurred on the case
  - **Last status change** — when the case's status was most recently updated
  - **Last assignment change** — when the case's assigned team member(s) were most recently changed
- **Manual status changes**: Your team can manually change a case's status at any time.
- **Built-in default statuses** (available to every firm):
  - Data Collection — initial phase where client information is gathered
  - Processing — case is being prepared
  - Filed and Pending — case has been filed, awaiting resolution
  - Completed — case is done
  - Archived — case is inactive
  - Additional built-in statuses include: Initiated, Retained, Triage, Document Collection, Credit Report Pulled, Questionnaire Collection, Petition Prep, Final Review, Ready to File, Signed & Paid, Post-Filing, Retaining, Bankruptcy Forms
- Your firm can also define its own statuses — see [Custom Statuses](./custom-statuses.md).
- **What happens when status changes**:
  - Moving to Completed, Filed and Pending, or any status with archive behavior completes all pending tasks for the case.
  - Archiving a case preserves the previous status so it can be restored later. Archiving also promotes any associated workflows to primary.
  - Unarchiving a case restores the previous status. If there was no previous status, it defaults to Data Collection.
  - Moving to Filed and Pending records the filing date. Moving back to Data Collection or Processing clears the filing date.
  - Moving to Completed records the completion date.
- **Court case number visible to clients**: After a case is filed with the court, its court-assigned case number is recorded on the case and shown to the client in their own portal view of the workflow, so clients can find their case number without contacting the firm. No case number appears before the case is filed.
- **Pause and resume**: Cases can be paused until a specific date. Pausing and resuming are tracked as separate events.

### Activity history

- **Activity log**: All status changes are recorded in the case's activity history alongside other events like document uploads, questionnaire completions, payments, and comments.
- **Case-filed activity**: When a case is filed electronically through the court's PACER system, a **Case Filed** entry is added to the case's activity history and appears in the Recent Activity view, reading "*name* filed the case via PACER." When a filed case is instead recorded manually — for example, a staff member registering a filing or resolving a filing deficiency — the entry reads "*name* registered the filed case," since it was not submitted through PACER. Cases whose status is changed to a filed status still show that as a status-change entry, so a single filing is never recorded twice.

## Configuration

- **Workflow type**: The workflow type ("basic" or "attorney case") affects how automatic status progression and completion logic behave. See [Automatic Status Updates](./automatic-status-updates.md).

## Edge Cases & Limitations

- Any string can technically be set as a status, though the system expects it to match either a built-in or custom status.
- When a case is archived and later unarchived, it restores to the previous status. If there is no previous status, it defaults to Data Collection.
- The completion date is preserved when archiving a case, so it remains accurate if the case is later unarchived.

## Related Features

- [Status Tracking](./README.md)
- [Automatic Status Updates](./automatic-status-updates.md)
- [Custom Statuses](./custom-statuses.md)
- [Tasks](./tasks.md)
- [PACER Integration](../../integrations/pacer/README.md)
