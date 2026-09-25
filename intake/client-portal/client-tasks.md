# Client Tasks

## Overview

Tasks on the client portal home point clients at what they need to do next — respond to a comment, enroll in credit counseling, connect a bank account, and so on. This page covers how tasks relate to the portal's "active" indicators, what dismissing a task does, and the specific tasks the portal surfaces.

## Key Behaviors

### Active status comes from the item, not the task

The portal's "active" indicators and the Your next step card are driven by the underlying entity status, not by the task system. If a client dismisses a task whose underlying item (for example a document checklist) is still open and assigned to them, the home page continues to surface that item as their next step with the correct Open button.

### Dismissing tasks

- **Dismissing a task** — Dismissing a task clears it from the client's list; it does not complete the underlying item. Where the control is offered, it is a trash icon that shows a **Dismiss task** label when hovered. (It was previously an unlabeled arrow that clients often mistook for "open" rather than "clear.") Dismissing only removes the task from the client's own list — the task stays on your team's list, so nothing is lost from the firm's side when a client clears one.
- **Items on the path timeline can no longer be dismissed.** The dismiss control has been removed from path items, so a client cannot clear a step from their own path — a step they need to complete stays visible until it is done or your team removes it.

  > TODO: Confirm which client-portal surfaces still offer the dismiss control now that path items do not, so this section can name them.

### Task types

- **Respond to Comment tasks** — A "Respond to Comment" task opens the reply thread for that comment directly, so the client lands where they can reply rather than on the full conversation with the comment merely highlighted. On a comment row the dismiss control reads **No reply needed** rather than "Dismiss task", which is what dismissing one actually means — the client is saying the comment does not need an answer, not that the conversation is closed. Your team still sees the comment and the task afterward.
- **Credit counseling enrollment task** — When the firm sends a credit counseling enrollment request, a task to enroll appears on the client's portal home, labeled **Get Pre-Filing Credit Counseling** before the case is filed (or **Get Post-Filing Debtor Education** afterward). Opening the task takes the client straight to the enrollment form. On joint filings, both debtors receive the task. The task clears on its own once enrollment is completed or skipped, and the client receives automated follow-up reminders to enroll while it remains outstanding. The accompanying "enrollment details needed" message now opens the enrollment card directly, instead of pointing to a button that was not shown.
- **Connect Bank Account task** — When a bank statements step is active on the client's case, a **Connect Bank Account** task appears on the portal home alongside the client's other tasks. Opening it takes the client straight to the Bank Statements Organizer, and the task clears once the client connects an account or the step is skipped. See [Bank Statements](../bank-statements.md).
- **Tasks from linked workflows** — When a client's workflow is linked to other workflows, the client tasks from those linked workflows also appear on the portal home. The client sees every task assigned to them in one place, not only the tasks on their main workflow.

## Configuration

- Followup reminders can be configured on questionnaire templates and document request templates with a customizable frequency (minutes, hours, days, or weeks) to remind clients of pending tasks.

## Related Features

- [Client Portal](./README.md)
- [Portal Home Page](./home-page.md)
- [Bank Statements](../bank-statements.md)
- [Credit Counseling](../../workflows/credit-counseling.md)
