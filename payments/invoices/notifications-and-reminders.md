# Invoice Notifications and Reminders

## Overview

Glade emails clients when an invoice is created or paid, can email the case's owners whenever a payment comes in, and can send automatic payment reminders while a balance is owed. This page covers each notification, how invoice emails wait on an unsigned retainer, and how reminders relate to the client's Pay Invoice task.

## Key Behaviors

- **Client notification on invoice creation:** When an invoice is created or becomes payable, the client can receive an email with a link to view and pay the invoice.
- **Invoice emails wait for an unsigned retainer:** If the case has a retainer agreement the client has not signed yet, invoice emails are held back rather than sent. This applies to the email sent when an invoice is created, when it becomes payable, and when a collaborator is added to it. Once the client signs the retainer — or the retainer is skipped — the held email is sent, so nothing is lost. This stops clients being asked to pay before they have agreed to representation, which was a common source of confused calls to firms. The invoice itself is created and payable as normal in the meantime; only the email is deferred. Cases with no retainer agreement are unaffected and their invoice emails send immediately. See [Custom Terms](../../workflows/custom-terms.md).
- **Payment confirmation:** When a payment succeeds, the client receives an email with the amount paid, remaining balance, and payment method used.
- **Team notification on every payment:** When an invoice's **Email my team on payment activity** setting is on, the case's owners receive an email for every payment on that invoice. This covers card and ACH payments, payment plan installments, and payments recorded as made outside of Glade. Each payment before the last one sends a payment email with the receipt attached, showing the client, invoice, payment method, amount and remaining balance. The final payment sends the paid-in-full email instead, which shows the invoice title and total. Previously the team was emailed only on the first payment and the final payment, and payments in between were not reported.
- **Payment follow-ups:** Templates can enable automatic payment reminder emails (and SMS reminders) on a configurable schedule (e.g., every 3 days, weekly) for unpaid invoices. Reminders are driven by the client's outstanding **Pay Invoice** task, and only continue while the invoice still has a balance to collect — that is, while it is **In Progress** or **Payment Failed**. They stop automatically once the invoice is **Paid**, **Voided**, **Skipped**, or **Edited** (replaced by a newer version), and once an active payment plan takes over collection. This prevents the situation where a client who has already paid — or whose invoice was edited and replaced — keeps receiving reminders on the old, no-longer-payable invoice.
- **Pay Invoice task while a balance is owed:** Because reminders are tied to the Pay Invoice task, a client cannot remove themselves from (or dismiss) that task while the invoice still has an outstanding balance. Attempting to do so is blocked with a message explaining there is still a balance to pay. Once the invoice is paid in full — or voided or skipped — the task can be dismissed normally. This keeps reminders flowing to clients who still owe, so a dismissed task no longer silently strands a client without follow-ups.

## Configuration

- Email notifications can be enabled or disabled per template.
- **Email my team on payment activity** is set on the invoice template and alone decides whether the case's owners are emailed about payments. The workflow's **Email on first payment** setting no longer affects payment emails.
- Follow-up reminders and their frequency are set on the template — see [Invoice Templates](./invoice-templates.md).

## Edge Cases & Limitations

- **Team payment emails need a case.** They go to the case's owners, so an invoice that isn't on a case sends no team email.
- **Deferred invoice emails cover the invoice email only.** Payment plan reminders and the client's Pay Invoice task are not held back while a retainer is unsigned — only the invoice email itself is deferred.

## Related Features

- [Invoices](./README.md)
- [Invoice Templates](./invoice-templates.md)
- [Invoice Lifecycle](./invoice-lifecycle.md)
- [Custom Terms](../../workflows/custom-terms.md)
