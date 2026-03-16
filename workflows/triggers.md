# Triggers

## Overview

Triggers are the events that start or advance a workflow. When something happens in the system — a client purchases a service, completes a questionnaire, or uploads documents — the workflow engine checks for matching triggers and moves the relevant cases forward. Triggers are the entry points and continuation points that connect real-world client actions to automated workflow steps.

## Key Behaviors

- Each trigger listens for a specific type of event. The available trigger types are:
  - **Product purchased** — a client completes payment for a service
  - **Purchase initiated** — a client starts a purchase (before payment completes)
  - **Questionnaire completed** — a client finishes or skips a questionnaire
  - **Documents uploaded** — a client uploads all required documents in a document request
  - **Custom terms agreed** — a client agrees to custom legal terms or agreements
  - **Credit report completed** — a credit report pull finishes
  - **Cart abandoned** — a client starts a purchase but does not complete it (fires on a schedule)
  - **Upcoming booking** — fires as a reminder before a scheduled consultation
  - **Booking scheduled** — a client schedules a consultation
  - **Start new thread** — a call-to-action button is clicked to begin a new sequence within the workflow
  - **Continue thread** — starts a new sequence within an existing case, optionally waiting until specific prerequisite items are completed first
  - **Client action taken** — a client-initiated action within a case triggers the next step
  - **All prerequisites met** — fires when all prior steps in the workflow are complete, rather than waiting for a specific client action
  - **E-signature request sent** — an e-signature request is created and delivered
  - **E-signature completed** — a client finishes signing an e-signature document
- When a trigger event occurs, the system handles it in two ways:
  1. **Starting a new case**: If the trigger is the first step in a workflow thread and the workflow is active, a new case is created for the client.
  2. **Advancing an existing case**: If the trigger is later in a workflow thread, the system finds cases that are waiting for this event and advances them.
- A trigger is considered complete when the required client action has been fulfilled. At that point, the system runs the actions that follow the trigger in the workflow.
- When a trigger completes, it can automatically update the case status (see [Status Tracking](./status-tracking.md)). This is configured per step.
- A trigger that starts a new thread can be gated by prerequisites — it only fires after specific questionnaires, document requests, or other items are completed first.
- Skipping a questionnaire counts the same as completing it for trigger purposes.

## Configuration

- **Trigger type**: Which event this trigger listens for (one of the types listed above).
- **Required**: Whether this trigger must be completed for the case to be considered finished.
- **Status on completion**: An optional case status to set automatically when this trigger completes.
- **Title**: An optional human-readable label for the trigger step.
- **Thread order**: Determines the display order when the trigger is the first step in a thread.
- **Team role assignments**: A trigger step can require a specific team role to be assigned before it proceeds. If the role is not assigned, the system creates a task to assign it.
- **Step order**: Triggers can depend on prior steps in the workflow. A trigger with prior steps only fires after those steps complete.
- **Prerequisite items**: Triggers of the "continue thread" type can wait for specific items to be completed before firing. Supported item types include: document requests, questionnaires, credit reports, custom terms, invoices, bookings, e-signature requests, bank account integrations, purchase references, team assignments, and general conditions.

## Edge Cases & Limitations

- Each trigger step currently supports only one required action at a time. A single trigger cannot wait for multiple unrelated client actions simultaneously.
- If a client completes an action very quickly (before the system has finished setting up the workflow), the system retries for up to approximately 30 seconds before giving up.
- Skipped questionnaires are treated the same as completed questionnaires.
- The "all prerequisites met" trigger type fires based on prior workflow steps being complete, rather than waiting for a specific client action.
- Triggers in draft or stale workflows are never evaluated.

## Related Features

- [Automation Rules](./automation-rules.md) — the workflows that contain trigger steps
- [Status Tracking](./status-tracking.md) — automatic status updates driven by trigger completion
- [Task Templates](./task-templates.md) — templates that define trigger-action sequences
