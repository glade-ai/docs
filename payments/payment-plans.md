# Payment Plans

## Overview

Payment plans allow clients to pay invoices in scheduled installments rather than a single lump sum. Firms configure the available options, and clients (or firms on their behalf) set up a plan by choosing an installment amount, frequency, and start date. Glade automatically charges the client's stored payment method on each scheduled date until the invoice is fully paid.

## Key Behaviors

### Setting up a payment plan

- Payment plans are created on an invoice. Only one active payment plan can exist per invoice at a time.
- Either the client or the firm can set up a plan.
- Setup requires four inputs: installment amount, frequency, start date, and a saved payment method.
- The system generates a schedule of individual installments based on these inputs.
- The plan starts on the selected start date and charges repeat at the chosen frequency until the invoice balance reaches zero.

### Supported frequencies

- **Weekly** — every 7 days
- **Every two weeks** — every 14 days (this option was previously labeled "Biweekly")
- **Semi-monthly (1st & 15th)** — twice a month, billed on the 1st and the 15th
- **Monthly** — every calendar month

These frequencies are available to anyone setting up a new plan; there is no setting to restrict which one a client can choose.

When you choose **semi-monthly**, the first installment moves forward to the next 1st or 15th on or after the start date you pick, and the remaining installments then fall on the 1st and 15th of each month. Every other frequency starts on the exact start date you choose.

**About "Bimonthly":** Plans created before semi-monthly billing was introduced may use a **Bimonthly** frequency, which bills once every two months. Bimonthly is no longer offered when setting up a new plan, but existing bimonthly plans keep running and continue to display as "Every 2 months."

### How installments work

- Each installment is a scheduled payment for a fixed amount.
- On the scheduled date, Glade automatically charges the client's stored payment method.
- The installment amount is the same for every payment except possibly the final one, which covers only the remaining balance if it is less than the standard installment amount.
- Each installment is tracked individually with its own status:

| Status | Meaning |
|--------|---------|
| Upcoming | Scheduled but not yet charged |
| Paid | Successfully charged |
| Deferred | The installment has been postponed. The amount is not collected on the original date and remains outstanding |
| Failed | All charge attempts exhausted without success |
| Retrying | Initial charge failed; automatic retry pending |

### Payment plan lifecycle

A payment plan moves through the following statuses over its lifetime:

| Status | Meaning |
|--------|---------|
| Active | Plan is running and installments are being charged on schedule |
| Completed | All installments have been paid and the invoice is fully settled |
| Canceled | Plan was manually canceled by the firm, or automatically canceled because the invoice was voided or skipped |
| Failed | Plan encountered unrecoverable payment failures (rare) |

### Failed installments and retries

- If a scheduled payment fails (for example, insufficient funds or an expired card), the system automatically retries.
- The system makes up to 3 total attempts: the initial attempt plus 2 retries.
- Retries are scheduled automatically after each failure.
- If all 3 attempts fail, the installment is marked as failed.
- Both the client and the firm are notified by email when retries are exhausted.
- The plan itself remains active. The failed amount rolls into future installments or requires manual intervention by the firm.
- Payment plan charges are processed as off-session payments. If a card requires 3D Secure authentication, the client receives a notification to complete authentication separately — the system does not attempt an automatic 3D Secure challenge during a retry. This prevents spurious authentication prompts for clients whose cards have 3D Secure enabled.
- **Pending payment guard**: If a payment attempt is already in progress when a new charge or retry is due, the system waits for the in-flight attempt to resolve before initiating another. This prevents duplicate charges and eliminates the spurious failure notifications that would otherwise occur when a retry is triggered while a previous attempt is still processing.

### Rescheduling a retrying installment

When an installment is **Retrying** — its initial charge failed and an automatic retry is still pending — firm staff can move it to a new date from the transactions dashboard. Open the installment's actions menu and choose **Edit installment**, then pick a new date.

- The new date must be at least tomorrow in the firm's time zone. If the retry's original date has already passed, the date picker starts on tomorrow instead of the stale past date.
- Saving a new date returns the installment to **Upcoming**, clears the pending retry, and schedules a fresh charge attempt for the date you chose.
- Only the date can be changed from this menu on a retrying installment. The delete option is not offered for retrying rows — it remains available only for upcoming installments dated in the future.
- The charge is scheduled for the exact date you pick; it no longer shifts by a day for firms in certain time zones.

Previously the actions menu appeared only for upcoming installments with a future date. Because a retry's date is always in the past, a stuck retry could not be moved or recovered from the dashboard and required manual intervention on the payment data. Firm staff can now resolve it directly.

### Modifying a payment plan

- Firms can modify an active payment plan at any time.
- The following changes can be made: installment amount, frequency, payment method, and next payment date.
- Individual installments can also be adjusted (amount or date).
- When a plan is modified, the remaining schedule is recalculated to reflect the new settings. Any values you have manually entered for the plan — such as the installment amount — are preserved and take precedence over recalculated defaults.
- **The schedule always adds up to what the invoice still owes.** Deleting an installment, editing one, or refunding a payment that has already been collected can leave a plan scheduled for less than the outstanding balance. Glade corrects this at the moment it happens rather than waiting: where the schedule falls short, installments are added to cover the difference; where it overshoots, the surplus is trimmed from the end. The plan goes on to collect the full amount either way. Previously the correction came only from the overnight health check, so a plan could sit under-scheduled for up to a day — and a plan that reached its last installment in that window would finish while the invoice still had a balance on it.
- Clients cannot modify their own plans. Only firms can make changes.

### What happens to a plan when the invoice is edited

Editing an invoice's line items or amounts replaces it with a new version (see [Invoices](./invoices.md)). An active payment plan moves across to the new version rather than being canceled, so the client's autopay arrangement stays in place and their stored payment method keeps being charged on schedule.

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
- Canceling a workflow with linked invoices also cancels the associated payment plans.

### External payments applied to a plan

- If a client makes a one-time payment outside the plan (for example, a manual payment or a direct payment on the invoice), the system applies it to the plan.
- The payment is applied to the next upcoming installment(s) in order.
- If the external payment covers one or more full installments, those installments are marked as paid.
- If it partially covers an installment, the remaining expected amount for that installment is reduced.
- The overall plan schedule is recalculated to reflect the payment.

### Maximum plan duration

- Invoice templates can set a maximum payment plan duration, measured in months.
- When a maximum is set, clients cannot create plans that would extend beyond that limit.
- The system calculates total duration based on the number of installments multiplied by the frequency interval.
- If a client's proposed plan exceeds the limit, they see an error asking them to increase the installment amount.
- Firm staff can override this limit when setting up plans on behalf of clients.

### Minimum installment amount

- Invoice templates can set a **minimum amount** for payment plans. When set, each installment in a plan must be at least this amount.
- The minimum is enforced when a plan is set up: a proposed plan whose installment falls below the minimum is rejected, prompting a larger installment (or a shorter schedule).
- This minimum applies **only** to payment plan installments. It does not affect one-time custom payments on the invoice — a client paying a single custom amount can pay below this threshold (see [Invoices](./invoices.md)).

### Processing fees on payment plans

- If "pass processing fees to customer" is enabled on the invoice, fees apply to each installment individually.
- Fees are calculated at the time each installment is charged, not upfront.
- The fee amount depends on the payment method used (card fees differ from ACH fees).

### Notifications

- The firm is notified when a payment plan is created, if email notifications are enabled on the invoice template.
- The firm is notified when a plan is modified.
- Both the client and firm are notified when a payment fails after all retry attempts are exhausted.
- Standard payment confirmation emails are sent for each successful installment.

### Client experience

- From the invoice payment page, clients can choose to set up a payment plan if partial payments are enabled on the invoice.
- Setup is a two-step process: first configure the plan settings (amount, frequency, start date), then select a payment method.
- The client sees the full installment schedule before confirming.
- Duration warnings appear if the plan approaches or exceeds the maximum duration limit.
- After setup, payments are charged automatically with no further action required from the client.
- When a client's invoice is on an active plan, the client portal home Balance card reflects it: the card shows the installment amount and cadence (for example, "$200.00 monthly") and the next payment date, so a client paying down a balance sees their plan summarized at a glance. Completed or canceled plans are not shown there.

### Firm management experience

- Firms view and manage payment plans from the transactions dashboard.
- Plan details show: status, frequency, installment amount, next payment date, and payment history. Deferred installments appear in the schedule alongside upcoming and paid ones, so you can see the full picture of what has been collected, postponed, and is still expected.
- Firms can modify plan settings, cancel plans, or adjust individual installments from this view — including rescheduling an installment that is stuck retrying.

## Configuration

| Setting | Description |
|---------|-------------|
| Payment plan availability | Controlled by the invoice. Plans are available when partial payments are enabled. |
| Maximum plan duration | Set on the invoice template. Limits how long a plan can extend, measured in months. |
| Minimum installment amount | Set on the invoice template ("minimum amount"). Each plan installment must be at least this amount. Applies only to payment plans, not to one-time custom payments. |
| Allowed frequencies | Weekly, every two weeks, semi-monthly (1st & 15th), and monthly are available for new plans. Bimonthly (every two months) is no longer offered for new plans but continues to run on existing plans. |
| Payment method | The plan uses a single stored payment method selected at setup. Changing it applies to all future installments. |
| Processing fee passthrough | If enabled on the invoice, processing fees are added to each installment at charge time. |
| Email notifications | Plan creation and failure notifications are gated by the invoice template's email notification settings. |

## Edge Cases & Limitations

- There is no distinct "down payment" feature. The first installment is the same amount as all others; only the start date can differ.
- Only one active payment plan can exist per invoice at a time.
- Clients cannot modify their own plans. Only firms can make changes.
- If all retry attempts fail for an installment, manual intervention by the firm may be needed to resolve the outstanding amount.
- Changing the payment method on a plan applies to all future installments, not just the next one.
- Maximum duration enforcement happens only at plan creation. It is not applied retroactively if the template limit changes after a plan is already active.
- When an invoice edit lowers the total, a plan that is now over-scheduled is not trimmed automatically. Review the remaining installments and remove or reduce the surplus yourself.
- Payment plan health is monitored daily. Stalled or misconfigured plans are flagged to operations for review.
- The daily health check remains the backstop for plans whose schedule no longer covers the remaining balance — deleting or editing an installment and refunding a payment are corrected as they happen, but other routes to a short schedule, such as a client pre-paying installments until there are no longer enough upcoming payments to cover what's still due, are caught by the overnight check. New installments are added on the plan's original schedule (the start date plus the chosen interval), never on a date that falls before tomorrow, and never before an existing pre-paid installment that sits further out in the future. Months are honored: a plan whose installment day is the 31st falls back to the 28th in February and to the 30th in April, then returns to the 31st in months that have one, rather than drifting permanently to an earlier day.

## Related Features

- [Invoices](./invoices.md)
- [Online Payments](./online-payments.md)
- [Payment Tracking](./payment-tracking.md)
