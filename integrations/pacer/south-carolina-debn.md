# South Carolina (SCB) Chapter 7 DeBN Elections

## Overview

Chapter 7 cases filed in the South Carolina Bankruptcy Court need a completed Debtor's Election Re: Electronic Noticing (DeBN) form for each filer. Glade reads the election from the uploaded DeBN PDF and passes it to PACER.

## Key Behaviors

- Chapter 7 cases filed in the South Carolina Bankruptcy Court need a completed Debtor's Election Re: Electronic Noticing (DeBN) form for each filer. Glade reads the election directly from the uploaded DeBN PDF — there is no separate questionnaire question to answer. Upload the signed DeBN form to the document slot during document collection and Glade extracts the elected action automatically.
- For an individual case, upload the debtor 1 DeBN form. For a joint case, upload a DeBN form for each debtor — both the debtor 1 and debtor 2 elections are read and sent to PACER.
- The supported actions read from the form are **Activate**, **Deactivate**, **Update**, or **Decline**. The extracted answer is passed through to PACER so the SCB filing engine fills the matching radio on the local form.
- Auto-extraction runs on both individual and joint SCB Chapter 7 filings. Non-Chapter 7 filings do not require the DeBN extraction.
- Re-uploading a newer DeBN form supersedes the previously extracted answer. The most recent extraction wins, so correcting an earlier upload mistake is a matter of replacing the file in the document slot.

## Edge Cases & Limitations

- If a required DeBN form has not been uploaded by the time a qualifying SCB Chapter 7 case is submitted, the filing is blocked with an error naming the missing election so your team can add the document before retrying. On a joint case, the election is required for both debtors — a missing form for either filer blocks the filing.
- If an uploaded DeBN form cannot be parsed — for example, no radio button is selected on the form — the filing modal shows an inline **election picker** so you can recover without leaving the filing. Pick the election the debtor signed (**Activate**, **Deactivate**, **Update**, or **Decline**) and submit again; Glade saves the choice to the case and retries the filing. On a joint case, a picker appears for each debtor whose election could not be read. Re-uploading a clean copy of the form is still an option if you prefer to fix the source document.

## Related Features

- [PACER Integration](./README.md)
- [Supported courts](./supported-courts.md)
- [Filing packet document types](../efiling/filing-packet/document-types.md) — DeBN (Debtor 1) and DeBN (Debtor 2) labels.
