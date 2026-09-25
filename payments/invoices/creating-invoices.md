# Creating Invoices

## Overview

Invoices can be created manually, generated from reusable templates, or triggered automatically by workflows. Each invoice contains one or more line items and can carry an optional note to the client. This page covers the three ways to create an invoice, line items, the invoice note, and how invoice templates connect to workflows.

## Key Behaviors

### Ways to create an invoice

There are three ways to create an invoice:

- **Manually** — A firm user creates an invoice directly by adding line items, setting an amount, and assigning it to a client. The invoice starts in an active state and is immediately payable.
- **From a template** — Firms set up reusable invoice templates with predefined line items, payment settings, and amounts. Creating an invoice from a template copies all settings into a new invoice, saving time for recurring billing scenarios. See [Invoice Templates](./invoice-templates.md).
- **Via a workflow** — Invoices can be generated automatically as a step in a workflow (for example, after a client submits an intake form or books an appointment). Workflow-generated invoices start in a "generating" state while line items are being finalized, then become active once amounts are set. If a client pays at the start of a workflow before the invoice is formally created, the invoice is correctly marked as paid once it is finalized — it does not remain active as if payment were still outstanding.

### Line items

Every invoice contains one or more line items. Each line item includes:

| Field | Description |
|-------|-------------|
| **Name** | A short label for the charge (e.g., "Consultation fee") |
| **Unit price** | The cost per unit |
| **Quantity** | Number of units |
| **Description** | Optional additional detail about the charge |

The invoice total is calculated as the sum of (unit price x quantity) for each line item.

Line items can be defined on a template and copied automatically when creating an invoice, or added and edited manually on individual invoices.

### Invoice note

An invoice can carry an optional **invoice note** — a short, plain-text message shown to the client on the invoice. Firms use it to explain what is due and when, such as how and by when the invoice is expected to be paid.

- The note can be set on an invoice template, so every invoice created from that template starts with the same message.
- When a case is started from a template, the note pre-fills from the template and can be edited before the invoice is sent.
- Staff can add or change the note directly on an existing invoice at any time. Editing the note does not create a new invoice version and does not change the invoice's status — it is separate from making a correction to line items or amounts.
- The note is visible to the client. It appears next to the balance due in the client portal and on each invoice in the case invoice list, which both clients and firm staff can see.

## Configuration

### Workflow integration

When connecting an invoice template to a workflow:

- The template is linked to a specific workflow step.
- Invoices are generated automatically when that step is triggered.
- Auto-assignment rules control who is attached to the invoice (the firm, the client, specific collaborators).
- Conditional logic can determine whether an invoice is generated based on workflow context.

## Edge Cases & Limitations

- Workflow-generated invoices have no final amount while in the "generating" state; they become payable once amounts are set.

## Related Features

- [Invoices](./README.md)
- [Invoice Templates](./invoice-templates.md)
- [Editing and Versioning](./editing-and-versioning.md)
- [Invoice Lifecycle](./invoice-lifecycle.md)
- [Workflows](../../workflows/README.md) — How invoices integrate with automated workflows.
