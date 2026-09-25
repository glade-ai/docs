# Invoice Templates

## Overview

Templates are the primary configuration tool for invoices. A template holds default line items, payment settings, notifications, and destination account settings, and every invoice created from it starts with those settings. This page covers what a template defines, archiving and creating templates, and overriding template settings on individual invoices.

## Key Behaviors

- Creating an invoice from a template copies all settings into a new invoice, saving time for recurring billing scenarios.
- Templates can be archived when no longer needed. Archiving does not affect invoices already created from the template.
- **Creating a template.** Saving a new template from the **New invoice template** dialog completes, and the template appears in your list ready to use. Previously the dialog refused the save and showed an error in place of creating the template, so a firm that needed a second template — a separate filing-fee template for court costs, for example — had no way to add one. Existing templates were never affected. If your team gave up on adding a template, try again.

## Configuration

### Template settings

Each template defines:

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

### Per-invoice overrides

All template settings can be overridden on individual invoices. This allows firms to use a template as a starting point and customize specific invoices as needed.

## Edge Cases & Limitations

- Archiving a template does not affect invoices already created from it.
- The minimum amount applies only to payment plan installments, not to one-time custom payments.

## Related Features

- [Invoices](./README.md)
- [Creating Invoices](./creating-invoices.md) — including connecting a template to a workflow
- [Payment Options](./payment-options.md)
- [Notifications and Reminders](./notifications-and-reminders.md)
