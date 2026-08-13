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

### Invoice note

An invoice can carry an optional **invoice note** — a short, plain-text message shown to the client on the invoice. Firms use it to explain what is due and when, such as how and by when the invoice is expected to be paid.

- The note can be set on an invoice template, so every invoice created from that template starts with the same message.
- When a case is started from a template, the note pre-fills from the template and can be edited before the invoice is sent.
- Staff can add or change the note directly on an existing invoice at any time. Editing the note does not create a new invoice version and does not change the invoice's status — it is separate from making a correction to line items or amounts.
- The note is visible to the client. It appears next to the balance due in the client portal and on each invoice in the case invoice list, which both clients and firm staff can see.

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

The **minimum amount** configured for payment plans does not apply to one-time custom payments. A client paying a single custom amount can pay any amount up to the balance due, even if it is below the payment-plan minimum installment threshold — that minimum only governs payment plan installments (see [Payment Plans](./payment-plans.md)).

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
- **Payment follow-ups:** Templates can enable automatic payment reminder emails (and SMS reminders) on a configurable schedule (e.g., every 3 days, weekly) for unpaid invoices. Reminders are driven by the client's outstanding **Pay Invoice** task, and only continue while the invoice still has a balance to collect — that is, while it is **In Progress** or **Payment Failed**. They stop automatically once the invoice is **Paid**, **Voided**, **Skipped**, or **Edited** (replaced by a newer version), and once an active payment plan takes over collection. This prevents the situation where a client who has already paid — or whose invoice was edited and replaced — keeps receiving reminders on the old, no-longer-payable invoice.
- **Pay Invoice task while a balance is owed:** Because reminders are tied to the Pay Invoice task, a client cannot remove themselves from (or dismiss) that task while the invoice still has an outstanding balance. Attempting to do so is blocked with a message explaining there is still a balance to pay. Once the invoice is paid in full — or voided or skipped — the task can be dismissed normally. This keeps reminders flowing to clients who still owe, so a dismissed task no longer silently strands a client without follow-ups.
- Email notifications can be enabled or disabled per template.

### Permissions and access

- **Firm users** always have full access to create, view, edit, and manage their invoices.
- **Clients** are automatically granted permission to view and pay their invoices when the invoice is created.
- **Collaborators** — Additional people (such as co-counsel or other team members) can be granted access to view or pay a specific invoice.
- **Workflow participants** — For workflow-generated invoices, the workflow owner and any assigned collaborators automatically receive access.

### Editing and versioning

Invoice changes are handled differently depending on what is being changed:

- **Settings changes** (title, payment configuration, enabled payment methods, the invoice note) can be updated directly on an active invoice without creating a new version.
- **Line item or amount changes** on an invoice that has already been sent or partially paid trigger versioning:
  - The original invoice is marked as "Edited" and becomes read-only.
  - A new invoice is created with the updated line items and amounts.
  - The new invoice references the original, maintaining a complete audit trail.
  - Any credits from payments already made on the original invoice carry forward to the new version.
  - If those carried-over payments already cover the new total — for example, when you edit an invoice that was already paid in full, or lower the amount so what the client already paid now covers it — the new version is marked **Paid** right away instead of showing a balance still due for money that was already collected. Anything that depends on the invoice being paid (workflow steps that were waiting on payment, payment-plan completion) advances just as it would after a normal final payment. If a balance still remains after the carried-over payments are applied, the new version stays payable (**In Progress**) for the difference.
  - Payments stay attached to the active invoice version, including ACH / bank-transfer payments. If a bank transfer confirms *after* the invoice has been edited, the confirmation is applied to the new active version rather than stranding the payment on the read-only original — so a paid ACH payment no longer disappears from the invoice when it is edited around the same time the payment settles.

This approach preserves a clean history of what was billed and what changed, which is important for legal billing compliance and client transparency.

Editing a line item keeps its link to any custom-terms variable that references it. Some line items are referenced by name in custom terms documents (for example, a retainer agreement that pulls the attorney-fee amount from the invoice). Editing the invoice's line items no longer clears that link, so the referenced amount continues to render in the agreement instead of showing a "not set" placeholder.

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

### Invoices on a deleted case

When a case is deleted, the invoices that belonged to it are no longer listed anywhere your team bills from.

- Deleting a case does not change its invoices — each one keeps whatever status it held at the moment the case was deleted. Previously those invoices kept listing as live, so a case deleted mid-payment left behind an invoice showing a status like **Payment Requested** and a balance that nobody could pay, with no case to open it from and no way to tell it apart from a real invoice.
- Invoices belonging to a deleted case are now hidden from the firm's Invoices list and its CSV export, the Invoices tab on a client's record, and the client's own invoice list in the portal.
- **Invoices not tied to a case are unaffected.** An invoice raised on its own still lists normally.
- Nothing about the invoice itself is altered — no amounts, statuses, or payment records change. Only what appears in the lists changes.
- Opening an invoice by its direct link still works, so an invoice that needs to be formally voided can still be reached and voided.
- Payments already collected against a hidden invoice stay visible in your payment records. A payment that succeeded before the case was deleted remains on the Payments list for reconciliation, even though its invoice no longer appears in the invoice lists.

This most often shows up when a case is deleted and re-created shortly afterwards — for example, a retainer case set up incorrectly and rebuilt a few minutes later. A payment already in flight moves to the replacement case's invoice, and the original is left behind. The client was only ever billed once, but the account could look as though they owed the amount twice.

### Voided vs. refunded payments on an invoice

When a payment on an invoice is reversed, the invoice shows the reversed amount with a label that reflects what actually happened to it:

- **Refunded** — the payment settled and was later returned to the client.
- **Voided** — the payment was cancelled before it settled, so no money changed hands.

Voided and refunded amounts are labeled distinctly, so a cancelled payment is no longer shown as a refund. This keeps the invoice consistent with the firm's payment records and easier to reconcile.

### Client-facing experience

When a client receives an invoice:

1. They click a link (from an email or shared URL) to view the invoice on a branded page showing the firm's logo and information.
2. The invoice detail page displays all line items, amounts, payment status, and payment history.
3. On the payment page, the client selects a payment method (credit card, debit card, or ACH — depending on what the firm has enabled) and enters payment information.
4. If partial payments are enabled, the client can choose how much to pay.
5. If payment plans are available, the client can set up an installment schedule.
6. If client modifications are disabled by the firm, the client sees a message explaining that changes are not permitted on this invoice.

If the firm has added an invoice note, it appears alongside the balance due so the client sees the payment instructions up front. When a client has more than one unpaid invoice, selecting their balance opens a short picker to choose which invoice to pay; a client with a single unpaid invoice goes straight to that invoice. Invoices that are still **Generating** — those without a final amount assigned yet — are not listed in this picker and are not counted toward the displayed balance, so the client does not see duplicate "$0.00" rows for invoices that are still being prepared.

### Filtering and searching invoices

The invoice list supports date filtering. The date filters are labeled **Created from** and **Created to**, and filter invoices by their creation date. Both filters can be set independently or together to narrow the list to a specific time window.

### Exporting invoice data

Firms can export their full invoice list as a CSV file for use in accounting software, reporting, or reconciliation. The export includes the billed customer's **Email** and **Phone Number** alongside the existing invoice columns, so exported data has the contact details needed for follow-up and reconciliation without a second lookup. The Phone Number column uses the client's contact phone number, falling back to the phone number on their login profile when no contact phone is on file — so the exported number matches the one your team uses to reach the client.

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
| **Invoice note** | Optional customer-visible message shown on the invoice, describing how and when payment is expected |
| **Minimum amount** | Optional minimum installment amount for payment plans. Applies only to payment plan installments — it does not block one-time custom payments below this amount. |
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
- **Invoices on deleted cases are hidden, not voided:** Hiding is based on the case having been deleted, not on whether money was collected. An invoice on a deleted case that had a successful payment against it is hidden along with the rest, so its total no longer appears in the invoice lists or the CSV export. The payment itself stays on the Payments list, so the money is still accounted for — but if you need the invoice back in view, it has to be reached by its direct link.
- **A case's invoice totals can still be off after payments are moved between invoices:** When a payment is re-pointed from one invoice to another and the original case is *not* deleted, the original invoice can keep a stale status and continue to count toward the balance shown on reports. Contact support if a case shows a balance that does not match what the client actually owes.

## Related Features

- [Payment Plans](./payment-plans.md) — Detailed documentation on installment payment configuration and behavior.
- [Online Payments](./online-payments.md) — How Glade processes payments, supported processors, and payment method management.
- [Payment Tracking](./payment-tracking.md) — Viewing payment history, refunds, and financial reporting.
- [Workflows](../workflows/README.md) — How invoices integrate with automated workflows.
