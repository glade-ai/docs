# Managing a Payment Plan

## Overview

Firms manage payment plans from the transactions dashboard: they can modify a plan's settings or individual installments, cancel it, and see how it responds to invoice edits and payments made outside the plan. This page covers the plan lifecycle, modifying and canceling plans, what happens when the invoice is edited, external payments, and how Glade keeps a plan's schedule covering what the invoice still owes.

## Key Behaviors

### Payment plan lifecycle

A payment plan moves through the following statuses over its lifetime:

| Status | Meaning |
|--------|---------|
| Active | Plan is running and installments are being charged on schedule |
| Completed | All installments have been paid and the invoice is fully settled |
| Canceled | Plan was manually canceled by the firm, or automatically canceled because the invoice was voided or skipped |
| Failed | Plan encountered unrecoverable payment failures (rare) |

### Firm management experience

- Firms view and manage payment plans from the transactions dashboard.
- Plan details show: status, frequency, installment amount, next payment date, and payment history. Deferred installments appear in the schedule alongside upcoming and paid ones, so you can see the full picture of what has been collected, postponed, and is still expected.
- Firms can modify plan settings, cancel plans, or adjust individual installments from this view — including rescheduling an installment that is stuck retrying (see [Rescheduling a retrying installment](./installments-and-retries.md#rescheduling-a-retrying-installment)).

### Modifying a payment plan

- Firms can modify an active payment plan at any time.
- The following changes can be made: installment amount, frequency, payment method, and next payment date.
- Individual installments can also be adjusted (amount or date).
- When a plan is modified, the remaining schedule is recalculated to reflect the new settings. Any values you have manually entered for the plan — such as the installment amount — are preserved and take precedence over recalculated defaults.
- **The schedule always adds up to what the invoice still owes.** Deleting an installment, editing one, or refunding a payment that has already been collected can leave a plan scheduled for less than the outstanding balance. Glade corrects this at the moment it happens rather than waiting: where the schedule falls short, installments are added to cover the difference; where it overshoots, the surplus is trimmed from the end. The plan goes on to collect the full amount either way. Previously the correction came only from the overnight health check, so a plan could sit under-scheduled for up to a day — and a plan that reached its last installment in that window would finish while the invoice still had a balance on it.
- Clients cannot modify their own plans. Only firms can make changes.

### What happens to a plan when the invoice is edited

Editing an invoice's line items or amounts replaces it with a new version (see [Invoices](../invoices/README.md)). An active payment plan moves across to the new version rather than being canceled, so the client's autopay arrangement stays in place and their stored payment method keeps being charged on schedule.

- The plan and its remaining schedule carry over to the new invoice. Nothing is canceled and the client is not asked to set the plan up again.
- **If the edit raises the invoice total** and the plan's remaining installments no longer cover what is due, installments are added on the plan's existing schedule until the full balance is covered.
- **If the edit lowers the invoice total** and the plan is now scheduled to collect more than is due, the schedule is left alone. Trimming it is a decision for your team — review the plan and adjust or remove the surplus installments yourself.
- **If the payments already collected cover the new total**, the remaining scheduled installments are canceled and no further charges are made.
- The plan is recorded as updated rather than canceled, so the case history shows the plan continuing across the edit.

Previously, editing an invoice canceled any active payment plan on it, silently ending the client's autopay agreement — the plan had to be rebuilt by hand and the client re-entered their payment details. If your team avoided editing invoices for this reason, it is now safe.

### Canceling a payment plan

- Firms can cancel an active plan at any time.
- Cancellation stops all future scheduled payments immediately.
- Payments already collected are not reversed.
- The invoice returns to its normal state with the remaining balance still due.
- Voiding or skipping an invoice automatically cancels any active payment plan on that invoice.
- **A plan cannot be set up on an invoice that can no longer be paid.** If a client tries to create a plan on an invoice that has been voided or is otherwise no longer payable — for example from a page they opened before the firm voided and replaced the invoice — the request is refused with an error. The client should set up the plan on the current invoice instead. Previously the plan was accepted, stayed active with nothing to collect, and every scheduled charge silently did nothing.
- Canceling a workflow with linked invoices also cancels the associated payment plans.

### External payments applied to a plan

- If a client makes a one-time payment outside the plan (for example, a manual payment or a direct payment on the invoice), the system applies it to the plan.
- The payment is applied to the next upcoming installment(s) in order.
- If the external payment covers one or more full installments, those installments are marked as paid.
- If it partially covers an installment, the remaining expected amount for that installment is reduced.
- The overall plan schedule is recalculated to reflect the payment.

## Configuration

| Setting | Description |
|---------|-------------|
| Payment method | The plan uses a single stored payment method selected at setup. Changing it applies to all future installments. |

## Edge Cases & Limitations

- Clients cannot modify their own plans. Only firms can make changes.
- Changing the payment method on a plan applies to all future installments, not just the next one.
- When an invoice edit lowers the total, a plan that is now over-scheduled is not trimmed automatically. Review the remaining installments and remove or reduce the surplus yourself.
- Payment plan health is monitored daily. Stalled or misconfigured plans are flagged to operations for review.
- The daily health check remains the backstop for plans whose schedule no longer covers the remaining balance — deleting or editing an installment and refunding a payment are corrected as they happen, but other routes to a short schedule, such as a client pre-paying installments until there are no longer enough upcoming payments to cover what's still due, are caught by the overnight check. New installments are added on the plan's original schedule (the start date plus the chosen interval), never on a date that falls before tomorrow, and never before an existing pre-paid installment that sits further out in the future. Months are honored: a plan whose installment day is the 31st falls back to the 28th in February and to the 30th in April, then returns to the 31st in months that have one, rather than drifting permanently to an earlier day.

## Related Features

- [Payment Plans](./README.md)
- [Installments, Retries, and Fees](./installments-and-retries.md)
- [Exporting Payment Plans](./exporting-payment-plans.md)
- [Invoices](../invoices/README.md)
- [Payment Tracking](../payment-tracking.md)
