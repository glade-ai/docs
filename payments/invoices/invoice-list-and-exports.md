# Invoice List, PDFs, and Exports

## Overview

Your firm's invoices can be browsed and filtered in the invoice list, downloaded as PDFs, exported to CSV, and synced to QuickBooks. This page covers date filtering, how invoices on deleted cases are handled in the lists, invoice and receipt PDFs, the CSV export, and QuickBooks sync.

## Key Behaviors

### Filtering and searching invoices

The invoice list supports date filtering. The date filters are labeled **Created from** and **Created to**, and filter invoices by their creation date. Both filters can be set independently or together to narrow the list to a specific time window.

Both dates are whole calendar days in **your firm's timezone**, and both ends are included. Picking the 1st and the 6th returns everything created from the start of the 1st through the end of the 6th; picking the same date for both returns that one day. Previously the range stopped at the beginning of the day you named rather than the end of it, so the last day selected was always missing and a single-day range came back empty — which read as "nothing was billed that day" rather than as a filtering problem. If your team learned to set the end date a day later than they meant, that adjustment now over-selects by a day and should be dropped.

### Invoices on a deleted case

When a case is deleted, the invoices that belonged to it are no longer listed anywhere your team bills from.

- Deleting a case does not change its invoices — each one keeps whatever status it held at the moment the case was deleted. Previously those invoices kept listing as live, so a case deleted mid-payment left behind an invoice showing a status like **Payment Requested** and a balance that nobody could pay, with no case to open it from and no way to tell it apart from a real invoice.
- Invoices belonging to a deleted case are now hidden from the firm's Invoices list and its CSV export, the Invoices tab on a client's record, and the client's own invoice list in the portal.
- **Invoices not tied to a case are unaffected.** An invoice raised on its own still lists normally.
- Nothing about the invoice itself is altered — no amounts, statuses, or payment records change. Only what appears in the lists changes.
- Opening an invoice by its direct link still works, so an invoice that needs to be formally voided can still be reached and voided.
- Payments already collected against a hidden invoice stay visible in your payment records. A payment that succeeded before the case was deleted remains on the Payments list for reconciliation, even though its invoice no longer appears in the invoice lists.

This most often shows up when a case is deleted and re-created shortly afterwards — for example, a retainer case set up incorrectly and rebuilt a few minutes later. A payment already in flight moves to the replacement case's invoice, and the original is left behind. The client was only ever billed once, but the account could look as though they owed the amount twice.

### Invoice PDF

Glade automatically generates a PDF document for each invoice. The PDF includes:

- Firm name, logo, address, phone, and email
- Client billing information
- Itemized line items with descriptions, quantities, unit prices, and line totals
- Invoice total
- Invoice ID and issue date

When payments are recorded, a receipt PDF can also be generated. PDFs are stored as documents attached to the invoice and can be downloaded at any time.

### Exporting invoice data

Firms can export their full invoice list as a CSV file for use in accounting software, reporting, or reconciliation. The export includes the billed customer's **Email** and **Phone Number** alongside the existing invoice columns, so exported data has the contact details needed for follow-up and reconciliation without a second lookup. The Phone Number column uses the client's contact phone number, falling back to the phone number on their login profile when no contact phone is on file — so the exported number matches the one your team uses to reach the client.

### QuickBooks integration

- Invoices sync to QuickBooks automatically when they become payable.
- Payments also sync to QuickBooks when completed.
- The sync is idempotent — running it multiple times does not create duplicate records in QuickBooks.

## Edge Cases & Limitations

- **Invoices on deleted cases are hidden, not voided:** Hiding is based on the case having been deleted, not on whether money was collected. An invoice on a deleted case that had a successful payment against it is hidden along with the rest, so its total no longer appears in the invoice lists or the CSV export. The payment itself stays on the Payments list, so the money is still accounted for — but if you need the invoice back in view, it has to be reached by its direct link.
- **A case's invoice totals can still be off after payments are moved between invoices:** When a payment is re-pointed from one invoice to another and the original case is *not* deleted, the original invoice can keep a stale status and continue to count toward the balance shown on reports. Contact support if a case shows a balance that does not match what the client actually owes.
- **QuickBooks sync timing:** Invoice data syncs to QuickBooks when the invoice becomes payable and when payments complete. Changes made directly in QuickBooks are not synced back to Glade.

## Related Features

- [Invoices](./README.md)
- [Invoice Lifecycle](./invoice-lifecycle.md) — voiding an invoice
- [Payment Tracking](../payment-tracking.md) — Viewing payment history, refunds, and financial reporting.
- [QuickBooks](../../integrations/quickbooks.md)
