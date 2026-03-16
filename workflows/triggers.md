# Triggers

## Overview

Triggers are event-driven workflow steps that listen for specific events in the system and initiate or continue workflow execution. They form the entry points and continuation points in a workflow's step graph. When an external event occurs (e.g., a product is purchased, a form is completed), the workflow engine evaluates all matching triggers and advances the relevant workflows.

## Key Behaviors

- Triggers are workflow steps with `type: 'trigger'`. Each trigger has an `eventName` that corresponds to a specific system event.
- The supported trigger types are:
  - `product-purchased` — fires when a product purchase payment succeeds
  - `purchase-initiated` — fires when a purchase is started (before payment completes)
  - `form-request-completed` — fires when a form request (questionnaire) is completed or skipped
  - `documents-uploaded` — fires when all required documents in a document request are uploaded
  - `custom-terms-agreed` — fires when a client agrees to custom terms/agreements
  - `credit-report-completed` — fires when a credit report pull completes
  - `cart-abandoned` — fires when a shopping cart is abandoned (scheduled event)
  - `upcoming-booking` — fires as a reminder before a scheduled booking
  - `booking-scheduled` — fires when a booking is scheduled
  - `initiate-cta` — fires when a call-to-action button is clicked to start a new workflow thread
  - `initiate-thread` — fires to start a new thread within an existing workflow, optionally gated by building block dependencies
  - `user-workflow-cta` — fires when a user-initiated action within a workflow is triggered
  - `all-dependencies` — fires when all external dependencies on the step are fulfilled
  - `e-signature-request-created` — fires when an e-signature request is created
  - `e-signature-request-completed` — fires when an e-signature is completed
- Trigger processing follows a two-phase approach:
  1. **New workflow triggers**: The system finds all matching trigger steps that have no dependencies (i.e., they start a thread) in enabled, non-archived, current-state workflows for the creator. For each match, it creates a new `UserWorkflow` and a `StepTaken` record.
  2. **Continuation triggers**: The system finds all pending `StepTaken` records that have unfulfilled `WorkflowExternalDependency` entries matching the event's reference. It marks those dependencies as completed.
- A trigger is considered complete when all its external dependencies are fulfilled. At that point, the system executes the trigger's downstream actions.
- Triggers listen to events from multiple services via the event listener pattern. Each listener file translates a service event into an `ExecuteEventData` object containing the trigger type, creator ID, person ID, and external reference information.
- The event listeners that feed triggers include: `purchase`, `formRequest`, `creditReport`, `documentRequest`, `customTerms`, `invoice`, `messages`, `payment`, `scheduledEvents`, `scheduling`, `creator`, and `userWorkflowOwner`.
- When a trigger step has a `workflowStatus` field set, the user workflow's status is automatically updated to that value when the trigger completes (see [Status Tracking](./status-tracking.md)).
- Trigger steps can have **building block dependencies** (`BuildingBlockDependency`) that gate thread initiation on the completion of specific form requests, document requests, or other building blocks.

## Configuration

- **eventName**: The trigger type (one of the `WORKFLOW_TRIGGERS` enum values).
- **isRequired**: Whether the trigger step must be completed for the workflow to be considered complete.
- **workflowStatus**: Optional status string to set on the user workflow when this trigger completes.
- **title**: Optional human-readable title for the trigger step.
- **rankOfThread**: Determines the ordering of threads when the trigger is the first step in a thread.
- **Owner assignments**: Trigger steps can have `WorkflowStepOwnerAssignment` records that require specific roles to be assigned before execution continues. If the required role is not assigned, an `assign-workflow-step` task is created.
- **Step dependencies**: Triggers can depend on prior steps (triggers or actions) via the `step_dependencies` join table. A trigger with dependencies only fires when those prior steps have completed.
- **External dependencies**: When a trigger is enabled (via `enableNextTrigger`), `WorkflowExternalDependency` records are created to track what external events must occur before the trigger fires. These reference types include: `document-request-user`, `form-request`, `credit-report`, `custom-terms`, `invoice`, `booking`, `e-signature-request`, `bank-account-integration`, `workflow-purchase-reference`, `workflow-owner-assignment`, and `global`.

## Edge Cases & Limitations

- A trigger step currently supports only a single external dependency check at a time. Multiple concurrent external dependencies on a single trigger are noted as a limitation in the codebase.
- If a trigger's external dependencies are not yet set up when the completing event arrives (race condition), the system retries with polling (up to ~30 seconds) before giving up.
- Skipped form requests are treated the same as completed form requests for trigger evaluation purposes.
- The `all-dependencies` trigger type is a meta-trigger that fires when all prior step dependencies are met, rather than listening for a specific external event.
- Triggers in workflows with `state: 'draft'` or `state: 'stale'` are never evaluated.

## Related Features

- [Automation Rules](./automation-rules.md) — the workflow definitions that contain trigger steps
- [Status Tracking](./status-tracking.md) — automatic status updates driven by trigger completion
- [Task Templates](./task-templates.md) — templates that define trigger-action sequences
