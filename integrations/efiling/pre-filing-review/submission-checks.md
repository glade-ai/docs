# Submission Checks and Duplicate Filings

## Overview

Several warnings used to exist only in a dialog that opened at the moment you submit. They are now pre-filing review checks like any other. This page covers those checks, including how Glade prevents a case from being filed twice.

## Key Behaviors

### Checks that used to appear only at submission

Several warnings used to exist only in a dialog that opened at the moment you submit. They are now review checks like any other, so they appear on the review your team works through rather than arriving as a surprise on the last click:

- **The case already has a case number**, and **a filing is already in progress on the case**, are blocking.
- **A recent filing attempt on the case** is advisory.
- **Missing required filing fields** is blocking, and the finding names the fields. This is the same set of fields as the [required fields check](./required-fields.md).
- **Schedule I and J figures missing on a Chapter 7 case** is advisory. This is what feeds the surplus comparison described in [Electronic Court Filing (eFiling)](../README.md); where the figures are not there to compare, the review says so instead of the comparison silently not happening.
- **A court notice on the case matching this client** is advisory.

That dialog has since been retired — see [Where pre-filing checks run](./README.md#where-pre-filing-checks-run). The distinction between a hard block and a soft warning is unchanged, and is now expressed as the blocking and advisory severities in the review; [Preventing duplicate filings](#preventing-duplicate-filings) describes how it applies to a repeat filing attempt.

Each of these fails closed. Where a check cannot gather what it needs — the case's filing history is unreadable, for example — it reports as unresolved rather than passing, so a check with nothing to go on never quietly clears a filing.

> TODO: Confirm what the court notice check is comparing and what a firm should do about a finding from it. The source change lists it as an advisory rule migrated from the existing pre-filing warnings, but not the condition that raises it.

### Preventing duplicate filings

Before a filing proceeds, Glade checks whether the case already has an assigned case number or an in-progress filing. Depending on the situation, you will see one of two states in the pre-filing dialog:

- **Hard block** — If a case number already exists, or if a filing is actively in progress for the case, the dialog shows only a **Go Back** button. You cannot proceed until the existing filing resolves. A red alert banner in the eFiling modal also shows the blocking reason.
- **Soft warning** — If a recent filing attempt exists but does not meet the hard-block conditions, you can review the details and continue by checking an acknowledgment checkbox and clicking **Continue Anyway**.

At the moment you click the final submit button, Glade performs a fresh check. If the status has changed to a hard-block condition while the dialog was open, the submission is blocked and you will see a toast and an updated alert banner.

These three situations — an existing case number, a filing already in progress, and a recent filing attempt — are also reported by the pre-filing review, so your team sees them while working through the review rather than only when the submission dialog opens. The dialog itself behaves exactly as described above.

> TODO: The source docs describe the pre-filing dialog above as still in use, while [Where pre-filing checks run](./README.md#where-pre-filing-checks-run) says the older submission dialog has been retired. Confirm whether this dialog is the one that was removed.

## Edge Cases & Limitations

- Once a case number is assigned, Glade hard-blocks any further automated filing attempts for that case. To file again (e.g., for an amended petition), contact support or file directly in PACER. See [Amending a filing](../../pacer/amending-a-filing.md).

## Related Features

- [Pre-filing Review](./README.md)
- [Required fields check](./required-fields.md)
- [Case numbers](../../pacer/case-numbers.md)
- [Filing progress](../filing-progress.md)
