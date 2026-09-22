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

### When a signed agreement cannot be generated

When a client signs, Glade produces the signed copy of the agreement before recording the signature. If that copy cannot be produced, the signature is not kept and the client can sign again.

- The agreement is treated as signed only once the signed copy exists. Only then is the client's **Agree to terms** task completed and, for an attorney-signed agreement, the agreement handed to the attorney.
- An agreement with no terms text is refused before anything is saved, rather than part-way through signing.
- Previously a failure at this point could leave the client's signature saved and their task completed while your team still saw the agreement as unsigned. The client could not sign again because the signature already appeared filled in.
- **A client who has already signed is not given a second Agree to terms task.** A later change on the workflow — regenerating the agreement or changing collaborators, for example — previously could open a new task for a client whose signature was already on the agreement.

### Invoice amounts on a retainer

A retainer can show amounts taken from the case's invoice — the base legal fee, for example. Those amounts are filled in once the invoice exists, and kept up to date while the retainer is unsigned.

- **Generating the invoice fills in the retainer.** When the invoice template links a line item — such as "Attorney Fees" — to an amount on the retainer, generating the invoice carries that link through even if the invoice's custom-terms field is left empty, and the retainer picks up the dollar amount.
- **Unsigned retainers update when the invoice does.** Creating the invoice, making it payable, or correcting its amount refreshes the figures on any retainer that has not yet been signed.
- Only the current version of the invoice counts. Voided, skipped, and superseded versions are ignored.
- **Signed, skipped, and hand-edited retainers are left alone.** A retainer that has been agreed to, skipped, or edited by your team is not rewritten when the invoice changes.

Previously a Chapter 7 retainer could go out reading `$[invoice:baseLegalFee not set]` in place of the fee, even after your team had generated the invoice and entered the amount, because the retainer was prepared before the invoice had any line items and was never refreshed afterward.

- A retainer still showing the placeholder is corrected the next time the invoice is generated or corrected. Retainers are not repaired in bulk.

### Printing an agreement for wet-ink signing

A firm can produce a complete, unsigned copy of a client's agreement to print and sign in ink, before the client has signed anything electronically. The copy carries the firm's letterhead and every detail filled in — the retainer amount, the fee, the attorney's name — exactly as the client would see it, with the signature lines left blank.

- The signature blocks print as empty ruled **By** and **Name** lines. They are not filled with the attorney's or client's name, and no handwritten signature image appears, so nothing on the page suggests it has already been signed.
- **Producing this copy does not sign, complete, or alter the agreement.** The client-facing e-signature step is untouched, the agreement stays unsigned, and the copy is not recorded as the executed document. If the client goes on to sign electronically, that produces the executed agreement as normal.
- It is available only while the agreement is still awaiting signature and has already been generated for the client. An agreement that has been signed, one that was skipped, and one that has not been generated yet cannot produce this copy.
- It is available to your firm's team members. Clients cannot produce it.

> TODO: Confirm where this action appears on the agreement and the file name the downloaded copy is given.

### Who signs a manual-signature agreement

When an agreement is set to be signed by an attorney and you assign attorneys through **Assign collaborators**, the signature and its accompanying task go to the **first attorney in the list you assigned**. If an attorney who was already the signatory is still among those assigned, they stay the signatory. Assigning no attorney at all clears the signatory as before.

This only shows up when a firm assigns two or more attorneys in a single action. Previously the signature landed on an arbitrary one of them, so the same assignment could produce a different signatory on different cases.

### The name on the attorney's signature

When an attorney countersigns an agreement, the name printed in the attorney's signature block is the attorney's own name, not the client's.

- Previously the signing form could arrive pre-filled with the client's name, and a typed signature then printed that name in the attorney's block — even though the signing certificate correctly recorded the attorney. If the name submitted for the attorney matches the client on the agreement, the attorney's own name is used instead.
- A customized attorney name that is not the client's — for example "Jane Smith, Esq." — is kept as entered.
- If the name is left blank, the signing attorney's name is used.
- Agreements already signed before this correction are not changed. Check the attorney signature block on any recently countersigned agreement where the client's name may have been printed.

### When a joint signer has no signature slot

On an agreement carrying more than one client signature slot — a joint retainer, typically — each slot is assigned to a particular signer. If the person signing has no slot assigned to them, for example because both slots were assigned to the attorney rather than one to each spouse, the attempt is refused with an error.

- Previously the page refreshed with the signature still blank and the **Agree to terms** task still outstanding, and nothing explained why. The signer could try repeatedly and never complete the step.
- When this happens, check who each signature slot on the agreement is assigned to and point the right slot at the spouse who is signing.
- Agreements with a single client signature slot are unaffected. That slot is used whoever it is assigned to.

### When the agreement was never assigned to the client

An agreement is created for a particular client, and that client can open and sign it even where the workflow step it came from does not list them among the people it is assigned to.

- Previously a client in that position could see the agreement on the case but was refused with **"This task has not been assigned to you."**, and no **Agree to terms** task was created — so the step could not be completed by anyone. Chapter 13 retainers on cases started from a firm's own workflow templates were the common case, because that step's assignment list is often left empty.
- The client now also gets the **Agree to terms** task, so the agreement reaches their task list rather than sitting only on the case.
- **Access that was deliberately taken away is not handed back.** Where the agreement has been passed to the attorney to sign, or the step has been skipped, the client cannot open, reset, or skip it — including a client who was never assigned it in the first place.
- Live cases already stuck in this position can be opened and signed straight away. Their **Agree to terms** task appears the next time something happens on the agreement; new cases get the task when the agreement is created.

Invoices already worked this way — the client an invoice is for can open it whether or not they were assigned it.

## Configuration

Custom terms templates are created and managed from the firm's template library. Each template requires a name and a body. Once created, a template can be referenced as a step in a workflow template.

## Edge Cases & Limitations

- Custom terms content is read-only for clients — they can accept the presented terms but cannot edit the text.

> TODO: Confirm whether editing a custom terms template affects clients who are already mid-workflow, or only affects new workflow instances started after the edit.

## Related Features

- [Automation Rules](./automation-rules.md)
- [Task Templates](./task-templates.md)
