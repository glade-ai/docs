# Client Experience and Access

## Overview

Clients view and pay invoices on a branded page reached from an email or shared link. This page covers who has access to an invoice and what the client sees when viewing and paying it.

## Key Behaviors

### Permissions and access

- **Firm users** always have full access to create, view, edit, and manage their invoices.
- **Clients** are automatically granted permission to view and pay their invoices when the invoice is created.
- **Collaborators** — Additional people (such as co-counsel or other team members) can be granted access to view or pay a specific invoice.
- **Workflow participants** — For workflow-generated invoices, the workflow owner and any assigned collaborators automatically receive access.

### Viewing and paying an invoice

When a client receives an invoice:

1. They click a link (from an email or shared URL) to view the invoice on a branded page showing the firm's logo and information.
2. The invoice detail page displays all line items, amounts, payment status, and payment history.
3. On the payment page, the client selects a payment method (credit card, debit card, or ACH — depending on what the firm has enabled) and enters payment information.
4. If partial payments are enabled, the client can choose how much to pay.
5. If payment plans are available, the client can set up an installment schedule.
6. If client modifications are disabled by the firm, the client sees a message explaining that changes are not permitted on this invoice.

If the firm has added an invoice note, it appears alongside the balance due so the client sees the payment instructions up front. When a client has more than one unpaid invoice, selecting their balance opens a short picker to choose which invoice to pay; a client with a single unpaid invoice goes straight to that invoice. Invoices that are still **Generating** — those without a final amount assigned yet — are not listed in this picker and are not counted toward the displayed balance, so the client does not see duplicate "$0.00" rows for invoices that are still being prepared.

## Edge Cases & Limitations

- Invoices still in the **Generating** state are excluded from the client's invoice picker and displayed balance.

## Related Features

- [Invoices](./README.md)
- [Payment Options](./payment-options.md)
- [Creating Invoices](./creating-invoices.md) — the invoice note
- [Client Portal](../../intake/client-portal/README.md)
