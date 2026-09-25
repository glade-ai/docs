# AI-Suggested File Names

## Overview

Before a document request is submitted for review, Glade suggests a descriptive name for each uploaded file based on its contents. Your team reviews the suggestions in a bulk rename step and approves the ones to apply. This page covers the bulk rename modal and what kinds of documents the suggestions recognize.

## Key Behaviors

- **AI-suggested file names** can be reviewed and applied in bulk before submitting a document request for review. The bulk rename modal lists each file with its current name and the AI-suggested name; each suggestion is editable inline and starts **un-approved** so nothing is renamed without your explicit OK. The modal includes a reminder that "Approved renames will overwrite the current file names" and, once you start approving suggestions, an in-modal warning tallies how many existing names will be overwritten ("This will overwrite N existing file names"). The footer button shows the same count — for example, **Apply 3 Renames** — and is disabled until at least one suggestion is approved.
- The submit-for-review AI rename prompt is limited to firm dashboard users.

### What the AI-suggested names recognize

The suggestions offered in the bulk rename step cover most of what clients actually upload to a bankruptcy intake. Until recently they did not: about one document in twenty came back named **UnrecognizableDoc**, which made it the single most common suggestion on the platform. Reviewing a month of real uploads showed only about a fifth of those genuinely had no document in them — the rest were ordinary intake paperwork with no name available for it.

The following are now recognized and named:

- **Court judgments, collection suits, writs, and summonses.** This was the largest group by volume, and the one worth knowing about: these are creditor claims arriving as unnamed files, not filing clutter.
- **Bankruptcy court documents** — discharge orders, trustee correspondence, and petition packets.
- **PACER and Case Locator search receipts.**
- **Payment receipts and remittance advice.**
- **Vendor and business invoices.**
- **Loan, title, and closing documents.**
- **Divorce and family law documents**, and **letters from attorneys**.
- **Signature pages**, named from the official form number printed in the page footer — for example *Signature Page - 106C*. Client photos of individually signed petition pages previously had no category at all.

Two naming problems were corrected at the same time:

- **A monthly profit and loss statement keeps its period.** The name format only allowed an exact day-to-day date range, so a statement covering a named month with no specific dates on it was named as undated — which had become the most common result for P&L statements even though the month was printed on the document.
- **Names are more consistent for the same situation.** A document containing several types is named with the plain category rather than sometimes carrying a year; a missing piece of a name is left out once rather than repeated; and payment-app statements no longer carry a meaningless account-number segment.

**What the checklist item is for is now taken into account.** A file uploaded against a checklist item is read knowing which document was asked for, so a page dropped into a Signature Pages item is interpreted in that light. The document's own contents still take precedence when the two disagree, so a misfiled upload is not named after the item it landed in.

**UnrecognizableDoc is still the right answer for some files** — a photo of a room or an object, a screenshot, a blank page, "N/A OR NONE", a handwritten note. Those were correctly named before and are unchanged.

## Edge Cases & Limitations

- These improvements apply to documents parsed from this point on. A document already uploaded keeps the suggestion stored for it — use **re-run AI** on the document to get a fresh one.
- Suggestions are still only suggestions. Nothing is renamed until someone on your team approves it, as described above.

## Related Features

- [Document Collection](./README.md)
- [Renaming and Downloading Files](./renaming-and-downloading-files.md)
- [Uploading and Reviewing Documents](./uploading-and-reviewing.md)
