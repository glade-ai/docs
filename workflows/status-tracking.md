# Status Tracking

## Overview

Status tracking governs how a user workflow's status and progress change over its lifecycle. Each user workflow (an instance of a workflow for a specific client) has a status, a numeric progress value, and counters for steps and tasks. Status transitions happen automatically when triggers complete and can also be changed manually by creators. The system supports both built-in statuses and creator-defined custom statuses.

## Key Behaviors

- A **user workflow** (`UserWorkflow`) tracks the state of a specific client's progression through a workflow. Key fields include:
  - `status` — a string representing the current lifecycle phase
  - `progress` — a float between 0 and 1 representing overall completion
  - `numStepsTaken` / `numWorkflowSteps` — count of completed steps vs total steps
  - `numCompletedTasks` / `numTotalTasks` — count of completed tasks vs total tasks
  - `lastActivityAt` — timestamp of the most recent activity
- **Automatic status updates**: When a trigger step completes, if that step has a `workflowStatus` field set, the user workflow's status is updated to that value. This allows workflow designers to define status transitions as part of the workflow step graph.
- **Progress calculation**: After each trigger completes, the system recalculates progress by examining all workflow steps, steps taken, and associated messages/attachments. The `calculateUserWorkflowProgress` method computes `numStepsTaken`, `numWorkflowSteps`, `numCompletedTasks`, `numTotalTasks`, and an `isCompleted` flag.
- **Automatic completion**: The `calculateNextStatus` method determines if a workflow should transition to `completed` status based on whether all steps are done. For `attorney-case` type workflows, certain slugs may have special completion logic.
- **Manual status changes**: Creators can manually update a user workflow's status via the API. The system validates the status change and emits a `USER_WORKFLOW_CHANGED` event.
- **Built-in default statuses** (created for each new creator):
  - `data-collection` (Data Collection) — initial phase where client information is gathered
  - `preparing-case` (Processing) — case is being prepared
  - `filed-and-pending` (Filed and Pending) — case has been filed, awaiting resolution
  - `completed` (Completed) — workflow is done
  - `archived` (Archived) — workflow is archived/inactive
  - Additional defaults include: `initiated`, `retained`, `triage`, `document-collection`, `credit-report-pulled`, `questionnaire-collection`, `petition-prep`, `final-review`, `ready-to-file`, `signed-paid`, `post-filing`, `retaining`, `bankruptcy-forms`
- **Custom statuses**: Creators can define their own statuses with custom titles, icons, and colors. Each custom status has:
  - `slug` — unique identifier per creator
  - `title` — display name
  - `icon` — one of a predefined set of icons (Archive, CheckCircle, Clock, Files, etc.)
  - `colour` — hex color code
  - `usesArchiveBehavior` — when true, transitioning to this status triggers the same side effects as archiving (completing all pending tasks, promoting associated workflows)
  - `disablesFollowups` — when true, suppresses automated followup emails/reminders for workflows in this status
- **Status change side effects**:
  - Transitioning to `completed`, `filed-and-pending`, or any status with `usesArchiveBehavior` completes all pending tasks for the user workflow.
  - Transitioning to `archived` sets `archivedAt`, preserves the previous status in `previousWorkflowStatus`, and promotes any associated workflows to main.
  - Transitioning to `unarchived` restores the previous status from `previousWorkflowStatus` (defaulting to `data-collection`) and clears `archivedAt`.
  - Transitioning to `filed-and-pending` sets the `filedAt` timestamp; transitioning back to `data-collection` or `preparing-case` clears it.
  - Transitioning to `completed` sets the `completedAt` timestamp.
- **Activity logging**: Status changes are recorded as `UserWorkflowActivity` entries with type `status-change`. Other activity types track document uploads, form completions, payments, comments, and more.
- **Pause/resume**: User workflows can be paused until a specific date (`pausedUntil`). Pausing and resuming emit separate events that downstream listeners can react to.
- **Task lifecycle**: Tasks are actionable items created during workflow execution (e.g., "complete form request", "pay invoice", "upload document"). Each task has an `action` type, a `referenceType` and `referenceId` linking it to the relevant entity, and a `completedAt` timestamp. Tasks are assigned to persons and belong to a user workflow.
- **Task followups**: Automated reminder emails/SMS linked to tasks via `TaskFollowup` and `FollowupHistory`. Followups are scheduled, sent, or canceled, and track the message content and delivery type.
- **Task efficiency**: The `TaskEfficiency` entity tracks how long tasks take from creation (`startedAt`) to first completion (`firstCompletedAt`), how many times they are reopened (`reopenCount`), and the last completion time (`lastCompletedAt`). This is used for performance reporting.

## Configuration

- **Custom statuses**: Created and managed per creator. Each status has a unique slug within the creator's scope, a display title, icon, colour, and optional behavioral flags (`usesArchiveBehavior`, `disablesFollowups`).
- **workflowStatus on steps**: Individual workflow steps can have a `workflowStatus` string that determines what status the user workflow transitions to when that step's trigger completes.
- **Workflow type**: The `type` field on a workflow (`basic` or `attorney-case`) affects how automatic status progression and completion logic behave.

## Edge Cases & Limitations

- The `status` field on `UserWorkflow` is typed as a plain string, not an enum. Any string value can be set, though the system expects it to match either a built-in or custom status slug.
- When a user workflow is archived and then unarchived, it restores to the `previousWorkflowStatus` value. If that value is null, it defaults to `data-collection`.
- Custom statuses with `usesArchiveBehavior` trigger the same task completion logic as the built-in `archived` status, but the user workflow's `status` field retains the custom status slug rather than changing to `archived`.
- Progress recalculation examines all steps and messages each time, which may be expensive for workflows with many steps.
- The `completedAt` timestamp is preserved when archiving so it can be restored if unarchived.

## Related Features

- [Automation Rules](./automation-rules.md) — the workflow definitions whose execution drives status changes
- [Triggers](./triggers.md) — trigger completion drives automatic status updates
- [Task Templates](./task-templates.md) — templates that define the initial workflow structure and steps
