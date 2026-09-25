# Setting Up a Payment Plan

## Overview

A payment plan is set up on an invoice by the client or by the firm on the client's behalf, by choosing an installment amount, frequency, start date, and saved payment method. Invoice templates can limit how long a plan may run and how small each installment may be. This page covers the setup inputs, supported frequencies, duration and minimum-amount limits, and what the client sees while setting up a plan.

## Key Behaviors

### Setup inputs

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

### Maximum plan duration

- Invoice templates can set a maximum payment plan duration, measured in months.
- When a maximum is set, clients cannot create plans that would extend beyond that limit.
- The system calculates total duration based on the number of installments multiplied by the frequency interval.
- If a client's proposed plan exceeds the limit, they see an error asking them to increase the installment amount.
- Firm staff can override this limit when setting up plans on behalf of clients.

### Minimum installment amount

- Invoice templates can set a **minimum amount** for payment plans. When set, each installment in a plan must be at least this amount.
- The minimum is enforced when a plan is set up: a proposed plan whose installment falls below the minimum is rejected, prompting a larger installment (or a shorter schedule).
- This minimum applies **only** to payment plan installments. It does not affect one-time custom payments on the invoice — a client paying a single custom amount can pay below this threshold (see [Invoices](../invoices/README.md)).

### Client experience

- From the invoice payment page, clients can choose to set up a payment plan if partial payments are enabled on the invoice.
- Setup is a two-step process: first configure the plan settings (amount, frequency, start date), then select a payment method.
- The client sees the full installment schedule before confirming.
- Duration warnings appear if the plan approaches or exceeds the maximum duration limit.
- After setup, payments are charged automatically with no further action required from the client.
- When a client's invoice is on an active plan, the client portal home Balance card reflects it: the card shows the installment amount and cadence (for example, "$200.00 monthly") and the next payment date, so a client paying down a balance sees their plan summarized at a glance. Completed or canceled plans are not shown there.

## Configuration

| Setting | Description |
|---------|-------------|
| Payment plan availability | Controlled by the invoice. Plans are available when partial payments are enabled. |
| Maximum plan duration | Set on the invoice template. Limits how long a plan can extend, measured in months. |
| Minimum installment amount | Set on the invoice template ("minimum amount"). Each plan installment must be at least this amount. Applies only to payment plans, not to one-time custom payments. |
| Allowed frequencies | Weekly, every two weeks, semi-monthly (1st & 15th), and monthly are available for new plans. Bimonthly (every two months) is no longer offered for new plans but continues to run on existing plans. |
| Payment method | The plan uses a single stored payment method selected at setup. Changing it applies to all future installments. |

## Edge Cases & Limitations

- There is no distinct "down payment" feature. The first installment is the same amount as all others; only the start date can differ.
- Only one active payment plan can exist per invoice at a time.
- Maximum duration enforcement happens only at plan creation. It is not applied retroactively if the template limit changes after a plan is already active.

## Related Features

- [Payment Plans](./README.md)
- [Installments, Retries, and Fees](./installments-and-retries.md)
- [Managing a Payment Plan](./managing-plans.md)
- [Invoices](../invoices/README.md)
- [Client Portal](../../intake/client-portal/README.md)
