# Scheduled One-Time Payments

## Overview

Firm staff can schedule a single payment on an invoice for a later date, charged to a payment method the client has already saved. Use it when a client agrees to pay a set amount on a specific future day, such as their next payday, without setting up a recurring payment plan. Nothing is charged until the chosen date.

> TODO: The invoice-screen controls for scheduling ship in a separate app release. Confirm the on-screen labels once it is live.

## Key Behaviors

### Scheduling a payment

1. Open the invoice and choose **Pay on behalf of client**.
2. Enter the amount, choose the client's saved card or bank account, and pick a payment date.
3. Click **Next**. The summary shows the date the payment is scheduled for and says that nothing is charged today.
4. Confirm. A confirmation names the amount and the date.

- **The date must be after today**, measured in your firm's time zone. You cannot schedule a payment for today.
- **Nothing happens to the invoice until the date.** No payment is recorded and the balance due does not change.
- The payment is a one-time charge. To collect on a repeating schedule, use a [payment plan](../payment-plans/README.md).

### Upcoming payments

- Scheduled payments are listed under the invoice's **Upcoming payments** with the status **Scheduled**, soonest first.
- Anyone who can view the invoice can see them, including the client.
- Staff can cancel a scheduled payment from its row. Once the charge has started, it can no longer be cancelled.
- A scheduled payment cannot be edited. To change the amount, date, or payment method, cancel it and schedule a new one.

### On the payment date

- Glade charges the saved payment method once, around midday in your firm's time zone.
- It charges the scheduled amount or the balance still owed, whichever is lower, so a client who has paid part of the invoice in the meantime is not overcharged.
- A successful charge appears as a payment under **Recent payments**, the balance goes down, and the payment leaves Upcoming payments.
- If the invoice has been paid, voided, or replaced, or nothing is owed, the scheduled payment is cancelled instead of charged.
- If another payment on the invoice is still clearing (for example, an ACH payment that has not settled), the scheduled charge waits until that payment settles. A clearing payment can still fail, so Glade does not reduce or skip the scheduled charge on its account.

### What cancels or moves a scheduled payment

- Voiding the invoice, a successful payment that pays the invoice in full, or archiving or deleting the case cancels the invoice's scheduled payments.
- Editing the invoice so that a new version is created carries scheduled payments over to the new version, the same way a payment plan carries over. See [Editing and Versioning Invoices](./editing-and-versioning.md).

### Payment gates

A [payment gate](../../workflows/payment-gates.md) is not satisfied by a scheduled payment. The case stays at the gate until the scheduled charge succeeds, and stays there if the charge is declined. Staff can still advance the step by hand in the meantime.

## Configuration

| Rule | Detail |
|------|--------|
| Payment method | Must be a card or bank account already saved to the invoice's client. A method belonging to someone else is refused. |
| Partial payments | If the invoice does not allow partial payments, the scheduled amount must be the full balance due. |
| Total scheduled | All upcoming scheduled payments on an invoice together cannot exceed the balance due. |
| Limit | An invoice can hold at most 20 upcoming scheduled payments. |
| Who can schedule or cancel | Firm staff only. Clients can see scheduled payments but cannot create or cancel them. |

## Edge Cases & Limitations

- **A declined charge is not retried.** Glade makes one charge attempt. A decline is recorded as a failed payment under **Recent payments** with the decline reason, and the firm needs to follow up with the client. Only technical errors (not declines) are retried automatically, for up to two days after the payment date.
- **The client is not notified** when a payment is scheduled for them.
- Scheduled payments do not appear in the legacy Glade app.
- A scheduled payment is not counted as paid or pending anywhere until it is charged, so reports and the invoice balance reflect it only from the payment date.

## Related Features

- [Payment Options](./payment-options.md)
- [Invoice Lifecycle](./invoice-lifecycle.md)
- [Editing and Versioning Invoices](./editing-and-versioning.md)
- [Client Experience and Access](./client-experience.md)
- [Payment Plans](../payment-plans/README.md)
- [Payment Gates](../../workflows/payment-gates.md)
