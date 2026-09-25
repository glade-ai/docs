# Editing and Versioning Invoices

## Overview

Invoice changes are handled differently depending on what is being changed. Settings can be changed in place, but changing line items or amounts on an invoice that has already been sent or partially paid creates a new version and preserves the original. This page covers what triggers a new version and how payments, payment plans, and custom-terms links carry over.

## Key Behaviors

- **Settings changes** (title, payment configuration, enabled payment methods, the invoice note) can be updated directly on an active invoice without creating a new version.
- **Line item or amount changes** on an invoice that has already been sent or partially paid trigger versioning:
  - The original invoice is marked as "Edited" and becomes read-only.
  - A new invoice is created with the updated line items and amounts.
  - The new invoice references the original, maintaining a complete audit trail.
  - Any credits from payments already made on the original invoice carry forward to the new version.
  - If those carried-over payments already cover the new total — for example, when you edit an invoice that was already paid in full, or lower the amount so what the client already paid now covers it — the new version is marked **Paid** right away instead of showing a balance still due for money that was already collected. Anything that depends on the invoice being paid (workflow steps that were waiting on payment, payment-plan completion) advances just as it would after a normal final payment. If a balance still remains after the carried-over payments are applied, the new version stays payable (**In Progress**) for the difference.
  - An active payment plan on the original invoice moves to the new version instead of being canceled, so the client's autopay arrangement survives the edit. If the new total is higher and the plan no longer collects enough, installments are added to cover the difference; if the carried-over payments already cover the new total, the remaining installments are canceled. See [Payment Plans](../payment-plans/README.md).
  - Payments stay attached to the active invoice version, including ACH / bank-transfer payments. If a bank transfer confirms *after* the invoice has been edited, the confirmation is applied to the new active version rather than stranding the payment on the read-only original — so a paid ACH payment no longer disappears from the invoice when it is edited around the same time the payment settles.

This approach preserves a clean history of what was billed and what changed, which is important for legal billing compliance and client transparency.

Editing a line item keeps its link to any custom-terms variable that references it. Some line items are referenced by name in custom terms documents (for example, a retainer agreement that pulls the attorney-fee amount from the invoice). Editing the invoice's line items no longer clears that link, so the referenced amount continues to render in the agreement instead of showing a "not set" placeholder.

## Edge Cases & Limitations

- **Edited invoices are read-only:** When an invoice is versioned due to line item changes, the original becomes permanently read-only. All future activity happens on the new version.

## Related Features

- [Invoices](./README.md)
- [Invoice Lifecycle](./invoice-lifecycle.md)
- [Payment Plans](../payment-plans/README.md)
- [Custom Terms](../../workflows/custom-terms.md)
