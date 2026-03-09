# Online Payments

## Overview

Online payments allow clients to pay invoices directly through Glade. Glade integrates with two payment processors — Stripe (for card payments) and Confido (for ACH/bank transfers and card payments) — to securely handle transactions. Firms configure which payment methods to accept, and clients choose from the available options when viewing an invoice. Payments are tracked automatically, and firms can issue refunds or record payments made outside the platform.

## Key Behaviors

### Payment processors

- Glade supports two payment processors: **Stripe** and **Confido**.
- Stripe handles card payments through Stripe Connect, where each firm has its own connected account.
- Confido handles ACH (bank transfer) payments and can also process credit and debit card payments.
- The processor used for a given payment depends on the firm's configuration and the payment method the client selects.

### Supported payment methods

- **Credit card** — processed through Confido or Stripe, depending on firm configuration.
- **Debit card** — processed through Confido or Stripe. Firms can enable a debit-only mode that restricts clients to debit cards, which carry lower processing fees.
- **ACH / bank transfer** — processed through Confido. Typically the lowest-cost option for firms, but settlement takes several business days.
- **Outside-of-Glade payments** — cash, check, wire transfer, or any other method handled outside the platform. These are recorded manually against the invoice for tracking purposes and are not processed through Glade.

### Payment flow (client experience)

1. The client receives an invoice link via email or a shared URL.
2. The client opens the link and views the invoice on a branded payment page displaying the firm's logo.
3. Available payment methods appear based on what the firm has enabled for that invoice.
4. The client selects a payment method and enters the required details (card information or bank account).
5. If the firm allows partial payments, the client can choose how much to pay.
6. If the firm passes processing fees to the client, the fee amount appears before the client confirms. The displayed fee updates dynamically as the client switches between payment methods.
7. The client submits the payment.
8. While the payment is processing, additional payment attempts on the same invoice are blocked to prevent double-charging.
9. On success, a confirmation screen appears and the client receives an email receipt.
10. On failure, an error screen appears with the option to retry or contact the firm for help.

### Stored payment methods

- Clients can save payment methods for future use, so they do not need to re-enter details each time.
- For Stripe, card details are stored securely through Stripe's card vault.
- For Confido, payment tokens are stored for reuse on future payments.
- When a client pays a new invoice, any saved payment methods appear as selectable options alongside the option to enter new details.
- Clients can add or remove saved payment methods from their profile.

### Processing fees and surcharges

- By default, the firm absorbs all processing fees.
- Firms can enable a "pass processing fees to customer" setting, configurable per invoice or invoice template.
- When this setting is enabled, the fee is calculated at the time of payment based on the method the client selects:
  - **ACH fees:** approximately 1%, capped at $30.
  - **Card fees:** approximately 2.95%.
- The fee amount is displayed to the client before they confirm the payment.
- Because fees vary by payment method, the displayed amount updates as the client switches between methods.

### Destination accounts and trust accounting

- Payments can be routed to different bank accounts depending on the firm's setup and the nature of the funds.
- **Primary account:** the default destination for payments processed through Stripe.
- **Secondary account:** available for firms that need to split payments across multiple accounts.
- **Trust / IOLTA accounts:** ACH payments processed through Confido can be directed to a dedicated trust account. This is important for legal compliance, as client funds must be kept separate from the firm's operating funds.
- The destination account is configured per invoice or invoice template.

### Payment confirmation and status updates

- Payment processors notify Glade when a payment succeeds, fails, or is disputed.
- Glade updates the payment status automatically based on these notifications — no manual intervention is needed for standard confirmations.
- If a payment fails, the invoice status reflects the failure and the client can retry.

### Refunds

- Firms can issue full or partial refunds on completed payments.
- Refunds are processed through the same payment processor that handled the original payment.
- Only one refund can be pending at a time per payment. A new refund cannot be initiated until the previous one completes.
- The refund amount cannot exceed the original payment amount minus any prior refunds already issued.
- If processing fees were passed to the client on the original payment, a proportional share of the fee is also refunded.
- Refund status is tracked as pending, succeeded, or failed.
- Both the client and the firm are notified when the refund completes.

### Recording outside payments

- Firms can record payments that were made outside of Glade — for example, cash, check, or wire transfer.
- These entries are logged against the invoice so the firm has a complete payment history in one place.
- Outside payments are marked as succeeded immediately, since no processor is involved.
- Outside payments cannot be refunded through Glade. Any refund for an outside payment must be handled directly between the firm and the client.

## Configuration

- **Payment methods** — credit card, debit card, and ACH can each be enabled or disabled per invoice or invoice template.
- **Debit-only mode** — when enabled, only debit cards are accepted. Credit cards are not available as a payment option. This reduces processing fees for the firm.
- **Pass processing fees to customer** — a toggle that shifts the processing fee from the firm to the client. Configurable per invoice or invoice template.
- **Destination account** — determines which bank account receives the funds. Options include the primary account, a secondary account, or a trust/IOLTA account. Configurable per invoice or invoice template.
- All payment settings can be defined on an invoice template and inherited by invoices created from that template. Individual invoices can override any inherited setting.

## Edge Cases & Limitations

- **Double-payment prevention:** while a payment is actively processing, the system blocks additional payment attempts on the same invoice to prevent duplicate charges.
- **ACH settlement time:** ACH payments take several business days to settle. The payment appears as processing until the bank transfer completes.
- **Fee calculation timing:** processing fee amounts are calculated at the time of payment, not when the invoice is created. If fee rates change between invoice creation and payment, the client sees the current rate.
- **One pending refund at a time:** only one refund can be in progress per payment. The firm must wait for a pending refund to resolve before initiating another.
- **Outside payments are not refundable in Glade:** payments recorded as outside-of-Glade have no associated processor transaction, so Glade cannot process a refund for them.
- **Debit-only restriction:** when debit-only mode is enabled, clients cannot pay with a credit card even if they have one saved. Only debit cards and ACH (if enabled) are available.
- **International cards:** payments from international cards may be subject to different fee rates depending on the processor.

## Related Features

- [Invoices](./invoices.md)
- [Payment Plans](./payment-plans.md)
- [Payment Tracking](./payment-tracking.md)
