# Confido Integration

## Overview

Glade integrates with Confido, a legal-tech payment platform, as an alternative payment processor for law firms. Confido handles payment collection (ACH, credit card, debit card), trust account management, and firm onboarding with compliance verification. Firms that use Confido can collect invoice payments and store client payment methods through Confido-hosted payment pages.

## Key Behaviors

### Connecting Confido

- When a firm enables Confido, Glade creates a Confido firm account and stores the firm ID and API token.
- The firm completes onboarding through a Confido-hosted sign-up page that handles KYC, identity verification, business license, and tax ID validation.
- Firm status progresses through: Created → Application in Draft → Submitted → In Review → Active.
- Once the firm reaches Active status, payment collection is enabled and the firm receives a confirmation email.
- Firms configure one or more bank accounts in Confido (operating and trust accounts). Each invoice can specify which bank account receives the funds.

### Payment flow

- When a client pays an invoice, Glade creates a Confido payment link with the amount, client details, and destination bank account.
- The client is redirected to a Confido-hosted page where they enter payment details.
- Confido processes the payment and sends a webhook to Glade with the transaction result.
- Glade records the payment and updates the invoice status.

### Payment methods

| Method | Processing fee |
|--------|---------------|
| Credit card | 2.95% |
| Debit card | 2.95% |
| ACH | 1% capped at $30 |

- Firms can choose to pass processing fees to the client or absorb them.
- Additional methods (Zelle, push-to-card, manual) are available depending on the firm's Confido configuration.

### Stored payment methods

- Clients can save a payment method for future use within a firm's account.
- Saved methods allow the firm to charge the client without requiring them to re-enter payment details — used for payment plan installments and retry attempts.

### Refunds and voids

- Firms can issue full or partial refunds through Glade, which are processed via Confido.
- Payments can be voided before they settle.
- Refund and void status updates are received via Confido webhooks.

### Transaction status

- Confido transaction statuses map to Glade payment states:
  - **Pending**: funds in transit, held, or processing (ACH and card payments follow different rules — ACH is only considered succeeded when deposited)
  - **Succeeded**: funds deposited to the firm's bank account
  - **Failed**: charged back, returned, voided, or errored

### Webhooks

- Glade receives Confido webhook events at `/webhooks/confido`:
  - `firm.updated` — firm status changes (triggers activation when status reaches Active)
  - `transaction.created` — new payment received
  - `transaction.ach_returned` — ACH reversal
  - `transaction.refunded` / `transaction.partially_refunded` — refund events
  - `transaction.voided` — payment voided
  - `transaction.deposited` — funds cleared to bank account

## Configuration

| Setting | Description |
|---------|-------------|
| Confido connection | Enabled per firm during onboarding |
| Bank accounts | Operating and trust accounts configured in Confido; each invoice specifies the destination account |
| Fee pass-through | Whether processing fees are charged to the client or absorbed by the firm |

## Edge Cases & Limitations

- Confido payment pages are hosted by Confido, not Glade — the client is redirected to Confido's domain to complete payment.
- ACH payments have stricter success rules than card payments: ACH is only marked as succeeded when funds are deposited, while card payments can succeed while still in transit.
- Webhooks may arrive before the internal payment record is fully persisted; Glade retries the lookup with short delays to handle this race condition.
- Stored payment methods are scoped to a firm — a client's saved method at one firm is not available at another.
- One firm account per Glade account.

## Related Features

- [Invoices](../payments/invoices.md)
- [Online Payments](../payments/online-payments.md)
- [Payment Plans](../payments/payment-plans.md)
- [Payment Tracking](../payments/payment-tracking.md)
- [Stripe Integration](./stripe.md)
