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
  - **Last assignment change** — when the case's assigned team member(s) were most recently changed
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
- **Archiving statuses**: Any status — including built-in default statuses — can be archived. Archiving a status removes it from the status picker so it cannot be assigned to new cases. When you archive a status that is currently in use, a confirmation prompt shows how many active workflows are using it, so you can make an informed decision before proceeding. See [Settings](../back-office/settings.md) for the archive/unarchive UI.
- **Archived status visibility**: Cases that are currently assigned an archived status continue to display that status correctly — the label, icon, and color remain visible in workflow lists and on the case. Archived statuses are only hidden from pickers where you select a status; existing cases are not affected.
- **Viewing archived statuses**: Archived statuses are hidden by default on the Custom Statuses settings page. Toggle **Show archived** to reveal them.
- **What happens when status changes**:
  - Moving to Completed, Filed and Pending, or any status with archive behavior completes all pending tasks for the case.
  - Archiving a case preserves the previous status so it can be restored later. Archiving also promotes any associated workflows to primary.
  - Unarchiving a case restores the previous status. If there was no previous status, it defaults to Data Collection.
  - Moving to Filed and Pending records the filing date. Moving back to Data Collection or Processing clears the filing date.
  - Moving to Completed records the completion date.
- **Court case number visible to clients**: After a case is filed with the court, its court-assigned case number is recorded on the case and shown to the client in their own portal view of the workflow, so clients can find their case number without contacting the firm. No case number appears before the case is filed.
- **Sortable workflow list**: In the workflow list view, cases can be sorted by status change date, last assignment date, or by the **Assignees** column (alphabetically by the primary owner's name). Sorting by Assignees lets you group cases by responsible team member for review or handoff.
- **Export unassigned workflows to CSV**: From the workflow list, you can export the current set of unassigned workflows to a CSV file. The export reflects the filters currently applied to the list, so narrowing by status or attorney before exporting limits the output to the matching cases. This is useful for triaging assignment backlogs offline or sharing the list with team leads outside Glade.
- **Last Payment Made column**: The workflow list table includes a **Last Payment Made** column showing the timestamp of the most recent payment received on the case. The column is blank for cases that have not received a payment yet.
- **Workflow tags**: Workflows can be labeled with tags to group related cases. Each tag is a short label with an optional emoji icon. The workflow list shows a **Tags** column, and the list filters include a tag filter — pick one or more tags to narrow the list to workflows carrying any of the selected tags (selecting several tags shows cases that match any one of them). When tagging workflows, you can choose from the tags your firm already uses, so the same label and icon stay consistent across cases.
- **Filter and pagination persistence**: Filter selections (status, assignees, attorney, settlement status), search term, sort order, and page number persist while you navigate within the dashboard. Returning to the workflow list keeps your previous view in place instead of resetting to defaults. Use the **Reset** link in the filters bar to clear all selections and return to page 1; the link appears whenever any filter is applied or you are past page 1.
- **Unassigned filter**: The assignment filter includes an **Unassigned** option (under an *Assignment Status* group) so you can isolate workflows with no current owner. The workflow list also accepts deep links that pre-apply filters — for example, opening the list from the dashboard's unassigned-workflows widget or from the paralegal report seeds the assignee, status, attorney, or settlement-status filters automatically.
- **Activity log**: All status changes are recorded in the case's activity history alongside other events like document uploads, questionnaire completions, payments, and comments.
- **Case-filed activity**: When a case is filed electronically through the court's PACER system, a **Case Filed** entry is added to the case's activity history and appears in the Recent Activity view, reading "*name* filed the case via PACER." When a filed case is instead recorded manually — for example, a staff member registering a filing or resolving a filing deficiency — the entry reads "*name* registered the filed case," since it was not submitted through PACER. Cases whose status is changed to a filed status still show that as a status-change entry, so a single filing is never recorded twice.
- **Pause and resume**: Cases can be paused until a specific date. Pausing and resuming are tracked as separate events.
- **Time-sensitive filing deadline**: A case can be marked as having to reach the court by a specific calendar date — an emergency Chapter 13 ahead of a foreclosure sale or a wage garnishment, for example. This is separate from the filed date, which records when a case was actually filed. See [Time-sensitive filing deadlines](#time-sensitive-filing-deadlines) below.
- **Tasks**: Tasks are actionable items created during a case — things like "complete questionnaire", "pay invoice", or "upload document". Each task is assigned to a person (client or team member) and tracks whether it has been completed.
- **Filing deficiency tasks**: When a case is filed manually (rather than through Glade's automated filing) and the court submission goes out missing required documents, Glade automatically creates an urgent task for **each** missing document, titled after that document. Previously a single task covered all of them at once. Every task references the affected filing and is assigned to both the team member who initiated the filing and the firm owner, so the missing documents can be addressed before the court's cure deadline. Splitting them per document lets your team divide the work and track what is still outstanding. Completing a task also clears that document from the case's filing deficiency, so the case's action-required banner narrows to the documents that remain — see [PACER Integration](../integrations/pacer.md) for the banner itself. Manual filings with no missing documents do not generate these tasks.
- **Automated reminders**: Tasks can have automated reminder emails and text messages attached to them. These reminders are scheduled, sent, and tracked automatically.
- **Task performance tracking**: The system tracks how long tasks take from creation to completion, how many times they are reopened, and the last completion time. This data is used for performance reporting.

### Time-sensitive filing deadlines

Some cases have to be filed with the court by a particular date — an emergency Chapter 13 filed ahead of a foreclosure sale, or a case racing a wage garnishment. Glade tracks that date on the case so your team can find these cases and work them in order rather than remembering them by hand.

- **Setting a deadline** — a case's settings let you record a **filing deadline** as a calendar date, plus an optional **reason** explaining why the case is time sensitive. Recording a deadline is what marks a case as time sensitive; a case with no deadline is not time sensitive.
- **Setting one at case creation** — the deadline and reason can also be entered when a staff member initiates a case, so an emergency filing carries its deadline from the moment it exists. A reason on its own is not accepted — the reason has to attach to a deadline.
- **Who set it** — Glade records which team member recorded the deadline and when. On a case created with a deadline, the person who created the case is recorded.
- **Clearing a deadline** — clearing the deadline also clears the reason and the record of who set it. The case is no longer time sensitive.
- **The date does not shift** — the deadline is a calendar day the court cares about, so it reads the same regardless of anyone's timezone.
- **Filtering, sorting, and reporting** — the workflow list can be filtered to time-sensitive cases only (or to cases that are not time sensitive), narrowed to deadlines falling inside a date range, and sorted by deadline. Cases with no deadline sort to the end in both directions. The cases CSV export includes a filing-deadline column and honors the same filters, so "which cases are due this week" can be answered as a list or as a spreadsheet.

#### Deadlines across related cases

A matter can carry several cases at once — an associated filing alongside the main one, or a new case created when a chapter converts. Each case carries its own deadline, because associated filings can genuinely be due on different dates.

- A case joining a matter that is already marked time sensitive **inherits the most recent deadline** on that matter, along with its reason and the record of who set it, provided the joining case has no deadline of its own.
- A case created with its own deadline keeps that deadline instead of inheriting.
- Answering explicitly that a new case is **not** time sensitive suppresses inheritance — it stays unmarked.
- When you create an associated case, the wizard shows the matter's most recent deadline so you can carry it over or override it deliberately.

## Configuration

- **Custom statuses**: Created and managed per firm. Each status has a unique identifier, display title, icon, color, and optional behavioral flags (archive behavior, disable followups). Any status — custom or built-in default — can be archived from the Custom Statuses settings page.
- **Status per workflow step**: Individual workflow steps can specify a status that the case automatically transitions to when that step's trigger completes.
- **Workflow type**: The workflow type ("basic" or "attorney case") affects how automatic status progression and completion logic behave.

## Edge Cases & Limitations

- Any string can technically be set as a status, though the system expects it to match either a built-in or custom status.
- When a case is archived and later unarchived, it restores to the previous status. If there is no previous status, it defaults to Data Collection.
- Custom statuses with archive behavior trigger the same task completion logic as the built-in Archived status, but the case retains the custom status rather than switching to Archived.
- Archiving a default status (one that shipped with your firm setup) does not delete it — it is preserved for historical reference but removed from the picker. Default statuses cannot be deleted, only archived.
- The number of active workflows shown in the archive confirmation reflects workflows at that moment; cases may have moved to other statuses by the time you confirm.
- The completion date is preserved when archiving a case, so it remains accurate if the case is later unarchived.
- The workflow list filters, the deadline sort, and the CSV export read the filing deadline from the matter's main case. A deadline set directly on a non-main case in the same matter is saved and shown on that case, but does not surface in those list views.
- The filing deadline is not a status. Setting one does not change the case's status, and passing the deadline does not move the case or raise an alert on its own.

## Related Features

- [Automation Rules](./automation-rules.md) — the workflows whose execution drives status changes
- [Triggers](./triggers.md) — trigger completion drives automatic status updates
- [Task Templates](./task-templates.md) — templates that define the initial workflow structure and steps
