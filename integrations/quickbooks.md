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
| Payments | When a payment succeeds and is linked to a Glade invoice | Payment amount, date, and customer, linked to the corresponding QuickBooks invoice. |

- Sync is one-way: Glade to QuickBooks. Changes made directly in QuickBooks are not reflected in Glade.
- Sync is automatic — once connected, data flows without manual intervention.
- Sync is idempotent — running the same sync multiple times does not create duplicate records in QuickBooks.

### Customer sync

- Customers are matched by email address. If a customer with the same email already exists in QuickBooks, Glade reuses that record rather than creating a new one.
- Customer name and email are synced.
- A customer must have an email address in Glade to sync to QuickBooks.
- **A name QuickBooks already has in use no longer costs you the payment.** QuickBooks requires a unique name across all of its customers, vendors, and employees, so a client whose name already appears there — often a namesake with a different email address, or no email at all — could not be created. Two things now happen instead of the sync giving up:
  - If the record already in QuickBooks has the **same email address** as the Glade client, Glade links to that record rather than trying to create a second one. Inactive records are checked too, so a client archived in QuickBooks is reused rather than duplicated.
  - If the email is different, Glade creates the client under a distinguishing name — their name followed by their email address — so a genuinely different person with the same name still reaches your books.
- Previously a name collision stopped the whole payment sync for that client and the payment was never pushed to QuickBooks. There was nothing on screen to say so, and firms lost a handful of payments a month this way, typically noticing only at reconciliation. **Payments missed before this was corrected are not synced retroactively** — enter them in QuickBooks by hand. Use the [QuickBooks Ledger report](#quickbooks-ledger-report) to identify which Glade payments have no QuickBooks record.
- When **Invoice sync timing** is set to "On First Payment", customers are not pushed to QuickBooks when they are created or updated in Glade. Instead, the customer record is created in QuickBooks only when their first payment is processed. This ensures customers appear in QuickBooks at the same time as their first invoice and payment, keeping the books clean for firms that use cash-basis accounting. If a customer already has a payment recorded in QuickBooks (their first payment has been processed), subsequent updates to their name, email, or phone in Glade still sync immediately.

### Invoice sync

- Invoices sync with their full amount, line items, and date.
- Line items are recorded against a configurable QuickBooks service item. By default, QuickBooks auto-selects the item; firms can set a specific item in the QuickBooks settings (see Configuration).
- A private memo on the QuickBooks invoice includes the Glade invoice ID for cross-reference.
- The QuickBooks invoice due date is set to the Glade invoice's creation date, so synced invoices show as due immediately rather than relying on QuickBooks' default customer terms. If a synced invoice is later out of date in QuickBooks, the next sync also updates its due date to match.
- **The invoice date is set explicitly rather than left to QuickBooks.** Glade sends both the transaction date and the due date on every synced invoice. Previously the transaction date was omitted, so QuickBooks stamped the invoice with the day the sync happened to run — which is normally the same day, but is the wrong day for an invoice that syncs after a delay or a retry.
- If an invoice is voided in Glade, the corresponding QuickBooks invoice is also marked as voided.
- Edited invoices (new versions) sync as updates to the existing QuickBooks invoice.

### Payment sync

- Only succeeded payments sync to QuickBooks. Failed or pending payments are not sent.
- Payments only sync to QuickBooks when they are linked to a Glade invoice. Payments without an associated invoice are not pushed to QuickBooks.
- Payments are written once — they are not updated after initial creation in QuickBooks.
- When a payment syncs, the QuickBooks payment references the linked invoice, so QuickBooks shows the invoice as partially or fully paid.
- When a firm makes a payment on behalf of a client, the payment syncs under the invoice's primary client in QuickBooks — not under the person who submitted the payment. This keeps your QuickBooks customer records accurate for on-behalf-of payment flows.
- When a QuickBooks sync fails after automatic retries are exhausted, Glade notifies the workflow's assigned team members via the case chat so they can follow up without leaving Glade.

### Invoice sync timing options

Firms choose when invoices sync to QuickBooks:

| Option | Behavior |
|--------|----------|
| Never | Invoices do not sync. Only customers and payments sync. |
| On invoice payable (default) | Invoices sync as soon as they have line items and are ready to accept payment. Customers are pushed to QuickBooks when created or updated in Glade. |
| On first payment | Invoices sync when the first payment succeeds. Customers are also created in QuickBooks at first payment time rather than when first added in Glade. Useful for firms that only want paid records in their books. |

### Sync status dashboard

- The QuickBooks settings page shows: connection status, connected company name, and counts of synced customers, invoices, and payments.
- Last sync timestamp is displayed.

### QuickBooks Ledger report

A **QuickBooks Ledger** report is available from the QuickBooks integration row in your firm's dashboard. The report lists every payment that has been synced to QuickBooks, giving your bookkeeper a side-by-side view of what's in Glade and what's been pushed to QuickBooks — useful when reconciling the two systems at month-end or when investigating a specific transaction.

Each row shows the payment, the client and case it belongs to, the linked invoice, the payment date and amount, the provider that processed the payment, and the matching QuickBooks payment and invoice references.

The report supports:

- **Search** across payment, invoice, client, and case identifiers — paste an ID from either Glade or QuickBooks and the matching row appears.
- **Status filter** to limit the report to specific payment statuses (for example, succeeded versus refunded).
- **Provider filter** to narrow the report to a specific payment provider.
- **Date range** filter on the payment date.
- **Pagination** for firms with high payment volume.

If the report fails to load, a toast appears so you know the load did not complete — refresh to retry.

### What date a record carries in QuickBooks

Every date Glade writes to QuickBooks is the **Eastern Time** calendar day, not the UTC day.

- A payment carries the Eastern-time day it succeeded on. A payment taken at 11:45pm Eastern on the last day of a month stays on that day and in that month, where it previously landed on the first of the next month.
- Invoices carry their own date the same way.
- This matters most at month-end close: a late-evening transaction on the 31st used to fall into the following month's books, so the two months' totals in QuickBooks did not match what Glade reported for the same periods.
- **Records already in QuickBooks are not corrected.** If your firm reconciled a month-end close before this change, check for late-evening transactions sitting on the first of the following month and re-date them in QuickBooks.

### Invoice line item rounding

Invoice line item amounts are rounded to the nearest cent before being sent to QuickBooks. A line item priced at $19.99 with a quantity of 3, for example, syncs as $59.97 — the calculated amount and the unit price are each rounded to two decimal places, so the QuickBooks invoice total always matches what Glade shows your firm and your client. This prevents penny-level mismatches between Glade and QuickBooks caused by floating-point arithmetic.

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
- If an automatic token refresh fails (for example, because the authorization was revoked in QuickBooks), the connection status immediately updates to show as disconnected. The Integrations page reflects the true connection state — a disconnected connection is never shown as active after token failure.

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
- Customers are matched by email only — if the same person has different emails in Glade and QuickBooks, a duplicate may be created. Where the name is also already in use, that duplicate carries the client's email address in its display name, which is what allows it to exist alongside the original. Merging the two records is done in QuickBooks.
- Payments are written once to QuickBooks and never updated afterward — refunds create separate records.
- Line items sync against the configured service item; if that item is later deleted in QuickBooks, Glade automatically clears the stale setting and falls back to QuickBooks' default item on the next sync.
- Customer address and phone number do not sync — only name and email.
- If the refresh token expires (after approximately 100 days without activity), the firm must manually reconnect.
- Reconnecting to the same QuickBooks company after disconnecting may create duplicate records (previously synced records are not re-matched).
- No estimates, quotes, or credit memo sync — only invoices and payments.
- Dates written to QuickBooks before the Eastern Time correction are not re-dated retroactively. Late-evening transactions from those periods may sit on the following calendar day in your books.

## Related Features

- [Invoices](../payments/invoices.md)
- [Online Payments](../payments/online-payments.md)
- [Payment Tracking](../payments/payment-tracking.md)
- [Glade MCP Server](./glade-mcp.md)
