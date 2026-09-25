# Tasks

## Overview

Tasks are actionable items created during a case — things like "complete questionnaire", "pay invoice", or "upload document". Each task is assigned to a person (client or team member) and tracks whether it has been completed. This page covers how tasks are created and assigned, filing deficiency tasks, assignment emails, reminders, performance tracking, and dismissing tasks from your own list.

## Key Behaviors

- **Tasks**: Tasks are actionable items created during a case — things like "complete questionnaire", "pay invoice", or "upload document". Each task is assigned to a person (client or team member) and tracks whether it has been completed.
- **Filing deficiency tasks**: When a case is filed manually (rather than through Glade's automated filing) and the court submission goes out missing required documents, Glade automatically creates an urgent task for **each** missing document, titled after that document. Previously a single task covered all of them at once. Every task references the affected filing and is assigned to both the team member who initiated the filing and the firm owner, so the missing documents can be addressed before the court's cure deadline. Splitting them per document lets your team divide the work and track what is still outstanding. Completing a task also clears that document from the case's filing deficiency, so the case's action-required banner narrows to the documents that remain — see [PACER Integration](../../integrations/pacer/README.md) for the banner itself. Manual filings with no missing documents do not generate these tasks.
- **Assigning a colleague an internal task emails them.** When a team member creates a task on a case by hand — "case to be filed", "call the trustee", anything your team writes itself — everyone newly assigned to it is emailed, as well as being notified in the inbox. Previously only consultation tasks sent this email, so a task handed to a colleague could sit unnoticed unless they happened to check their inbox.
  - Reassigning the task later emails whoever it moves to.
  - The person doing the assigning is not emailed, and nobody is emailed for assigning a task to themselves.
  - **Document review tasks are deliberately left out.** A "Review Documents" task is created every time a client uploads a file, so emailing on those would bury the ones a colleague actually handed over. Case owners continue to receive the existing documents-in-review email for that work.
  - A task that is not attached to a case, and a task that is already complete, sends nothing.
- **Automated reminders**: Tasks can have automated reminder emails and text messages attached to them. These reminders are scheduled, sent, and tracked automatically.
- **Task performance tracking**: The system tracks how long tasks take from creation to completion, how many times they are reopened, and the last completion time. This data is used for performance reporting.
- Moving a case to Completed, Filed and Pending, or any status with archive behavior completes all pending tasks for the case — see [Case Status](./case-status.md).

### Dismissing and restoring tasks

The task list lets each team member clear items they no longer need to watch, without changing what anyone else sees or who the work belongs to.

- **Dismissing is per person.** Dismissing a task removes it from your own list only — everyone else, including whoever the task is assigned to, still sees it. Dismissals are remembered, so a task you cleared does not reappear the next time you open the list.
- **You can dismiss a task you are not assigned to.** Any team member who can see a task can dismiss it, including unassigned tasks and tasks that are already complete. Dismissing never reassigns the task or takes it away from another team member. Previously, dismissing a task that was assigned to someone else appeared to work but had no effect.
- **Restoring brings a task back.** A dismissed task can be restored to your list. If dismissing it also dropped your own assignment, restoring gives that assignment back; if you were not assigned at the time, restoring leaves assignment untouched.
- **Filtering by dismissal state.** The list shows **active** tasks by default — everything you have not dismissed. You can switch it to show **dismissed** tasks only, or **all** tasks regardless of dismissal.
- **Including completed tasks.** A separate setting adds completed tasks to the list alongside incomplete ones. It is off by default and is independent of the dismissal filter, so the two can be combined in any way — completed work you have not dismissed, dismissed work that is still open, and so on. The list previously showed incomplete tasks only, with no way to bring completed ones back into view.
- **Dismissals apply to your task inbox, not to a case.** The **Tasks** panel on a client and on a workflow shows every open task on that case, including ones you have dismissed from your own inbox, so everyone looking at the same case sees the same list. The task stays dismissed in your inbox. Previously a dismissed task was hidden from those panels too, so the person who dismissed it saw fewer open tasks on the case than their colleagues and the case could look further along than it was. Choosing to show **dismissed** tasks on those panels still works as before.

## Edge Cases & Limitations

- Dismissing a task does not complete it. The underlying work stays outstanding for whoever is assigned, and the task still counts toward the case's task totals — dismissal only controls whether it appears in your own list.

## Related Features

- [Status Tracking](./README.md)
- [Case Status](./case-status.md)
- [Task Templates](../task-templates.md)
- [Inbox](../../back-office/inbox.md)
- [PACER Integration](../../integrations/pacer/README.md)
