# Payment Gates

## Overview

Payment gates let attorneys pause workflow progression at a specific step until the client has reached a payment threshold. When a workflow step includes a payment gate, the client sees a progress indicator in their workflow timeline showing how close they are to the required payment amount. The next steps in the workflow do not proceed until the gate condition is met.

Payment gates are configured by firm staff in the workflow step editor alongside other step attachments such as invoices and document requests.

## Key Behaviors

- A payment gate is added to a workflow step as an attachment. When the step is active, the gate appears in the client's workflow timeline as a card showing a progress ring, the payment threshold, and a link to the associated invoice.
- The progress ring fills proportionally as the client pays toward the threshold:
  - For **minimum amount** gates, the ring reflects the amount paid relative to the required minimum (for example, $150 of a $250 minimum shows roughly 60% filled).
  - For **percentage** gates, the ring reflects the percentage of the total invoice paid relative to the required percentage.
- When the threshold is met, the ring changes to a filled checkmark, signaling that the gate condition is satisfied and the workflow can continue.
- Gates are linked to a specific invoice on the workflow. The client can click **View** on the gate card to open the associated invoice and make a payment.
- Payment gates are visible to both the client and the firm team in the workflow timeline.
- Only one payment gate per attachment chip is supported. A step can have multiple gate attachments if needed.
- If the gate's display condition (set on the attachment) causes the gate to be skipped for a particular client, no gate card appears for that client.

## Configuration

Payment gates are configured in the workflow builder when editing a Send Message step:

1. In the step editor, click **+** in the message compose area and select **Payment Gate**.
2. In the configuration modal, select the invoice to link to the gate.
3. Choose the gate type:
   - **Minimum amount** — specify a dollar amount the client must pay before the gate clears.
   - **Percentage of invoice** — specify what percentage of the total invoice must be paid.
4. Enter the threshold value and click **Save**. A gate chip appears in the message with a shield icon.
5. Click **Update Step** to save the step and persist the gate configuration.

To edit an existing gate, click the gate chip in the step editor — the configuration modal reopens pre-filled with the current settings. Adjust the values and save to update the gate in place.

To remove a gate, delete its chip from the message. The gate configuration is removed when you next save the step.

## Edge Cases & Limitations

- Payment gates require an invoice to be linked. You must select an existing invoice template or workflow invoice when configuring the gate.
- The gate clears automatically when the payment threshold is met — no manual action is required from the firm team.
- Gates are order-based: if a step has multiple gate attachments, their pairing with the underlying gate configurations follows the order they appear in the message.
- Display conditions on the gate attachment control whether the gate appears for a particular client. If the condition is not met, the gate is skipped and does not block the workflow for that client.
- The gate card is read-only for clients — they cannot modify the threshold or the linked invoice from the timeline view.

## Related Features

- [Automation Rules](./automation-rules.md)
- [Invoices](../payments/invoices.md)
- [Triggers](./triggers.md)
