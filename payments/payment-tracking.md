# Payment Tracking

## Overview

Payment tracking in Glade provides firms with a complete view of all payment activity — incoming payments, refunds, and payouts. The Transactions dashboard lets firms search, filter, and export payment data, while automatic notifications and QuickBooks integration keep records synchronized across systems.

## Key Behaviors

### Payment records

- Every payment processed through Glade — or recorded manually — creates a payment record.
- Each record tracks the amount, payment method used (card type and last four digits), status, date, associated invoice, customer, and whether the payment is part of a payment plan.
- Additional data tracked per payment: processing fees, application fees (Glade's fee), refunded amount, net amount, discounts, and tax.
- Notes can be added to any payment for internal reference.

### Payment statuses

| Status | Meaning |
|--------|---------|
| Succeeded | Payment completed successfully. |
| Pending | Payment submitted to the processor, awaiting confirmation. |
| Failed | Payment was declined or encountered an error. |
| Voided | Payment was cancelled before settlement. |
| Requires payment method | Payment initiated but awaiting a payment method. This is uncommon and typically an internal state. |

### Viewing payment history

- Firms access payment history from the Transactions section of the dashboard.
- Payments display in a paginated table showing 20 records per page.
- Each row shows: customer name, amount, date, status, refunded amount, total invoice amount, destination account, description, workflow, and whether the payment is from a payment plan.
- Clicking into any payment opens its full details.

### Searching and filtering

- Filter by status: All, Succeeded, Refunded, Failed, or Voided.
- Filter by date range. The default range is the current month.
- Free-text search works across customer name, invoice ID, workflow name, and payout ID.
- All filters combine. For example, a firm can search for a specific customer's failed payments within a date range.

### Revenue summary

- The Transactions dashboard displays aggregate revenue statistics at the top of the page.
- Metrics include total collected, net revenue (after fees and refunds), and processing fees.
- Statistics update dynamically as filters and date range change.

### Refunds

- Firms can issue refunds on any succeeded payment.
- Both full and partial refunds are supported.
- To issue a refund: select the payment, enter the refund amount, and confirm.
- The refund amount cannot exceed the original payment minus any prior refunds on that payment.
- Only one refund can be pending at a time per payment. A new refund cannot be initiated until the current one completes.
- Refunds are processed through the original payment processor (Stripe or Confido).
- If processing fees were passed to the customer on the original payment, a proportional fee amount is also refunded.
- Refund statuses: Pending (submitted to the processor), Succeeded, or Failed.
- The client receives a notification when the refund completes.
- Payments recorded as outside-of-Glade cannot be refunded through the system — the firm must handle those refunds directly with the client.

### Payouts

- A payout represents a transfer of funds from the payment processor to the firm's bank account.
- Payouts bundle multiple individual payments into a single bank deposit.
- Each payout tracks: amount, gross amount, status, submission date, and expected delivery date.
- Payout statuses: Paid (deposited into the firm's account), Pending (in transit), or Failed.
- Firms view payouts in a separate tab within the Transactions dashboard.
- Each payout can be expanded to see which individual payments it includes.
- Payout data can be exported as a CSV file.

### CSV export

- Firms can export payment data as a CSV file for use in accounting software or reporting.
- The export respects current filters, including date range, status, and search terms.
- CSV columns include: Customer, Amount, Currency, Refunded Amount, Discounts, Glade Fee, Processing Fee, Customer-Paid Fees, Tax, Net, Account, Description, Product Title, Price Title, Notes, Date, Payment Plan (yes/no), and Workflow.
- Payout data can also be exported separately as its own CSV file.

### Email notifications

- A payment confirmation email is sent to the client when a payment succeeds. The email includes the amount, remaining balance, and payment method used.
- Firms can opt in to receive a notification when the first payment is made on an invoice.
- If a payment plan installment fails and all retry attempts are exhausted, both the client and the firm receive a notification.
- Clients receive a notification when a refund completes.

### QuickBooks integration

- Succeeded payments sync to QuickBooks automatically when the firm has the QuickBooks integration enabled.
- Each payment syncs exactly once — duplicate records are not created.
- The synced payment is linked to the corresponding invoice and customer in QuickBooks.
- Sync occurs at the time the payment succeeds.
- The invoice must already be synced to QuickBooks before its payments can sync.
- Changes made directly in QuickBooks are not synced back to Glade. The sync is one-directional.

### Disputes

When a client files a dispute with their card issuer against a payment processed through Stripe, the dispute is surfaced in Glade so your team can track it.

- Disputed payments are flagged in the payment list and the payment detail view.
- Each dispute shows the reason the client provided to their card issuer (e.g., "unrecognized charge", "service not provided") and the current dispute status.
- Dispute statuses reflect the state of the chargeback process: **Warning needs response**, **Warning under review**, **Warning closed**, **Needs response**, **Under review**, **Charge refunded**, **Won**, or **Lost**.
- A dispute does not automatically refund the payment. The outcome depends on the chargeback process with the card issuer.

### Outside-of-Glade payments

- Payments made outside the platform (cash, check, wire, etc.) can be recorded manually on an invoice.
- These payments are recorded as succeeded immediately — no payment processor is involved.
- They appear in payment history alongside processor-handled payments.
- The recorded amount is tracked against the invoice for balance calculation and reconciliation purposes.
- Outside-of-Glade payments cannot be refunded through Glade.

## Configuration

- Payment tracking has no standalone configuration. It reflects the payment activity generated by invoices, payment plans, and payment settings.
- CSV export is available from both the Payments and Payouts tabs on the Transactions dashboard.
- QuickBooks sync is configured at the firm level and requires completing the QuickBooks integration setup.
- Email notification preferences are controlled per invoice template.

## Edge Cases & Limitations

- Only one refund can be pending per payment at a time. The firm must wait for the current refund to complete before initiating another.
- Refunds on outside-of-Glade payments must be handled outside the system.
- QuickBooks sync is one-directional. Changes made in QuickBooks do not flow back to Glade.
- Payout timing depends on the payment processor and the firm's bank. Glade displays the expected delivery date but cannot guarantee exact timing.
- ACH payments may show as pending for several business days before settling.
- Revenue summary statistics reflect only the currently visible filtered data, not all-time totals. Changing the date range or status filter updates the displayed metrics.
- Processing fee refund amounts are calculated proportionally. They may not exactly match the original fee when only a partial refund is issued.
- CSV exports are limited to the current filter criteria. To export all data, clear all filters first.

## Related Features

- [Invoices](./invoices.md)
- [Online Payments](./online-payments.md)
- [Payment Plans](./payment-plans.md)
