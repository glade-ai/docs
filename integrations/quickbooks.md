# QuickBooks Integration

## Overview

Glade integrates with QuickBooks Online to automatically sync customer, invoice, and payment data from Glade into a firm's QuickBooks account. The sync is one-way — Glade is the source of truth, and data flows from Glade to QuickBooks. Firms connect their QuickBooks account through a standard authorization flow and can configure when invoices sync.

## Key Behaviors

### Connecting QuickBooks

- Firms connect from the Integrations page in their dashboard settings.
- Clicking "Connect QuickBooks" redirects to QuickBooks' authorization page.
- After granting access, the firm is redirected back to Glade with the connection active.
- The connected QuickBooks company name is displayed in settings.
- Each Glade account can connect to one QuickBooks company at a time.

### What syncs

| Data | When it syncs | Details |
|------|---------------|---------|
| Customers | When a customer is created or updated in Glade | Matched by email — if a QuickBooks customer with the same email exists, Glade links to them instead of creating a duplicate |
| Invoices | Configurable (see Configuration) | Invoice amount, line items, date, and a reference back to the Glade invoice ID |
| Payments | When a payment succeeds | Payment amount, date, and customer. Linked to the QuickBooks invoice when available. |

- Sync is one-way: Glade to QuickBooks. Changes made directly in QuickBooks are not reflected in Glade.
- Sync is automatic — once connected, data flows without manual intervention.
- Sync is idempotent — running the same sync multiple times does not create duplicate records in QuickBooks.

### Customer sync

- Customers are matched by email address. If a customer with the same email already exists in QuickBooks, Glade reuses that record rather than creating a new one.
- Customer name and email are synced.
- A customer must have an email address in Glade to sync to QuickBooks.

### Invoice sync

- Invoices sync with their full amount, line items, and date.
- Line items are recorded against a configurable QuickBooks service item. By default, QuickBooks auto-selects the item; firms can set a specific item in the QuickBooks settings (see Configuration).
- A private memo on the QuickBooks invoice includes the Glade invoice ID for cross-reference.
- If an invoice is voided in Glade, the corresponding QuickBooks invoice is also marked as voided.
- Edited invoices (new versions) sync as updates to the existing QuickBooks invoice.

### Payment sync

- Only succeeded payments sync to QuickBooks. Failed or pending payments are not sent.
- Payments are written once — they are not updated after initial creation in QuickBooks.
- When a payment is linked to an invoice that has already been synced, the QuickBooks payment references that invoice, so QuickBooks shows the invoice as partially or fully paid.
- If the associated invoice has not been synced to QuickBooks yet, the payment is recorded as an unapplied payment.

### Invoice sync timing options

Firms choose when invoices sync to QuickBooks:

| Option | Behavior |
|--------|----------|
| Never | Invoices do not sync. Only customers and payments sync. |
| On invoice payable (default) | Invoices sync as soon as they have line items and are ready to accept payment. |
| On first payment | Invoices sync when the first payment succeeds. Useful for firms that only want paid invoices in their books. |

### Sync status dashboard

- The QuickBooks settings page shows: connection status, connected company name, and counts of synced customers, invoices, and payments.
- Last sync timestamp is displayed.

### Disconnecting

- Firms can disconnect QuickBooks at any time from the settings page.
- Disconnecting revokes the authorization and stops all future syncing.
- Data already synced to QuickBooks remains there — disconnecting does not delete records from QuickBooks.
- Previously synced records in Glade retain their QuickBooks references but no longer update.

### Token management

- The QuickBooks connection uses OAuth tokens that refresh automatically in the background.
- Access tokens refresh every hour; refresh tokens are valid for approximately 100 days.
- If the refresh token expires (e.g., if the firm has not used Glade in over 100 days), the firm must reconnect QuickBooks.
- Glade proactively refreshes tokens on a weekly basis to prevent expiration.

## Configuration

| Setting | Description |
|---------|-------------|
| QuickBooks connection | Connect or disconnect from the Integrations settings page |
| Invoice sync timing | Choose when invoices sync: Never, On Invoice Payable (default), or On First Payment |
| Service item | Choose which QuickBooks service item invoice line items are recorded against. The dropdown is populated from your QuickBooks account. Leave unset to use QuickBooks' default auto-selection. The two settings operate independently — changing one does not affect the other. |
| Connected company | Displayed in settings after connection — one QuickBooks company per Glade account |

## Edge Cases & Limitations

- One-way sync only — changes made in QuickBooks (editing an invoice, adding a payment) do not flow back to Glade.
- One QuickBooks company per Glade account — connecting a different company requires disconnecting first.
- Customers without an email address in Glade cannot sync to QuickBooks.
- Customers are matched by email only — if the same person has different emails in Glade and QuickBooks, a duplicate may be created.
- Payments are written once to QuickBooks and never updated afterward — refunds create separate records.
- Line items sync against the configured service item; if that item is later deleted in QuickBooks, Glade automatically clears the stale setting and falls back to QuickBooks' default item on the next sync.
- Customer address and phone number do not sync — only name and email.
- If the refresh token expires (after approximately 100 days without activity), the firm must manually reconnect.
- Reconnecting to the same QuickBooks company after disconnecting may create duplicate records (previously synced records are not re-matched).
- No estimates, quotes, or credit memo sync — only invoices and payments.

## Related Features

- [Invoices](../payments/invoices.md)
- [Online Payments](../payments/online-payments.md)
- [Payment Tracking](../payments/payment-tracking.md)
- [Glade MCP Server](./glade-mcp.md)
