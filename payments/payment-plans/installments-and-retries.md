# Installments, Retries, and Fees

## Overview

Each payment plan is made up of individual installments that Glade charges automatically to the client's stored payment method on their scheduled dates. This page covers how installments are charged and tracked, what happens when a charge fails, how firm staff reschedule an installment stuck retrying, how processing fees apply, and which notifications are sent.

## Key Behaviors

### How installments work

- Each installment is a scheduled payment for a fixed amount.
- On the scheduled date, Glade automatically charges the client's stored payment method.
- The installment amount is the same for every payment except possibly the final one, which covers only the remaining balance if it is less than the standard installment amount.
- Each installment is tracked individually with its own status:

| Status | Meaning |
|--------|---------|
| Upcoming | Scheduled but not yet charged |
| Paid | Successfully charged |
| Deferred | The installment has been postponed. The amount is not collected on the original date and remains outstanding |
| Failed | All charge attempts exhausted without success |
| Retrying | Initial charge failed; automatic retry pending |

### Failed installments and retries

- If a scheduled payment fails (for example, insufficient funds or an expired card), the system automatically retries.
- The system makes up to 3 total attempts: the initial attempt plus 2 retries.
- Retries are scheduled automatically after each failure.
- If all 3 attempts fail, the installment is marked as failed.
- Both the client and the firm are notified by email when retries are exhausted.
- The plan itself remains active. The failed amount rolls into future installments or requires manual intervention by the firm.
- Payment plan charges are processed as off-session payments. If a card requires 3D Secure authentication, the client receives a notification to complete authentication separately — the system does not attempt an automatic 3D Secure challenge during a retry. This prevents spurious authentication prompts for clients whose cards have 3D Secure enabled.
- **Pending payment guard**: If a payment attempt is already in progress when a new charge or retry is due, the system waits for the in-flight attempt to resolve before initiating another. This prevents duplicate charges and eliminates the spurious failure notifications that would otherwise occur when a retry is triggered while a previous attempt is still processing.

### Rescheduling a retrying installment

When an installment is **Retrying** — its initial charge failed and an automatic retry is still pending — firm staff can move it to a new date from the transactions dashboard. Open the installment's actions menu and choose **Edit installment**, then pick a new date.

- The new date must be at least tomorrow in the firm's time zone. If the retry's original date has already passed, the date picker starts on tomorrow instead of the stale past date.
- Saving a new date returns the installment to **Upcoming**, clears the pending retry, and schedules a fresh charge attempt for the date you chose.
- Only the date can be changed from this menu on a retrying installment. The delete option is not offered for retrying rows — it remains available only for upcoming installments dated in the future.
- The charge is scheduled for the exact date you pick; it no longer shifts by a day for firms in certain time zones.

Previously the actions menu appeared only for upcoming installments with a future date. Because a retry's date is always in the past, a stuck retry could not be moved or recovered from the dashboard and required manual intervention on the payment data. Firm staff can now resolve it directly.

### Processing fees on payment plans

- If "pass processing fees to customer" is enabled on the invoice, fees apply to each installment individually.
- Fees are calculated at the time each installment is charged, not upfront.
- The fee amount depends on the payment method used (card fees differ from ACH fees).

### Notifications

- The firm is notified when a payment plan is created, if email notifications are enabled on the invoice template.
- The firm is notified when a plan is modified.
- Both the client and firm are notified when a payment fails after all retry attempts are exhausted.
- Standard payment confirmation emails are sent for each successful installment.

## Configuration

| Setting | Description |
|---------|-------------|
| Processing fee passthrough | If enabled on the invoice, processing fees are added to each installment at charge time. |
| Email notifications | Plan creation and failure notifications are gated by the invoice template's email notification settings. |

## Edge Cases & Limitations

- If all retry attempts fail for an installment, manual intervention by the firm may be needed to resolve the outstanding amount.

## Related Features

- [Payment Plans](./README.md)
- [Setting Up a Payment Plan](./setting-up-a-plan.md)
- [Managing a Payment Plan](./managing-plans.md)
- [Online Payments](../online-payments.md)
