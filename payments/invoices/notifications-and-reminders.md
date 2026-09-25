# Invoice Notifications and Reminders

## Overview

Glade emails clients when an invoice is created or paid, can notify the firm of a first payment, and can send automatic payment reminders while a balance is owed. This page covers each notification, how invoice emails wait on an unsigned retainer, and how reminders relate to the client's Pay Invoice task.

## Key Behaviors

- **Client notification on invoice creation:** When an invoice is created or becomes payable, the client can receive an email with a link to view and pay the invoice.
- **Invoice emails wait for an unsigned retainer:** If the case has a retainer agreement the client has not signed yet, invoice emails are held back rather than sent. This applies to the email sent when an invoice is created, when it becomes payable, and when a collaborator is added to it. Once the client signs the retainer — or the retainer is skipped — the held email is sent, so nothing is lost. This stops clients being asked to pay before they have agreed to representation, which was a common source of confused calls to firms. The invoice itself is created and payable as normal in the meantime; only the email is deferred. Cases with no retainer agreement are unaffected and their invoice emails send immediately. See [Custom Terms](../../workflows/custom-terms.md).
- **Payment confirmation:** When a payment succeeds, the client receives an email with the amount paid, remaining balance, and payment method used.
- **Firm notification:** Firms can opt in to receive a notification when the first payment is made on an invoice.
- **Payment follow-ups:** Templates can enable automatic payment reminder emails (and SMS reminders) on a configurable schedule (e.g., every 3 days, weekly) for unpaid invoices. Reminders are driven by the client's outstanding **Pay Invoice** task, and only continue while the invoice still has a balance to collect — that is, while it is **In Progress** or **Payment Failed**. They stop automatically once the invoice is **Paid**, **Voided**, **Skipped**, or **Edited** (replaced by a newer version), and once an active payment plan takes over collection. This prevents the situation where a client who has already paid — or whose invoice was edited and replaced — keeps receiving reminders on the old, no-longer-payable invoice.
- **Pay Invoice task while a balance is owed:** Because reminders are tied to the Pay Invoice task, a client cannot remove themselves from (or dismiss) that task while the invoice still has an outstanding balance. Attempting to do so is blocked with a message explaining there is still a balance to pay. Once the invoice is paid in full — or voided or skipped — the task can be dismissed normally. This keeps reminders flowing to clients who still owe, so a dismissed task no longer silently strands a client without follow-ups.

## Configuration

- Email notifications can be enabled or disabled per template.
- Follow-up reminders and their frequency are set on the template — see [Invoice Templates](./invoice-templates.md).

## Edge Cases & Limitations

- **Deferred invoice emails cover the invoice email only.** Payment plan reminders and the client's Pay Invoice task are not held back while a retainer is unsigned — only the invoice email itself is deferred.

## Related Features

- [Invoices](./README.md)
- [Invoice Templates](./invoice-templates.md)
- [Invoice Lifecycle](./invoice-lifecycle.md)
- [Custom Terms](../../workflows/custom-terms.md)
