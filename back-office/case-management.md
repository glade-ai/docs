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
- Cases can be initiated by a specific team member and assigned to one or more owners, each of whom can have a role on that case (e.g., Paralegal, Documents Team).
- A case can be marked as the primary case, with associated sub-workflows linked to it. Associated workflows appear together in intake status reports.
- Case data supports both single-value fields (e.g., debtor SSN, attorney info) and repeatable items (e.g., creditors, assets). The system preserves a full history of field changes for audit purposes.
- All case activity is logged, including status changes, document uploads, payments, form completions, e-signature requests, court notices, and owner assignment changes.
- Cases support PACER integration for bankruptcy filings, including case number and court data tracking.
- Tags provide lightweight visual categorization (icon and text label) on case list views.
- Collaborators on a case have specific permissions: ability to assign team members, invite other collaborators, and receive customer notifications. The system tracks how each collaborator was added (manually, as a customer, as an organization member, etc.).

## Configuration

- **Custom statuses**: Your firm defines its own statuses with a title, icon, color, and behavioral flags. Some statuses can be configured to treat cases as archived or to disable automated follow-up reminders. A set of default statuses is created when your firm is set up (e.g., Data Collection, Processing, Filed and Pending, Completed, Archived).
- **Workflow templates**: Each case is based on a workflow template that defines the steps, contexts, invoices, owners, and fee structure. Workflow templates are either "basic" or "attorney-case" type, with an optional case type for further categorization.
- **Follow-up cadence**: Configured at the firm level to control how often automated client follow-up reminders are sent for outstanding tasks.
- **District templates**: Cases can be linked to a district template for court-specific filing configuration. The district template editor shows an info tooltip for each field label so you can learn what a field does without leaving the page. Document configurations that share the same display name (for example, Ch. 7 and Ch. 13 variants of the same petition type) are grouped under a single collapsible header with condition labels for each variant, reducing visual clutter when a district has many document types configured.

## Edge Cases & Limitations

- Custom statuses are free-text values, so entering an unrecognized status name does not produce an error. Make sure status names match exactly.
- Removing a repeatable item (e.g., a creditor) hides it from views but preserves its data history for audit purposes. It is not permanently deleted.
- Clearing a field value creates a new history entry rather than erasing previous values, so the full edit history is always retained.
- The previous status of a case is only recorded when a status change occurs. Newly created cases do not have a previous status.

## Related Features

- [Reporting](./reporting.md) — intake status, paralegal, and documents reports operate on case data.
- [Staff Management](./staff-management.md) — team members are assigned as case owners with workflow roles.
- [Settings](./settings.md) — custom statuses, workflow templates, and follow-up cadence are configured at the firm level.
