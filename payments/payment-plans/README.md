# Payment Plans

## Overview

Payment plans allow clients to pay invoices in scheduled installments rather than a single lump sum. Firms configure the available options, and clients (or firms on their behalf) set up a plan by choosing an installment amount, frequency, and start date. Glade automatically charges the client's stored payment method on each scheduled date until the invoice is fully paid.

## Topics

- [Setting Up a Payment Plan](./setting-up-a-plan.md) — setup inputs, supported frequencies, maximum duration and minimum installment limits, and the client's setup experience.
- [Installments, Retries, and Fees](./installments-and-retries.md) — how installments are charged and tracked, failed-charge retries, rescheduling a retrying installment, processing fees, and notifications.
- [Managing a Payment Plan](./managing-plans.md) — plan lifecycle, modifying and canceling plans, what happens when the invoice is edited, external payments, and schedule health checks.
- [Exporting Payment Plans](./exporting-payment-plans.md) — downloading the Payment Plans section of the transactions dashboard as a spreadsheet.

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

- Only one active payment plan can exist per invoice at a time.
- Clients cannot modify their own plans. Only firms can make changes.

## Related Features

- [Invoices](../invoices/README.md)
- [Online Payments](../online-payments.md)
- [Payment Tracking](../payment-tracking.md)
