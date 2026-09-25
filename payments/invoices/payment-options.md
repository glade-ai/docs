# Payment Options

## Overview

Each invoice controls how a client can pay it: which payment methods are accepted, whether partial payments or installment plans are allowed, whether processing fees are passed to the client, and which bank account receives the funds. This page covers those payment settings as they apply to invoices.

## Key Behaviors

### Payment methods

Glade supports three payment methods for invoices. Each can be enabled or disabled independently per invoice or template:

| Method | Processor | Notes |
|--------|-----------|-------|
| **Credit card** | Stripe | Standard card payment |
| **Debit card** | Stripe | Firms can optionally require debit-only, which typically carries lower processing fees |
| **ACH / bank transfer** | Confido | Usually the lowest-fee option; funds may take longer to settle |

Firms can also record payments made **outside of Glade** (cash, check, wire transfer, etc.) for tracking and reconciliation purposes. These are logged against the invoice but do not go through a payment processor.

### Partial payments

When partial payments are enabled on an invoice:

- Clients can pay any amount less than the full balance due.
- After a partial payment succeeds, the invoice remains active with the updated remaining balance.
- Clients can make multiple partial payments over time until the full amount is collected.
- The invoice tracks amount paid, amount pending (in-flight), and amount due at all times.

When partial payments are disabled, the client must pay the full balance in a single transaction.

The **minimum amount** configured for payment plans does not apply to one-time custom payments. A client paying a single custom amount can pay any amount up to the balance due, even if it is below the payment-plan minimum installment threshold — that minimum only governs payment plan installments (see [Payment Plans](../payment-plans/README.md)).

### Payment plans

Firms can set up installment-based payment plans on an invoice:

- **Frequencies supported:** weekly, biweekly, monthly, or bimonthly.
- **How it works:** The client enters their payment information once. Glade charges the stored payment method automatically on each scheduled date for the installment amount.
- **Failed installments:** If a scheduled payment fails, the system schedules a retry automatically.
- **Cancellation:** Firms can cancel or modify a payment plan at any time.
- **Completion:** When all installments have been collected and the invoice is fully paid, the invoice moves to the Paid status.
- **Duration limits:** Templates can set a maximum payment plan duration (in months) to cap how long clients can spread payments.

### Processing fees and surcharges

- By default, the firm absorbs all payment processing fees charged by the payment processor.
- Firms can enable **"pass processing fees to customer"** on an invoice or template. When enabled, the processing fee is added as a surcharge to the client's payment amount — the firm receives the full invoice amount and the client pays the invoice total plus the fee.
- The surcharge amount varies depending on the payment method used (card payments typically have higher fees than ACH).

### Destination accounts and trust accounting

Glade supports routing payments to different bank accounts, which is important for legal billing compliance:

- **Primary account:** Card payments are routed to the firm's primary Stripe account by default.
- **Secondary account:** A secondary Stripe account can be configured for split-payment scenarios.
- **Trust / IOLTA accounts:** ACH and bank transfer payments can be routed to a dedicated trust or IOLTA (Interest on Lawyers' Trust Accounts) bank account via Confido. This supports the legal industry requirement to keep client funds separate from firm operating funds.

Destination account settings can be configured per invoice or template.

## Edge Cases & Limitations

- **Payment plan failures:** If a scheduled installment fails and retries are exhausted, the payment plan may need manual intervention from the firm.
- **ACH settlement time:** ACH / bank transfer payments may take several business days to settle, during which the payment shows as pending.
- **Processing fee variability:** The exact surcharge amount when passing processing fees to the client depends on the payment method used and current processor rates. The amount is calculated at the time of payment, not when the invoice is created.

## Related Features

- [Invoices](./README.md)
- [Invoice Templates](./invoice-templates.md)
- [Payment Plans](../payment-plans/README.md) — Detailed documentation on installment payment configuration and behavior.
- [Online Payments](../online-payments.md) — How Glade processes payments, supported processors, and payment method management.
- [Stripe](../../integrations/stripe.md)
- [Confido](../../integrations/confido.md)
