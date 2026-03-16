# Automation Rules

## Overview

Automation rules define what happens automatically when events occur during a case. Your firm configures these rules per service or globally, and the system runs them whenever the matching event takes place. For example, when a client purchases a service, the automation rule can send a welcome message, deliver a questionnaire, and request documents — all without manual intervention.

## Key Behaviors

- A workflow is a sequence of **steps** organized into **threads**. Each step is either a **trigger** (something that happens, like a client completing a questionnaire) or an **action** (something the system does in response, like sending a message). Steps run in order within a thread.
- A single workflow can contain multiple threads, each representing an independent sequence of steps. Threads are ordered by rank.
- When a trigger event occurs, the system checks all active workflows for your firm to see if any match. If a matching trigger is the first step in a thread, a new case is created and execution begins automatically.
- If a matching trigger is later in a thread (not the first step), the system checks whether the case is waiting for that event and advances the case accordingly.
- The available action types are:
  - **Send message** — sends a message to the client, optionally with attachments such as invoices, questionnaires, document requests, booking links, custom terms, credit report requests, or e-signature requests
  - **Generate all case PDFs** — compiles and generates all PDF documents for the case
  - **Send e-signature request** — sends a document for the client to sign electronically
  - **Send document request** — asks the client to upload specific documents
  - **Send email** — sends an email notification
- After an action completes, the system enables the next trigger in the sequence. That next trigger waits for the client to take the required action (such as completing a questionnaire or uploading a document) before the workflow continues.
- Workflows can apply to a specific service or apply globally across all services for your firm.
- A workflow can be in one of three states: **active**, **draft**, or **stale**. Only active workflows run automatically.
- You can lock a workflow to prevent accidental changes. Default system workflows (such as confirmation receipts, abandoned cart emails, and booking reminders) are locked automatically.
- If a step needs to be retried, your team can force re-execution of a previously completed action.

## Configuration

- **Enabled/disabled toggle**: Activate or deactivate a workflow without deleting it.
- **Archived**: Hide a workflow without deleting it. Archived workflows do not run.
- **Locked**: Prevent editing of the workflow. Useful for protecting default workflows.
- **Email on completion**: Send a notification to your team when all steps in a case finish.
- **Email on first payment**: Send a notification when the first payment is received on a case.
- **Start related workflows on completion**: Allow this workflow to automatically kick off related workflows when it finishes.
- **Preserve assignments on duplication**: Keep team member assignments when a workflow is copied.
- **USCIS updates**: Enable automatic USCIS case status tracking (immigration cases).
- **PACER submissions**: Enable PACER court filing integration (bankruptcy/litigation cases).
- **Platform fee**: Fee percentage applied to invoices in this workflow.
- **Estimated total fees**: Estimated total fees shown to clients before they purchase.
- **Workflow type**: Either "basic" or "attorney case", which affects how status progression works.
- **Case type**: Optional categorization (e.g., bankruptcy chapter type).
- **Workflow owners**: Team members assigned as default owners for every new case created from this workflow.
- **Step assignments**: Individual steps can require a specific team role. If the required role is not assigned when the step runs, the system creates an assignment task.

## Edge Cases & Limitations

- Each step currently supports only one required client action at a time. A single step cannot wait for multiple things simultaneously (e.g., both a questionnaire and a document upload).
- If an action fails to execute, the failure is logged and the step is marked as failed. The system does not automatically retry failed actions.
- Only active workflows are evaluated. Workflows in draft or stale state are ignored.

## Related Features

- [Triggers](./triggers.md) — the event types that start or advance automation rules
- [Task Templates](./task-templates.md) — reusable templates that define complete workflow configurations
- [Status Tracking](./status-tracking.md) — how case status progresses as steps complete
