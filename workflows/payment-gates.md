# Payment Gates

## Overview

A payment gate is a requirement you attach to a workflow step that blocks the step from completing until a client has paid a specified amount toward an invoice. Attorneys use payment gates to ensure a minimum payment is received before work on a particular phase begins — for example, requiring a retainer deposit before document preparation starts.

## Key Behaviors

- Payment gates are added from the `+` attachment menu inside a **Send Message** step in the workflow template editor, alongside invoices, questionnaires, document requests, and other attachments.
- Clicking **Payment Gate** in the menu opens a modal where you choose an invoice, select a gate type, and enter a threshold value.
- Once saved, the payment gate appears as a chip with a shield icon in the step's message composition area.
- Each payment gate is tied to a specific invoice. The gate tracks how much the client has paid toward that invoice and compares it to your configured threshold.
- To remove a payment gate, click the `×` on the chip. Removing the chip also removes the gate configuration when you save the step.
- Click **Update Step** to save the payment gate configuration alongside the rest of the step.

## Configuration

| Setting | Description |
|---------|-------------|
| **Invoice** | The invoice the gate monitors. The client's payment toward this invoice is tracked against the threshold. |
| **Gate type** | **Minimum amount** — a fixed dollar amount the client must have paid. **Percentage** — a percentage of the total invoice the client must have paid. |
| **Threshold** | The dollar amount (minimum amount gates) or percentage (percentage gates) required to clear the gate. |

## Edge Cases & Limitations

- Editing an existing payment gate chip is not yet supported. To change a gate's settings, remove the chip and add a new one.
- A payment gate controls when the step completes, not whether the message is visible. If you also configure a display condition on the payment gate chip, the condition controls the chip's visibility in the message independently of the gate's enforcement.
- Only one payment gate can be configured per message step at a time.

## Related Features

- [Automation Rules](./automation-rules.md)
- [Invoices](../payments/invoices.md)
- [Online Payments](../payments/online-payments.md)
