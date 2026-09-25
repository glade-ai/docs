# Invoice Lifecycle

## Overview

An invoice moves through a series of statuses as it progresses from creation to payment. This page covers each status, the common payment flows between them, voiding and skipping an invoice, and how reversed payments are labeled on an invoice.

## Key Behaviors

### Statuses

| Status | Meaning |
|--------|---------|
| **Generating** | The invoice has been created (usually by a workflow) but does not have a final amount yet. Line items are still being set up. |
| **In Progress** | The invoice has an amount set and is ready to accept payment. This is the main active state. Partially paid invoices also return to this status between payments. |
| **Payment Requested** | A payment has been submitted to the payment processor and is awaiting confirmation. While in this state, additional payment attempts are blocked to prevent double-charging. |
| **Final Payment Initiated** | The last payment needed to cover the full invoice amount has been sent to the processor but has not yet been confirmed. |
| **Paid** | The invoice is fully paid. All payments have been confirmed by the processor. |
| **Payment Failed** | The most recent payment attempt was declined (e.g., insufficient funds, expired card). The client can retry with a different payment method. |
| **Voided** | The invoice has been cancelled — typically because the amount needs to change or it was created in error. This is permanent. |
| **Skipped** | Payment collection has been intentionally paused (e.g., fees waived, pro bono). Unlike voiding, skipping is reversible. |
| **Edited** | The invoice has been replaced by a newer version. This happens when line items change on an invoice that has already been sent. The original is preserved for audit purposes. See [Editing and Versioning](./editing-and-versioning.md). |

### Common payment flows

**Single full payment:**
> In Progress → Payment Requested → Final Payment Initiated → Paid

**Partial payments (when enabled):**
> In Progress → Payment Requested → In Progress (partial confirmed) → Payment Requested → Final Payment Initiated → Paid

**Failed payment with retry:**
> In Progress → Payment Requested → Payment Failed → Payment Requested → Final Payment Initiated → Paid

**Payment plan (installments):**
> Same as partial payments, but each installment is charged automatically on a schedule until the full amount is collected.

### Voiding an invoice

- Any active (non-terminal) invoice can be voided by the firm.
- Voiding permanently cancels the invoice and any associated payment plan.
- If the invoice was linked to a workflow, a new empty invoice is automatically created as a replacement so the workflow can continue.
- Voiding is irreversible — once voided, an invoice cannot be reactivated. A new invoice must be created if billing is still needed.

### Skipping an invoice

- Firms can "skip" an invoice to pause payment collection without permanently cancelling it.
- Skipping cancels any active payment plan on the invoice.
- Unlike voiding, skipping is reversible — a skipped invoice can be "unskipped" at any time to resume collection.
- Common use cases: waived fees, pro bono arrangements, payment deferred to a later date.

### Voided vs. refunded payments on an invoice

When a payment on an invoice is reversed, the invoice shows the reversed amount with a label that reflects what actually happened to it:

- **Refunded** — the payment settled and was later returned to the client.
- **Voided** — the payment was cancelled before it settled, so no money changed hands.

Voided and refunded amounts are labeled distinctly, so a cancelled payment is no longer shown as a refund. This keeps the invoice consistent with the firm's payment records and easier to reconcile.

## Edge Cases & Limitations

- **Double-payment prevention:** While a payment is being processed (Payment Requested status), additional payment attempts are blocked. This prevents accidental double-charging but means clients must wait for a failed payment to be confirmed before retrying.
- **Voiding is permanent:** Once an invoice is voided, it cannot be restored. If the firm still needs to bill the client, a new invoice must be created.

## Related Features

- [Invoices](./README.md)
- [Editing and Versioning](./editing-and-versioning.md)
- [Payment Options](./payment-options.md)
- [Payment Tracking](../payment-tracking.md) — refunds and payment history
