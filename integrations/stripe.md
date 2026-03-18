# Stripe Integration

## Overview

Glade uses Stripe as its primary payment processor for collecting payments from clients on behalf of law firms. Firms connect a Stripe account to accept credit/debit card and ACH payments through Glade-generated payment links and invoices. Glade handles payment processing, fee calculation, refunds, and payouts to the firm's bank account.

## Key Behaviors

### Connecting Stripe

- Firms connect from the Payments settings page in their dashboard.
- Glade supports two connection models:
  - **Express** (default): Glade creates and manages a Stripe Express account on the firm's behalf. The firm completes Stripe's onboarding form (KYC, identity verification, bank details). Payments are processed through Glade's platform account and transferred to the firm.
  - **Connect** (self-managed): The firm connects an existing Stripe account via OAuth. Payments are charged directly on the firm's account.
- Once the account is active and transfers are enabled, the firm can begin accepting payments.
- Each firm can also create secondary Express accounts for separate brands or currencies.

### Payment methods

| Method | Fee | Details |
|--------|-----|---------|
| Credit/debit card | 2.9% + $0.30 (US); +1.5% international | All major networks (Visa, MC, Amex, Discover) |
| ACH bank transfer | 0.8% capped at $10 | Verified via microdeposits (1–2 business days) |

- Firms can choose whether processing fees are passed to the client or absorbed by the firm.
- Payment method setup uses Stripe's SetupIntent flow for ACH verification.

### Payment processing

- When a client pays an invoice or purchases a service, Glade creates a Stripe PaymentIntent with the amount, currency, and fee configuration.
- The client completes payment through a Stripe-hosted form embedded in the Glade payment page.
- On success, Glade records the payment, updates the invoice status, and notifies the firm.
- On failure, the payment is marked as failed and can be retried.

### Subscriptions

- Glade supports recurring billing via Stripe subscriptions.
- Subscriptions can include trial periods, discount codes, and custom payment terms.
- Billing dates and status updates are driven by Stripe webhooks.

### Refunds

- Firms can issue full or partial refunds from the payment detail view.
- Refunds are processed through Stripe and tracked in Glade.
- For Express accounts, refunds also reverse the transfer to the firm.
- Refunded amounts are cumulative — multiple partial refunds are supported.

### Payouts

- Glade batches successful payments into payouts on a configurable schedule (daily, weekly, or monthly).
- Payout amount = total payments minus refunds minus platform fees.
- Only succeeded payments with no pending refunds are included.
- Payout status progresses: pending → in transit → paid (or failed).
- Firms can export payout details as CSV.

### Fee structure

- **Processing fees** (Stripe's fees) are either passed to the client or absorbed by the firm, depending on the firm's configuration.
- **Platform fees** (Glade's margin) are deducted from each payment before transfer to the firm.
- For Express accounts, Glade's application fee includes compensation for Stripe processing costs since those fees come out of Glade's platform account.

### Webhooks

- Glade listens for Stripe webhook events to keep payment state in sync:
  - `payment_intent.succeeded` / `payment_intent.payment_failed` — payment status updates
  - `customer.subscription.updated` — billing date and subscription status changes
  - `customer.updated` — payment method changes trigger retry of failed invoices
  - Refund status events — track refund completion

### Statement descriptors

- Firms can set a custom statement descriptor (up to 22 characters) that appears on client bank statements.

## Configuration

| Setting | Description |
|---------|-------------|
| Stripe connection | Connect or disconnect from Payments settings |
| Account type | Express (Glade-managed) or Connect (self-managed) |
| Processing fee pass-through | Whether Stripe processing fees are charged to the client |
| Payout schedule | Daily, weekly, or monthly batched payouts |
| Statement descriptor | Custom text on client bank/card statements |

## Edge Cases & Limitations

- Express and Connect accounts have different fee structures — Express accounts require Glade to absorb Stripe processing fees within the application fee.
- ACH payments take 1–2 business days for microdeposit verification before the first payment can be processed.
- Refunds are write-once from Stripe's perspective — a refund cannot be reversed once issued.
- Payouts only include payments that have fully succeeded with no pending refunds at the time the payout is created.
- International card payments incur an additional 1.5% fee on top of the standard processing rate.
- Each firm connects one primary Stripe account; secondary accounts can be created for multi-brand scenarios.

## Related Features

- [Invoices](../payments/invoices.md)
- [Online Payments](../payments/online-payments.md)
- [Payment Plans](../payments/payment-plans.md)
- [Payment Tracking](../payments/payment-tracking.md)
- [QuickBooks Integration](./quickbooks.md)
- [Confido Integration](./confido.md)
