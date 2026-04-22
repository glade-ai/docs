# Invoices

## Overview

Invoices are the primary billing tool in Glade. Law firms create invoices to bill clients for legal services, and clients pay those invoices online through Glade's payment system. Invoices can be created manually, generated from reusable templates, or triggered automatically by workflows. Each invoice contains one or more line items, supports multiple payment methods, and moves through a defined lifecycle from creation to payment.

This page covers how invoices work end-to-end — creating them, sending them, collecting payment, and managing them after the fact.

## Key Behaviors

### Creating an invoice

There are three ways to create an invoice:

- **Manually** — A firm user creates an invoice directly by adding line items, setting an amount, and assigning it to a client. The invoice starts in an active state and is immediately payable.
- **From a template** — Firms set up reusable invoice templates with predefined line items, payment settings, and amounts. Creating an invoice from a template copies all settings into a new invoice, saving time for recurring billing scenarios.
- **Via a workflow** — Invoices can be generated automatically as a step in a workflow (for example, after a client submits an intake form or books an appointment). Workflow-generated invoices start in a "generating" state while line items are being finalized, then become active once amounts are set. If a client pays at the start of a workflow before the invoice is formally created, the invoice is correctly marked as paid once it is finalized — it does not remain active as if payment were still outstanding.

### Line items

Every invoice contains one or more line items. Each line item includes:

| Field | Description |
|-------|-------------|
| **Name** | A short label for the charge (e.g., "Consultation fee") |
| **Unit price** | The cost per unit |
| **Quantity** | Number of units |
| **Description** | Optional additional detail about the charge |

The invoice total is calculated as the sum of (unit price x quantity) for each line item.

Line items can be defined on a template and copied automatically when creating an invoice, or added and edited manually on individual invoices.

### Invoice lifecycle

An invoice moves through a series of statuses as it progresses from creation to payment:

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
| **Edited** | The invoice has been replaced by a newer version. This happens when line items change on an invoice that has already been sent. The original is preserved for audit purposes. |

#### Common payment flows

**Single full payment:**
> In Progress → Payment Requested → Final Payment Initiated → Paid

**Partial payments (when enabled):**
> In Progress → Payment Requested → In Progress (partial confirmed) → Payment Requested → Final Payment Initiated → Paid

**Failed payment with retry:**
> In Progress → Payment Requested → Payment Failed → Payment Requested → Final Payment Initiated → Paid

**Payment plan (installments):**
> Same as partial payments, but each installment is charged automatically on a schedule until the full amount is collected.

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

### Invoice PDF

Glade automatically generates a PDF document for each invoice. The PDF includes:

- Firm name, logo, address, phone, and email
- Client billing information
- Itemized line items with descriptions, quantities, unit prices, and line totals
- Invoice total
- Invoice ID and issue date

When payments are recorded, a receipt PDF can also be generated. PDFs are stored as documents attached to the invoice and can be downloaded at any time.

### Notifications

- **Client notification on invoice creation:** When an invoice is created or becomes payable, the client can receive an email with a link to view and pay the invoice.
- **Payment confirmation:** When a payment succeeds, the client receives an email with the amount paid, remaining balance, and payment method used.
- **Firm notification:** Firms can opt in to receive a notification when the first payment is made on an invoice.
- **Payment follow-ups:** Templates can enable automatic payment reminder emails on a configurable schedule (e.g., every 3 days, weekly) for unpaid invoices.
- Email notifications can be enabled or disabled per template.

### Permissions and access

- **Firm users** always have full access to create, view, edit, and manage their invoices.
- **Clients** are automatically granted permission to view and pay their invoices when the invoice is created.
- **Collaborators** — Additional people (such as co-counsel or other team members) can be granted access to view or pay a specific invoice.
- **Workflow participants** — For workflow-generated invoices, the workflow owner and any assigned collaborators automatically receive access.

### Editing and versioning

Invoice changes are handled differently depending on what is being changed:

- **Settings changes** (title, payment configuration, enabled payment methods) can be updated directly on an active invoice without creating a new version.
- **Line item or amount changes** on an invoice that has already been sent or partially paid trigger versioning:
  - The original invoice is marked as "Edited" and becomes read-only.
  - A new invoice is created with the updated line items and amounts.
  - The new invoice references the original, maintaining a complete audit trail.
  - Any credits from payments already made on the original invoice carry forward to the new version.

This approach preserves a clean history of what was billed and what changed, which is important for legal billing compliance and client transparency.

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

### Client-facing experience

When a client receives an invoice:

1. They click a link (from an email or shared URL) to view the invoice on a branded page showing the firm's logo and information.
2. The invoice detail page displays all line items, amounts, payment status, and payment history.
3. On the payment page, the client selects a payment method (credit card, debit card, or ACH — depending on what the firm has enabled) and enters payment information.
4. If partial payments are enabled, the client can choose how much to pay.
5. If payment plans are available, the client can set up an installment schedule.
6. If client modifications are disabled by the firm, the client sees a message explaining that changes are not permitted on this invoice.

### Filtering invoices

The invoice list supports filtering by date range. The date filter is labeled **Created from** / **Created to** and filters by the date the invoice was created, not by due date or payment date.

### Exporting invoice data

Firms can export their full invoice list as a CSV file for use in accounting software, reporting, or reconciliation.

### QuickBooks integration

- Invoices sync to QuickBooks automatically when they become payable.
- Payments also sync to QuickBooks when completed.
- The sync is idempotent — running it multiple times does not create duplicate records in QuickBooks.

### Destination accounts and trust accounting

Glade supports routing payments to different bank accounts, which is important for legal billing compliance:

- **Primary account:** Card payments are routed to the firm's primary Stripe account by default.
- **Secondary account:** A secondary Stripe account can be configured for split-payment scenarios.
- **Trust / IOLTA accounts:** ACH and bank transfer payments can be routed to a dedicated trust or IOLTA (Interest on Lawyers' Trust Accounts) bank account via Confido. This supports the legal industry requirement to keep client funds separate from firm operating funds.

Destination account settings can be configured per invoice or template.

## Configuration

### Invoice templates

Templates are the primary configuration tool for invoices. Each template defines:

| Setting | Description |
|---------|-------------|
| **Title** | Name of the template (e.g., "Standard consultation", "Flat fee — filing") |
| **Line items** | Default charges with descriptions, prices, and quantities |
| **Minimum amount** | Optional floor for the invoice total |
| **Payment methods** | Which methods are enabled: credit card, debit card, ACH |
| **Debit card required** | Whether to force debit card only (lower fees) |
| **Pass processing fees** | Whether to add processing fees as a surcharge to the client |
| **Partial payments** | Whether clients can pay less than the full balance |
| **Max payment plan months** | Maximum duration for installment plans |
| **Client modifications** | Whether clients can request changes to the invoice |
| **Modification message** | Custom message shown when client changes are disabled |
| **Email notifications** | Whether to send payment emails to the client |
| **Follow-up reminders** | Automatic payment reminders with configurable frequency |
| **Destination account** | Which bank account receives the funds |

Templates can be archived when no longer needed. Archiving does not affect invoices already created from the template.

### Per-invoice overrides

All template settings can be overridden on individual invoices. This allows firms to use a template as a starting point and customize specific invoices as needed.

### Workflow integration

When connecting an invoice template to a workflow:

- The template is linked to a specific workflow step.
- Invoices are generated automatically when that step is triggered.
- Auto-assignment rules control who is attached to the invoice (the firm, the client, specific collaborators).
- Conditional logic can determine whether an invoice is generated based on workflow context.

## Edge Cases & Limitations

- **Double-payment prevention:** While a payment is being processed (Payment Requested status), additional payment attempts are blocked. This prevents accidental double-charging but means clients must wait for a failed payment to be confirmed before retrying.
- **Voiding is permanent:** Once an invoice is voided, it cannot be restored. If the firm still needs to bill the client, a new invoice must be created.
- **Edited invoices are read-only:** When an invoice is versioned due to line item changes, the original becomes permanently read-only. All future activity happens on the new version.
- **Payment plan failures:** If a scheduled installment fails and retries are exhausted, the payment plan may need manual intervention from the firm.
- **ACH settlement time:** ACH / bank transfer payments may take several business days to settle, during which the payment shows as pending.
- **Processing fee variability:** The exact surcharge amount when passing processing fees to the client depends on the payment method used and current processor rates. The amount is calculated at the time of payment, not when the invoice is created.
- **QuickBooks sync timing:** Invoice data syncs to QuickBooks when the invoice becomes payable and when payments complete. Changes made directly in QuickBooks are not synced back to Glade.

## Related Features

- [Payment Plans](./payment-plans.md) — Detailed documentation on installment payment configuration and behavior.
- [Online Payments](./online-payments.md) — How Glade processes payments, supported processors, and payment method management.
- [Payment Tracking](./payment-tracking.md) — Viewing payment history, refunds, and financial reporting.
- [Workflows](../workflows/README.md) — How invoices integrate with automated workflows.
