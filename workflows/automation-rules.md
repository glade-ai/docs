# Automation Rules

## Overview

Automation rules in Glade are workflow definitions that automatically execute a sequence of actions when specific events occur. They are the core orchestration mechanism that connects triggers (events) to actions (side effects) within the workflow engine. Creators (legal professionals) configure automation rules per product or globally, and the system evaluates them whenever a matching event fires.

## Key Behaviors

- A workflow is a directed graph of **steps**, where each step is either a **trigger** (event listener) or an **action** (side effect). Steps are connected via dependency edges (`step_dependencies` join table).
- Steps are organized into **threads** — linear chains of trigger-action pairs that begin with a step that has no dependencies. Multiple threads can exist within a single workflow and are ordered by `rankOfThread`.
- When a trigger fires, the system looks up all enabled, non-archived, current-state workflows for the creator whose steps match the trigger event. If the trigger step has no prior dependencies, a new user workflow is created and execution begins.
- If a matching trigger step has dependencies (i.e., it is not the first step in a thread), the system checks for pending `StepTaken` records with unfulfilled external dependencies and completes them instead of starting a new workflow.
- Actions execute sequentially after a trigger completes. The supported action types are:
  - `send-message` — sends a message with optional attachments (invoices, form requests, document requests, booking links, custom terms, credit reports, e-signature requests)
  - `generate-all-workflow-pdfs` — generates all compiled PDF documents for the workflow
  - `send-e-signature-request` — sends an e-signature request
  - `send-document-request` — sends a document request
  - `send-email` — sends an email notification
- After an action succeeds, the system enables the next trigger(s) in the chain by creating `StepTaken` records with associated `WorkflowExternalDependency` entries. These external dependencies must be fulfilled (e.g., a form request completed, document uploaded) before the next trigger fires.
- Workflows can be scoped to a specific product (`referenceType: 'product'`, `referenceId` set) or apply globally across all products for a creator (`referenceId: null`).
- A workflow has a `state` field with values `current`, `draft`, or `stale`. Only workflows in the `current` state are evaluated for trigger matching.
- Workflows can be locked (`isLocked: true`) to prevent modification. Default global workflows (e.g., confirmation receipt, abandoned cart email, booking reminder) are locked.
- The system supports **re-execution** of actions via the `forceReexecute` flag, which allows retrying a previously executed step.

## Configuration

- **isEnabled**: Boolean toggle to activate or deactivate a workflow.
- **isArchived**: Boolean flag to soft-archive a workflow without deleting it.
- **isLocked**: Prevents editing of the workflow definition.
- **sendEmailToCreatorOnCompletion**: Sends a notification email to the creator when all steps complete.
- **sendEmailToCreatorOnFirstPayment**: Sends a notification when the first payment is received.
- **canInitiateAssociatedWorkflows**: Allows this workflow to start related workflows upon completion.
- **preserveWorkflowAssignment**: Keeps owner assignments when the workflow is duplicated.
- **enableUscisUpdates**: Enables USCIS case status tracking (immigration-specific).
- **enablePacerSubmissions**: Enables PACER court filing integration (bankruptcy/litigation-specific).
- **noodleFee**: Platform fee percentage applied to invoices in this workflow.
- **estimatedTotalFees**: Estimated total fees shown to clients.
- **type**: Either `basic` or `attorney-case`, which affects status progression behavior.
- **caseType**: Optional case categorization (e.g., for bankruptcy chapter types).
- **Workflow owners**: Persons assigned as default owners, copied to each new user workflow instance.
- **Step owner assignments**: Individual steps can require specific roles via `WorkflowStepOwnerAssignment`, which creates assignment tasks when the trigger fires.

## Edge Cases & Limitations

- The current implementation only supports a single `WorkflowExternalDependency` per step. Multiple concurrent dependencies on a single step are not fully supported.
- A circuit breaker (1000 iterations) prevents infinite loops when traversing thread step graphs, logging an error if circular dependencies are detected.
- When an action execution fails, the failure is logged and reported to Sentry, but the trigger is marked as failed rather than retried automatically.
- External dependency setup uses a polling mechanism (`waitForExternalDependenciesToBeSetup`) that retries up to 10 times at 1-second intervals, then once at 20 seconds, to handle race conditions where webhook events arrive before dependencies are created.
- Workflows in `draft` or `stale` state are not evaluated for trigger matching.

## Related Features

- [Triggers](./triggers.md) — the event types that initiate automation rule evaluation
- [Task Templates](./task-templates.md) — workflow templates that define reusable workflow configurations
- [Status Tracking](./status-tracking.md) — how user workflow status progresses as steps complete
