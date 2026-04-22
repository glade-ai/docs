# Payment Gates

## Overview

Payment gates let you require clients to complete a payment before they can proceed past a specific step in a workflow. When you add a payment gate to a message step, the client sees the linked invoice and cannot continue until they have paid the required amount.

## Key Behaviors

- Payment gates are attached to **Send Message** steps in the workflow builder. To add one, open a message step for editing, click the **+** button in the message compose area, and select **Payment Gate** from the menu.
- A configuration modal opens where you select an invoice, choose a gate type, and set a threshold:
  - **Minimum amount** — the client must pay at least a fixed dollar amount before proceeding.
  - **Percentage of invoice** — the client must pay at least a given percentage of the invoice total.
- Save is disabled until both an invoice and a valid threshold are entered.
- After saving, a payment gate chip appears in the message step alongside any other attachments. The chip uses a shield icon and a bold title to distinguish it from other attachment types.
- Click **Update Step** to persist the gate configuration to the workflow.
- The gate's status — whether unpaid, partially satisfied, or cleared — is visible when viewing the workflow detail, so your team can track which clients have met the payment condition.
- To modify a gate's configuration after saving, remove the chip and add a new gate with the updated settings.

## Configuration

| Option | Description |
|--------|-------------|
| **Invoice** | The invoice the gate is tied to. Select from invoices associated with this workflow. |
| **Gate type** | **Minimum amount** — client must pay at least a fixed dollar threshold. **Percentage of invoice** — client must pay at least a percentage of the invoice total. |
| **Threshold** | The dollar amount (for minimum amount type) or the percentage (for percentage type). |

## Edge Cases & Limitations

- Payment gates can only be attached to Send Message steps. Other step types do not support this attachment.
- A payment gate must be linked to an invoice — gates without an invoice cannot be saved.
- There is no inline edit flow for existing payment gate chips. To change a gate's configuration, remove the chip and add a new gate.
- Conditional display and assignee settings available on the gate chip are attachment-level only and do not yet fully control when the gate becomes active. Use these settings with care until full condition and assignment support is confirmed.

## Related Features

- [Invoices](../payments/invoices.md)
- [Automation Rules](./automation-rules.md)
- [Triggers](./triggers.md)
