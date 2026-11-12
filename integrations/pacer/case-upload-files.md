# Case Upload Files

## Overview

Alongside the petition, the court's case upload step reads three files that Glade builds for the case: the debtor information file, the creditor information file, and the Creditor Matrix PDF. This page covers when those files are produced and how Glade checks the dollar figures in them before they reach the court.

## Key Behaviors

### When the case upload files are produced

The three files the court's case upload step reads — the debtor information file, the creditor information file, and the Creditor Matrix PDF — are built **once, when the schedules questionnaire is completed**. What the attorney reviews is what is filed.

- Compiling the petition uses the files as they already stand. Submitting the filing uses them as they already stand. Neither step rebuilds them.
- To produce new files, edit the schedules questionnaire and submit it again. That is the only thing that regenerates them.
- Previously the files were rebuilt at the moment of submission, from whatever the answers said at that instant — so a filing could go to the court as a version nobody had looked at.

**A known consequence.** Editing a questionnaire that has already been completed regenerates the petition PDF but not the creditor file or the Creditor Matrix. Until the questionnaire is submitted again, those two can be behind the current answers. Re-submit the schedules questionnaire after editing a completed one if the creditor list has changed.

### Negative amounts are caught before the files are built

Court case upload rejects a negative dollar amount outright, which used to surface as a filing failure with nothing in it to say which figure was at fault. Glade now checks the case's currency answers first:

- If any amount that the court expects to be zero or positive is negative, the filing is stopped before the files are generated and **every offending figure is named**, so all of them can be corrected in one pass rather than one failed submission at a time.
- Three figures that are legitimately allowed to run negative are exempted and reported to the court as `0.00`: monthly net income, monthly disposable income, and sixty-month disposable income. A genuine Schedule J or means-test deficit does not block a filing.
- **Income totals pulled below zero by a business or rental loss are also reported as `0.00`.** Monthly income (Schedule I line 12), current monthly income (Form 122A-1 line 11 / Form 122C-1), and each debtor's total current monthly income (Form 122A-1 line 17) can legitimately net below zero when the debtor has a business or rental loss. Glade reports these figures to the court as `0.00`, so the debtor information file is built. The form PDFs still show the real negative figure. The means-test result is unchanged, because a current monthly income of zero and a negative one are both below median.
- The problem is reported as a specific error on the filing rather than producing an empty debtor information file, which is how it previously failed.
- **On a Chapter 13 case, the Chapter 7 means-test income figures are ignored.** Chapter 13 questionnaires still carry the Chapter 7 means test (Form 122A-1) alongside the Chapter 13 one (Form 122C-1). Those Chapter 7 figures are not the case's current monthly income on a Chapter 13, because the Chapter 13 form supplies it, so they are not carried into the Chapter 13 case's debtor information file.

A Chapter 7 or Chapter 13 case that previously failed this way produced everything except the debtor information file, since the other documents are generated independently. The file is not created retroactively — **regenerate the case's documents** to produce it.

### Negative amounts in the pre-filing review

Alongside the petition, Glade sends the court a data file describing the case. None of the dollar figures in it can be negative. A negative figure — a monthly expense entered below zero, for example — is caught at review time and the finding **names the fields that are negative**, so you can go to them directly.

- Previously a negative amount was not caught. It failed quietly while the file was being built, so the first sign of trouble came at submission with nothing to identify the cause.
- The lines a court expects to be able to go negative are excluded and do not trip the check. This includes the income totals that a business or rental loss can pull below zero, listed above.

This is the **Negative amounts on the case-upload data** check in the [pre-filing review](../efiling/pre-filing-review/README.md), and it is blocking.

## Edge Cases & Limitations

- The creditor information file and the Creditor Matrix are only rebuilt when the schedules questionnaire is submitted. Editing a completed questionnaire refreshes the petition PDF but leaves those two behind until the questionnaire is submitted again — see [When the case upload files are produced](#when-the-case-upload-files-are-produced).

## Related Features

- [PACER Integration](./README.md)
- [Filing workflow](./filing-workflow.md)
- [Pre-filing review](../efiling/pre-filing-review/README.md)
- [Duplicate creditors check](../efiling/pre-filing-review/duplicate-creditors.md)
- [Questionnaires](../../workflows/questionnaires/README.md)
