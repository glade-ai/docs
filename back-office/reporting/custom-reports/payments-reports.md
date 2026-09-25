# Payments Reports

## Overview

Payments are available as a custom report subject, so your firm can build a saved view over its payment records the same way it does over cases — for example, *payments that failed in the last 7 days on a case with a payment plan*.

## Key Behaviors

Payment reports can be filtered and sorted by:

- **Payment status** — one or several statuses at a time (for example, failed and pending together). This replaces having to pick a single status.
- **On a payment plan** — restrict to payments that are part of a payment plan, or to payments that are not.
- **Invoice** — restrict to the payments made against one invoice.
- **Payment method** — search by payment method to narrow to a particular card or bank account.
- **Date order** — sort oldest-first or newest-first. Paging through a large payment report is stable: payments that share the same timestamp (every charge in one payment-plan run, for example) keep a consistent order instead of some rows repeating on one page and going missing from another.

Choosing several statuses and the older single-status filter at the same time is not allowed — the report asks you to use one or the other. **Refunded** is not a payment status; a refund is recorded as an amount returned on a payment, so it is only available through the single-status filter.

## Configuration

- **Payments report filters**: Payment status (one or more), payment-plan membership, a specific invoice, payment method search, and date sort order. There is no setting that enables these — they are available on any payments report.

## Edge Cases & Limitations

- A payments report cannot combine the multi-select **Payment status** filter with the older single-status filter. Use one or the other.
- **Refunded** is not selectable in the multi-select payment status filter, because a refund is an amount returned on a payment rather than a status the payment sits in.

## Related Features

- [Custom Reports](./README.md)
- [Exporting](./exports.md)
- [Financial Reports](../financial-reports.md)
