# Custom Terms

## Overview

Custom terms are agreement templates — such as retainer agreements and engagement letters — that clients must read and accept as a step in a workflow. Firms create and maintain custom terms templates; Glade presents the terms to clients at the designated point in their workflow.

## Key Behaviors

- Custom terms templates are written using a markdown-based editor with two tabs: **Edit** for drafting the content and **Preview** for reviewing the rendered result before saving.
- Variable references in the template (placeholders such as `{{PrincipalAttorney}}` or `{{invoice:RetainerFee}}`) are validated when you publish the template. If any reference cannot be resolved — for example, a typo in the variable name or a case mismatch — publishing is blocked and every invalid reference is listed in one error message so you can correct them in a single pass. This prevents broken placeholders from reaching client-facing retainers.
- Valid references include static fields like client name, attorney name, signature blocks, and case number; workflow context variables defined on any of your workflows; typed dynamic variables registered on the template; `invoice:<name>` references that match a line item on one of your invoice templates; and `attorney:<name>` references to the case's filing attorney. Variable names are case-sensitive — `principalAttorney` and `PrincipalAttorney` are not interchangeable.
- **Filing attorney references** are available through an `attorney:` namespace — for example `{{attorney:fullName}}` or `{{attorney:mailingAddress}}` — so an engagement letter or retainer can name the attorney handling the case and carry their details. The namespace covers the same information kept on the Attorney Information page: the attorney's name (in parts, and as one composed full name), email and phone numbers, bar and licensing details, the organization they practice under, USCIS number, and their mailing and physical addresses (in parts, and as one composed single-line address).
  - The attorney assigned to the case is used. If the case has no assigned attorney, the firm's default filing attorney is used instead.
  - Any detail that has not been filled in — and every reference on a case with no attorney and no firm default — renders as blank rather than printing a placeholder or "N/A" into a client-facing agreement.

> TODO: Confirm the exact variable name for each attorney detail, and whether the attorney variables are listed in the editor's variable picker or must be typed by hand.

- A formatting toolbar provides one-click actions for: bold, italic, underline, links, bulleted lists, ordered lists, paragraph breaks, and page breaks. Toolbar actions insert formatting at the current cursor position without repositioning you in the document.
- The **Preview** tab renders the terms in Times New Roman, matching exactly what clients see when they review and accept the agreement.
- Page breaks inserted in the editor are preserved in the preview and in the final client-facing document.
- When clients encounter a custom terms step in a workflow, the document is displayed in the same Times New Roman rendering as the editor preview.
- Clients must actively accept the terms to complete the workflow step.

### Editing the details on a client's agreement

**Edit details** changes the values filled into a client's agreement — the retainer amount, the fee, the time frame, and the like. Saving it updates every place those values are shown, not only the agreement itself:

- The **Details** panel above the agreement and the **Context** sidebar beside it are brought in line with what you saved, alongside the body of the agreement. Previously only the body picked up the change: a retainer edited from $500 to $1,000 read $1,000 in the agreement and $500 in both panels, with nothing your team could do to correct them.
- **The panels update while you are still looking at them.** Saving refreshes them in place, so the corrected figures appear as soon as the save finishes. For a short period both panels held their old values until you navigated away from the case and came back — the saved figures were right, but there was no way to confirm that without leaving the page.
- Agreements already showing an older value are corrected the next time someone saves **Edit details** on them. Nothing is repaired in bulk, so an agreement nobody re-saves keeps the values it is showing now.
- **Saving writes every detail, not only the one you changed.** Edit details submits all of the agreement's values together, so the panels are brought in line with the terms as a set. Where your firm enters a value in the sidebar that the agreement works out for itself — an amount taken from an invoice, for example — saving replaces the sidebar's figure with the agreement's. Check the sidebar after a save if your firm relies on entering those separately.

Two kinds of value are deliberately left alone, because **Edit details** cannot produce them:

- Context values that name a person, and those chosen from a fixed list — a case type, for example.
- A detail that feeds more than one context value on the same workflow. Neither is changed rather than Glade guessing which one you meant, so those keep their existing values.

### Who signs a manual-signature agreement

When an agreement is set to be signed by an attorney and you assign attorneys through **Assign collaborators**, the signature and its accompanying task go to the **first attorney in the list you assigned**. If an attorney who was already the signatory is still among those assigned, they stay the signatory. Assigning no attorney at all clears the signatory as before.

This only shows up when a firm assigns two or more attorneys in a single action. Previously the signature landed on an arbitrary one of them, so the same assignment could produce a different signatory on different cases.

## Configuration

Custom terms templates are created and managed from the firm's template library. Each template requires a name and a body. Once created, a template can be referenced as a step in a workflow template.

## Edge Cases & Limitations

- Custom terms content is read-only for clients — they can accept the presented terms but cannot edit the text.

> TODO: Confirm whether editing a custom terms template affects clients who are already mid-workflow, or only affects new workflow instances started after the edit.

## Related Features

- [Automation Rules](./automation-rules.md)
- [Task Templates](./task-templates.md)
