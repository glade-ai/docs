# Generating a Draft Petition

## Overview

While you are still working on a bankruptcy schedules questionnaire, you can generate a draft petition to review or send for review — without submitting the questionnaire. This page covers generating a marked draft or an unmarked copy for signatures, what goes into the draft and where it is saved, and how the draft packet is rebuilt when a completed questionnaire is edited.

## Key Behaviors

### Generating a draft

Three actions sit together on the form: **Check petition**, **Generate draft**, and **Submit petition**.

- **Generate draft** builds the petition PDF from the answers as they stand right now. The schedules task stays open, the workflow does not advance, and the client is not notified. Only **Submit petition** does those things, and its behavior is unchanged.
- **Generate draft** offers two choices — the marked draft described below, and an unmarked copy for signing. See [An unmarked copy for signatures](#an-unmarked-copy-for-signatures).
- You can generate a draft as many times as you need while you keep editing. Each run produces a fresh PDF from the current answers.
- A short status message appears while the PDF is being assembled. When it is ready, a **Draft petition generated** message with an **Open draft** link stays on the form — the link opens that exact draft in a new tab, so you can come back to it after the status message has gone.
- Clicking **Generate draft** again while a draft is already being built does not start a second run.

Generating a draft is available to your team on a supported bankruptcy schedules questionnaire. Previously the only way to produce a petition PDF was to submit the questionnaire, which also completed the schedules task and moved the case forward — so a paralegal who wanted a copy to check had to advance the case to get one.

### The draft is marked as a draft

Every page of the **Petition (Draft)** document carries a marking down the right-hand margin: the Glade mark, the word **DRAFT** repeated down the page, and a shield showing how many blocking issues the petition check found at the moment the draft was built.

- The marking exists so a printed draft cannot be mistaken for the filing copy once it is off the screen and in a stack of paper on a desk.
- The **shield count matches the Petition Check badge** — it counts blocking findings, and it leaves out signature fields, exactly as the badge in the questionnaire header does. It is a snapshot from when the draft was generated, so it does not move as you correct fields; generate a new draft to refresh it.
- **Signature Pages are not marked.** The pages a client signs in ink come from the unmarked copy, so nothing overprints a signature block.
- **The petition compiled for filing is not marked.** Only the draft carries it.
- If the marking or the issue count cannot be produced for some reason, the draft is still generated — just without the marking — rather than the generation failing.

### An unmarked copy for signatures

The marking down the margin is what makes the draft unsuitable to sign, so **Generate draft** also produces an unmarked copy on request. Choosing it opens two options:

- **Generate draft petition (with watermark)** — the marked **Petition (Draft)** document described above. This is what the button has always done.
- **Generate petition for signatures** — the same petition, built from the same answers, with no marking. It is saved as **Petition for Signatures (Draft)** in Forms & Schedules, next to the marked draft rather than in place of it.

Use the second when you are collecting wet-ink signatures from the debtor before the case is ready to file, and the first when you want a review copy that cannot be mistaken for the filing version.

- Both documents are produced when you ask for the unmarked one, so the marked draft stays available.
- **Submitting the questionnaire produces it too.** Submitting a bankruptcy schedules questionnaire saves **Petition for Signatures (Draft)** alongside the marked **Petition (Draft)** and the separate signature pages, so nobody has to remember a second **Generate petition for signatures** run after every submit. The progress message shown while the documents are assembled covers the new file.
- **Generate petition on demand is unchanged.** Asking for the marked draft on a case that has no unmarked copy still does not create one — only a submit, or an explicit **Generate petition for signatures**, does that.
- **The two never drift apart.** Once a case has an unmarked copy, it is rebuilt every time the draft is regenerated — by hand or automatically — so the pages the debtor signs always match the current draft.
- The **Open draft** link after generation opens whichever document you asked for.
- If the unmarked copy cannot be produced, the action reports an error rather than quietly handing back the marked draft in its place.

### What goes into the draft, and where it is saved

When you generate a draft you choose which of the case's documents go into it and the order they appear in. Two further options control what is produced and where it is filed:

- **Generate signature pages PDF separately** — as well as the compiled draft, Glade pulls the signature pages out of it and files them as their own **Signature Pages.pdf**. The pages the debtor has to sign can then be printed or sent on their own, without the rest of the petition alongside them. With the option off, no separate document is produced.
- **Save location** — choose which of the case's document folders the draft is saved into. The draft and the separate signature pages document both go to the folder you pick. With no choice made, both are saved to **Forms & Schedules**, which is where drafts have always gone.

Both options were previously offered on the form but had no effect on what was produced. A draft was always saved to Forms & Schedules and never came with a separate signature pages document.

If the signature pages cannot be pulled out of the compiled draft, the draft itself is still produced and saved to the folder you chose — you simply do not get the separate document. Generating the draft again is safe and produces both.

> TODO: Confirm what the draft's version choice — working draft, or for signatures with no watermark — does on this path, and whether a draft compiled this way is marked at all. The petition compiled here is assembled from documents that were generated earlier, so it does not carry the margin marking described above.

The creditor matrix is appended to the petition draft as its final pages — see [Creditors](../schedules/creditors.md#the-matrix-in-the-petition-draft).

### Editing a Completed Questionnaire After the Petition Is Drafted

When a **completed** Bankruptcy Schedules questionnaire is edited, Glade rebuilds the case's petition draft packet on its own — the filled court forms, the **Petition (Draft)** document, and the **Signature Pages** — so Forms & Schedules shows the edit instead of an out-of-date packet. Previously the packet stayed as it was at completion, and a correction made afterward did not reach the draft until someone regenerated it by hand.

- Rebuilding happens only for a questionnaire that has already been completed. Saves made while a questionnaire is still in progress do not rebuild anything; the packet is first produced when the questionnaire is completed.
- The replacement documents are put in place before the previous ones are removed, so the case is never left with no draft.
- If a rebuild produces no signature pages, the earlier Signature Pages file is still removed rather than leaving an obsolete packet on the case.
- Several edits saved in quick succession produce one rebuild from the latest answers, not one per save.
- Only the documents are rebuilt. Downstream workflow steps, notifications, and tasks that ran when the questionnaire was first completed are not triggered again.
- This applies to Glade's own questionnaire templates. Questionnaires on an external form provider are not rebuilt this way.

## Edge Cases & Limitations

- Petitions already generated are not rebuilt when a generation correction ships; generate the petition again to pick it up.
- The shield count on a draft is a snapshot and does not update as fields are corrected.

## Related Features

- [Questionnaires](../README.md)
- [Petition](./README.md)
- [Petition Check](./petition-check.md)
- [Signatures](./signatures.md)
- [Signature Pages](../../signature-pages.md)
- [Creditors](../schedules/creditors.md)
- [PDF Fill Mappings](../templates/pdf-fill-mappings.md)
