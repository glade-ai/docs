# Case Management

## Overview

Case management is the core back-office feature that lets your firm track client matters from intake through completion. A "case" is a specific instance of a workflow template assigned to a client. Cases progress through configurable statuses, accumulate activity history, and can have multiple team members assigned.

## Key Behaviors

- Each case tracks a client, a workflow template, and optionally belongs to a logical case group that ties related workflows together.
- Cases have a status that uses your firm's custom statuses (e.g., "Data Collection", "Processing", "Filed and Pending", "Completed", "Archived").
- Cases track progress as a percentage based on steps taken and tasks completed.
- Cases record key lifecycle dates: when filed, completed, canceled, ended, archived, and paused until a future date.
- A "last activity" timestamp updates whenever significant activity occurs on a case, providing a recency signal for dashboards and reports.
- The case list can be sorted by any column, including Progress. Sorting by Progress orders cases by their completion percentage without affecting any active status or other filters.
- A **Last paid** column on the case list shows the date of the most recent succeeded payment on each case, so your team can scan which cases have had recent payment activity and which have gone quiet. Cases with no payments yet show an empty value; the column is sortable like the other date columns.
- Cases can be initiated by a specific team member and assigned to one or more owners, each of whom can have a role on that case (e.g., Paralegal, Documents Team).
- A case can be marked as the primary case, with associated sub-workflows linked to it. Associated workflows appear together in intake status reports.
- **Starting an associated case keeps each filer distinct.** When your team starts a new case from an existing one — for example, a joint Chapter 13 continuing as a Chapter 7 — the second filer is carried across as their own person, separate from the primary debtor. Previously the second filer's slot on the new case could be bound to the primary debtor's record, so both debtor slots showed the same name and the primary debtor's details were also written into the second filer's case data fields. Cases that were already affected are not repaired by this change; the second filer's details have to be corrected on those cases.
- Case data supports both single-value fields (e.g., debtor SSN, attorney info) and repeatable items (e.g., creditors, assets). The system preserves a full history of field changes for audit purposes.
- When two data sources provide different values for the same case field (for example, a questionnaire response and a manually entered value disagree on a party's address), the system flags the field as conflicted. You can resolve the conflict by selecting which value should be authoritative. The selected value becomes the active value for that field immediately after resolution.
- **Your team can read the case data it writes.** Any team member on the firm that owns a case can open that case's stored values, a field's change history, the breakdown of where each value came from, and the list of conflicted fields. These views were previously restricted to Glade staff, so a paralegal could enter a value and then be unable to read it back, and could resolve a conflict from the detail view while the conflicts list itself refused to load. If your team learned to ask Glade support to look up a stored value or a field's history, that is no longer necessary.
- Case data reads stay scoped to the firm: a team member can only open cases belonging to their own firm, and clients never have access to these views.
- All case activity is logged, including status changes, document uploads, payments, form completions, e-signature requests, court notices, and owner assignment changes. The activity log also records high-value actions that were previously not captured:
  - **Petition Check** — when a Petition Check is run, the log records it along with which required fields were still missing, so you can see when the case was validated and what was outstanding at the time.
  - **Case document generation** — when a case document is generated, the log records that the document was created.
  - **PACER filing** — when a case is successfully filed with PACER, the log records "Filed case with PACER" so the filing is part of the case's audit trail.
  - **Creditors omitted from or restored to the creditor matrix** — when a creditor is left off the creditor mailing matrix, or put back on it, the log records which creditor it was and which team member made the change, so the decision has a name and a date against it.

  These entries are deduplicated, so repeating the same action (for example, re-running a Petition Check or retrying a filing submission) does not clutter the log with duplicate entries.

  Creditor matrix entries are recorded when the schedules questionnaire is completed rather than at the moment the checkbox is ticked, because that is the point at which the matrix is compiled. Completing the questionnaire again without changing any of the checkboxes adds nothing, and regenerating the matrix as part of a filing does not add entries of its own.
- Cases support PACER integration for bankruptcy filings, including case number and court data tracking.
- A case's bankruptcy chapter is read correctly regardless of how it was recorded. Chapters saved by older versions of Glade were stored in a different form, and on those cases the chapter used to display as an unformatted value, while opening it for editing showed no chapter selected at all — as though the case had none. Both now show the recorded chapter. Nothing needs to be re-entered, and no stored value was changed. A chapter value Glade cannot interpret displays as a dash rather than as raw text.
- Searching by case number in the dashboard's global search finds the matching case even when that case number belongs to an **associated (non-primary) case** in a case group. Previously a case number stored on a linked, non-primary matter could be missed; searching now returns it. Searches by other fields (name, email, phone) continue to match primary cases.
- **Previewing a case the way the client sees it.** Your team can open a read-only preview of a client's workflow without signing in as the client. The preview renders exactly what the client gets — the same tasks, documents, invoices, and visibility rules, evaluated as though the client were looking at it — with the firm's own navigation left out, so nothing on screen is something the client cannot see. Everything in the preview is read-only: tasks cannot be completed, documents cannot be uploaded or removed, invoices cannot be paid, and messages cannot be posted on the client's behalf. Controls that only view something, such as opening a document to read it, still work. Use it to check what a client is actually looking at before calling them about it.
- Tags provide lightweight visual categorization (icon and text label) on case list views.
- Collaborators on a case have specific permissions: ability to assign team members, invite other collaborators, and receive customer notifications. The system tracks how each collaborator was added (manually, as a customer, as an organization member, etc.).

## Configuration

- **Custom statuses**: Your firm defines its own statuses with a title, icon, color, and behavioral flags. Some statuses can be configured to treat cases as archived or to disable automated follow-up reminders. A set of default statuses is created when your firm is set up (e.g., Data Collection, Processing, Filed and Pending, Completed, Archived).
- **Workflow templates**: Each case is based on a workflow template that defines the steps, contexts, invoices, owners, and fee structure. Workflow templates are either "basic" or "attorney-case" type, with an optional case type for further categorization.
- **Follow-up cadence**: Configured at the firm level to control how often automated client follow-up reminders are sent for outstanding tasks.
- **District templates**: Cases can be linked to a district template for court-specific configuration.

## Edge Cases & Limitations

- Custom statuses are free-text values, so entering an unrecognized status name does not produce an error. Make sure status names match exactly.
- Removing a repeatable item (e.g., a creditor) hides it from views but preserves its data history for audit purposes. It is not permanently deleted.
- Clearing a field value creates a new history entry rather than erasing previous values, so the full edit history is always retained.
- Creditor matrix entries in the activity log may appear with an unformatted label until the display text for them is finished. The creditor named on the entry and the team member it is attributed to are correct.
- Because creditor matrix entries are written when the schedules questionnaire is completed, a checkbox ticked and then unticked before completion leaves no entry — the log records the state the matrix was compiled with, not every intermediate change.
- The previous status of a case is only recorded when a status change occurs. Newly created cases do not have a previous status.

## Related Features

- [Reporting](./reporting.md) — intake status, paralegal, and documents reports operate on case data.
- [Staff Management](./staff-management.md) — team members are assigned as case owners with workflow roles.
- [Settings](./settings.md) — custom statuses, workflow templates, and follow-up cadence are configured at the firm level.
