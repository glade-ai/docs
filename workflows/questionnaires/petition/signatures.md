# Signatures

## Overview

When a questionnaire or case document with signature fields is submitted or turned into a PDF, Glade asks how signatures should be handled before it produces anything. This page covers the signature confirmation choices, generating a PDF from a case document, and where the names on generated signatures come from.

## Key Behaviors

### Signature confirmation at submission

When the signature confirmation modal appears at submission time, you have three choices:

- **Sign** — apply or confirm the signature and submit.
- **Skip** — submit while keeping any signature values that were already entered in the questionnaire. Use this when you have manually typed signatures earlier and want them preserved on the saved draft or PDF.
- **Clear & Submit** — clear every signature field on the questionnaire (including signatures inside list and table rows) and then submit. Use this when you are saving the questionnaire as a draft for client review and the draft should not show any signatures or signing dates.

**Submit Anyway** is also available when a required signature has been skipped — you can submit the questionnaire without completing the signature. See [Submitting a Questionnaire](../filling-out/submitting.md).

### Generating a PDF from a case document

**Save & Generate PDF** on a case document asks about signatures before it produces the PDF, the same way submitting the schedules questionnaire does. Where the case document has signature fields on it, the signature confirmation modal opens first and offers the same three choices — generate the signatures, skip and keep whatever is already entered, or clear them — and the PDF is produced afterwards.

- Previously the PDF was written immediately, so a local form could go out with a blank signature block, or with a signature left over from an earlier round, even though the questionnaire already knew how to collect one.
- **Cancelling the modal leaves the case document as it is** and produces no PDF.
- **Generating the PDF does not submit or complete the case document.** The form stays open and the workflow does not advance — this is only about producing the document.
- A case document with no signature fields on it generates straight away, with no modal.

### Where the names on generated signatures come from

When signatures are generated for a bankruptcy schedules questionnaire, each signer's typed name is taken from the name recorded on the case — the debtor's, the spouse's on a joint case, and the attorney's, each read as separate first, middle, and last name entries.

- **Middle names now appear.** The debtor's and the spouse's names previously came from a single combined name that had nowhere to hold a middle name, so a middle name recorded on the case never reached their signature. The attorney's name was read from a different record again. All three signers now read from the same place.
- Where a signer has no name recorded on the case, Glade falls back to the name it used before, so a case that was signing correctly continues to.
- Correct a name that comes out wrong on the case record rather than on the signature itself, and the next generated signature picks it up.

## Edge Cases & Limitations

- The Petition Check counts incomplete signatures separately, and a signature mark with no name after it is not accepted as complete — see [Petition Check](./petition-check.md#signature-date-and-currency-answers).

## Related Features

- [Questionnaires](../README.md)
- [Petition](./README.md)
- [Generating a Draft Petition](./draft-petition.md)
- [Submitting a Questionnaire](../filling-out/submitting.md)
- [Case Documents](../../case-documents.md)
- [Signature Pages](../../signature-pages.md)
- [E-Signatures](../../e-signatures.md)
