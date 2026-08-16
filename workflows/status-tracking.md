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
- **Tasks**: Tasks are actionable items created during a case — things like "complete questionnaire", "pay invoice", or "upload document". Each task is assigned to a person (client or team member) and tracks whether it has been completed.
- **Filing deficiency tasks**: When a case is filed manually (rather than through Glade's automated filing) and the court submission goes out missing required documents, Glade automatically creates an urgent task for **each** missing document, titled after that document. Previously a single task covered all of them at once. Every task references the affected filing and is assigned to both the team member who initiated the filing and the firm owner, so the missing documents can be addressed before the court's cure deadline. Splitting them per document lets your team divide the work and track what is still outstanding. Completing a task also clears that document from the case's filing deficiency, so the case's action-required banner narrows to the documents that remain — see [PACER Integration](../integrations/pacer.md) for the banner itself. Manual filings with no missing documents do not generate these tasks.
- **Automated reminders**: Tasks can have automated reminder emails and text messages attached to them. These reminders are scheduled, sent, and tracked automatically.
- **Task performance tracking**: The system tracks how long tasks take from creation to completion, how many times they are reopened, and the last completion time. This data is used for performance reporting.

### Dismissing and restoring tasks

The task list lets each team member clear items they no longer need to watch, without changing what anyone else sees or who the work belongs to.

- **Dismissing is per person.** Dismissing a task removes it from your own list only — everyone else, including whoever the task is assigned to, still sees it. Dismissals are remembered, so a task you cleared does not reappear the next time you open the list.
- **You can dismiss a task you are not assigned to.** Any team member who can see a task can dismiss it, including unassigned tasks and tasks that are already complete. Dismissing never reassigns the task or takes it away from another team member. Previously, dismissing a task that was assigned to someone else appeared to work but had no effect.
- **Restoring brings a task back.** A dismissed task can be restored to your list. If dismissing it also dropped your own assignment, restoring gives that assignment back; if you were not assigned at the time, restoring leaves assignment untouched.
- **Filtering by dismissal state.** The list shows **active** tasks by default — everything you have not dismissed. You can switch it to show **dismissed** tasks only, or **all** tasks regardless of dismissal.
- **Including completed tasks.** A separate setting adds completed tasks to the list alongside incomplete ones. It is off by default and is independent of the dismissal filter, so the two can be combined in any way — completed work you have not dismissed, dismissed work that is still open, and so on. The list previously showed incomplete tasks only, with no way to bring completed ones back into view.

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
- Dismissing a task does not complete it. The underlying work stays outstanding for whoever is assigned, and the task still counts toward the case's task totals — dismissal only controls whether it appears in your own list.

## Related Features

- [Automation Rules](./automation-rules.md) — the workflows whose execution drives status changes
- [Triggers](./triggers.md) — trigger completion drives automatic status updates
- [Task Templates](./task-templates.md) — templates that define the initial workflow structure and steps
