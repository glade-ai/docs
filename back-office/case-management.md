# Case Management

## Overview

Case management is the core back-office feature that allows legal professionals (creators) to track client matters from intake through completion. A "case" is represented by a `UserWorkflow` — an instance of a `Workflow` template assigned to a specific client (`Person`). Cases progress through configurable statuses, accumulate activity history, and can have multiple team members assigned as owners.

## Key Behaviors

- Each case (`UserWorkflow`) tracks a client (`personId`), a workflow template (`workflowId`), and an optional `caseId` that groups related workflows under a single logical case.
- Cases have a `status` field that uses creator-defined custom statuses (e.g., "Data Collection", "Processing", "Filed and Pending", "Completed", "Archived").
- Cases track progress via `numStepsTaken`, `numWorkflowSteps`, `numCompletedTasks`, `numTotalTasks`, and a computed `progress` float (0 to 1).
- Lifecycle timestamps record when a case is filed (`filedAt`), completed (`completedAt`), canceled (`canceledAt`), ended (`endedAt`), archived (`archivedAt`), and paused (`pausedUntil`).
- `lastActivityAt` is updated whenever significant activity occurs on the case, providing a recency signal for dashboards and reports.
- Cases can be initiated by a team member (`initiatedByPersonId`) and assigned to one or more owners via `UserWorkflowOwner`, each of whom can have workflow roles (e.g., Paralegal, Documents Team).
- The `isMainUserWorkflow` flag distinguishes the primary case from associated sub-workflows. Associated workflows are linked via `AssociatedUserWorkflow` and appear together in intake status reports.
- Case data is stored in an append-only `FieldVersion` table, keyed by `caseId` and `fieldPath`. Singleton fields (e.g., debtor SSN, attorney info) have `entityId = NULL`; repeated items (creditors, assets) are tracked via `CaseEntity` rows with their own field versions.
- All case activity is logged in `UserWorkflowActivity` with typed events including status changes, document uploads, payments, form completions, e-signature requests, court notices, and owner assignment changes.
- Cases support PACER integration for bankruptcy filings, tracked via `enablePacerSubmissions`, `caseNumber`, `fullCaseNumber`, and related court data.
- Tags (`tagIcon`, `tagText`) provide lightweight visual categorization on case list views.
- Collaborators (`UserWorkflowCollaborator`) control per-person permissions on a case, including `canAssign`, `canInviteCollaborators`, and `canReceiveCustomerNotifications`. Collaborator source tracks how they were added (manually, as customer, as organization member, etc.).

## Configuration

- **Custom statuses**: Creators define their own workflow statuses with title, icon, colour, and behavioral flags (`usesArchiveBehavior`, `disablesFollowups`). A set of default statuses is provisioned on creator setup (e.g., Data Collection, Processing, Filed and Pending, Completed, Archived).
- **Workflow templates**: Each case is an instance of a `Workflow`, which defines the steps, contexts, invoices, owners, and fee structure. Workflows have a `type` of either `basic` or `attorney-case`, and an optional `caseType`.
- **Followup cadence**: Configured at the creator level (`followupCadence`, `followupCadenceUnits`, `followupCadencePercentage`) to drive automated client follow-up reminders.
- **District templates**: Cases can be linked to a `DistrictTemplate` for court-specific configuration.

## Edge Cases & Limitations

- `USER_WORKFLOW_STATUS` is typed as `string` rather than an enum, meaning the system relies on custom status slugs matching correctly. Invalid status values are not prevented at the entity level.
- Soft-deleting a `CaseEntity` hides it from queries but preserves its `FieldVersion` rows for audit history. There is no cascade delete.
- The `FieldVersion` table is append-only with no `updatedAt` or `deletedAt` columns. A cleared field is represented by a new row with `value = NULL`, not by deletion.
- `previousWorkflowStatus` is nullable and only populated on status transitions; it may be `null` for newly created cases.

## Related Features

- [Reporting](./reporting.md) — intake status, paralegal, and documents reports operate on case data.
- [Staff Management](./staff-management.md) — team members are assigned as case owners with workflow roles.
- [Settings](./settings.md) — custom statuses, workflow templates, and followup cadence are configured at the creator level.
