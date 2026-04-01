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
- **Biweekly** — every 14 days
- **Monthly** — every calendar month
- **Bimonthly** — every 2 calendar months

All four frequencies are always available; there is no setting to restrict which frequencies a client can choose.

### How installments work

- Each installment is a scheduled payment for a fixed amount.
- On the scheduled date, Glade automatically charges the client's stored payment method.
- The installment amount is the same for every payment except possibly the final one, which covers only the remaining balance if it is less than the standard installment amount.
- Each installment is tracked individually with its own status:

| Status | Meaning |
|--------|---------|
| Upcoming | Scheduled but not yet charged |
| Paid | Successfully charged |
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

### Modifying a payment plan

- Firms can modify an active payment plan at any time.
- The following changes can be made: installment amount, frequency, payment method, and next payment date.
- Individual installments can also be adjusted (amount or date).
- When a plan is modified, the remaining schedule is recalculated to reflect the new settings.
- Clients cannot modify their own plans. Only firms can make changes.

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

### Firm management experience

- Firms view and manage payment plans from the transactions dashboard.
- Plan details show: status, frequency, installment amount, next payment date, and payment history.
- Firms can modify plan settings, cancel plans, or adjust individual installments from this view.

## Configuration

| Setting | Description |
|---------|-------------|
| Payment plan availability | Controlled by the invoice. Plans are available when partial payments are enabled. |
| Maximum plan duration | Set on the invoice template. Limits how long a plan can extend, measured in months. |
| Allowed frequencies | All four frequencies (weekly, biweekly, monthly, bimonthly) are always available. |
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
- Payment plan health is monitored daily. Stalled or misconfigured plans are flagged to operations for review.

## Related Features

- [Invoices](./invoices.md)
- [Online Payments](./online-payments.md)
- [Payment Tracking](./payment-tracking.md)
