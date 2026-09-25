# Switching a Case to Another Workflow

## Overview

A case can be switched to a different workflow — for example converting a Chapter 7 case to Chapter 13, or back. This page covers which workflows a case can be switched to and what carries over to the new case when it switches.

## Key Behaviors

### Choosing a workflow in another service

When you switch a case to a different workflow — for example moving a Chapter 7 case onto a Chapter 13 workflow after an attorney recommendation — you can choose any workflow your firm offers, not only the workflows in the service the case is already under.

- The choices are grouped by the service each workflow belongs to. A workflow that is not part of any service can still be chosen; it simply has no group.
- Only workflows your firm would start a new case on are offered. Disabled, retired, and draft workflows are not listed, and switching to them is refused.
- A case can only be switched to one of your own firm's workflows.

> TODO: Confirm where the workflow switch is started from on a case, and whether the picker opens on the case's current service by default.

### What carries over when a case switches workflow

When a case is switched to a different workflow, the client's credit report and the money they have already paid move to the new case.

- **The credit report moves even if the new case has started one of its own.** A new workflow often opens its own credit report step within seconds of being created, before the switch has finished. If that report has never actually been pulled, it is set aside (skipped, not deleted) and the client's real report — with its bureau results and documents — moves onto the new case. If your team has already pulled a report on the new case, that report is kept and the old one is not moved over it.
- **Payments already made carry forward even when the new fee is lower.** Changing chapter usually changes the fee, so the new invoice can be smaller than what the client has already paid. The new invoice is credited up to its full amount, and the case's switch record names the remaining amount as owed back to the client as a credit or refund.
- Previously, in both situations, that part of the switch failed. The credit report stayed on the archived case, and when the client had paid more than the new invoice, the payment was not recorded on either case — the only trace was the failure noted in the switch record, and your team had to repair the case by hand.

> TODO: Confirm where the switch record (the internal note listing each step of the switch) appears on the case, and whether cases switched before this correction need to be reviewed for a missing credit report or carried-over payment.

## Edge Cases & Limitations

- Disabled, retired, and draft workflows cannot be switched to.
- A case cannot be switched to another firm's workflow.

## Related Features

- [Status Tracking](./README.md)
- [Workflow Switch](../workflow-switch.md)
- [Credit Reports](../../intake/credit-reports/README.md)
- [Invoices](../../payments/invoices/README.md)
