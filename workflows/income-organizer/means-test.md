# Means Test

## Overview

The Income Organizer feeds the Chapter 7 means test (and the Chapter 13 equivalent forms): the Current Monthly Income six-month average, the long-form means test deduction lines, and the Chapter 7 median income screen.

## Key Behaviors

### Means Test Income Window

For the Chapter 7 means test, a debtor's Current Monthly Income is the average of income across the six full calendar months before the month the case is filed. Glade anchors this six-month window to the **last completed calendar month**, so a month that is still in progress is never included.

- A pay stub dated in the current (still-running) month does not pull the window forward or drop the earliest month. For example, a case worked in June averages December through May, not January through June.
- Cases whose most recent pay stub already falls in a prior month are unaffected — the window is not forced to add empty current-month figures, so the average is not artificially lowered.
- Income sources that do not count toward the means test — Social Security and government assistance (such as welfare or food stamps) — are left out of the six-month average. They also do not anchor the window, so a benefit entry dated in the current (still-running) month does not pull the window forward and drop an earlier month. Previously a current-month government-assistance entry could shift the window forward and drop the earliest month's paychecks, understating the gross monthly income; excluded sources no longer affect the window. These sources still count where they belong elsewhere, such as on Schedule I.
- **A Schedule I calculation mode does not change Current Monthly Income.** Setting an employment source to YTD or to latest paystub shapes Schedule I and the long-form deduction lines only. The means test still averages the six full calendar months before filing, because that is what the statute and Forms 122A-1 / 122C-1 require. Previously Current Monthly Income followed whichever mode the source was set to, so a source on YTD or latest paystub produced a means-test figure that was not the six-month average. Re-check the means test on any case with an employment source set to one of those modes — the figure may have moved.

This applies to the standard six-month means test calculation. The YTD period method can still be applied to the means test deliberately, which flags it as a non-standard calculation method; see [Period Method Preview](./calculation-modes.md#period-method-preview).

### Long-Form Means Test Deductions

The means test deduction lines — taxes, involuntary deductions, life insurance, court-ordered payments, health care and HSA contributions, and (on Chapter 13) mandatory retirement — are calculated from the paystubs on the case instead of being typed in by hand. The figures reach the deduction lines of **Form 122A-2** (Chapter 7) and **Form 122C-2** (Chapter 13).

- The amounts are worked out from the same paystubs the organizer already holds, averaged by month the way Schedule I figures are. Records excluded from the means test, and non-means-test income such as Social Security, are left out.
- Figures appear on the forms after the organizer recalculates. Adding a paystub or correcting one and recalculating brings the deduction lines with it.
- This is separate from the current monthly income calculation that fills Forms 122A-1 and 122C-1. That calculation is unchanged; the deduction lines are what is new.
- **Mandatory retirement is counted once.** It is applied to the deduction line for it and is not also subtracted further down the Chapter 13 form, so disposable income is not reduced twice for the same contribution.
- On the questionnaire, these fields name the long form means test calculator as their source. Overriding one by hand sticks through later recalculations — see [Questionnaires](../questionnaires/README.md).

Lines the paystubs cannot answer are left blank rather than filled with `$0.00`, so a line you still need to answer is visibly unanswered instead of reading as a zero somebody meant.

### Chapter 7 Median Income Screen

The median income screen compares the client's annualized current monthly income directly against the household median income for their state and family size — deductions are not subtracted from this comparison. The result is shown clearly:

- A green check with the amount the client is **under** the median, per month, when income is below median.
- A red X with the amount the client is **over** the median, per month, when income is above median.
- The corresponding annual over/under amount is shown alongside the monthly figure.

Amounts of zero display as `$0.00` rather than a dash. When income or median data is missing, the screen shows a neutral state instead of a pass or fail.

## Edge Cases & Limitations

- Current Monthly Income is produced by two calculations while an older one is being retired, and the older one can still follow an employment source's Schedule I calculation mode. Where a case shows two different Current Monthly Income figures for a source set to YTD or latest paystub, the six-month average is the correct one.
- The long-form means test deduction lines are calculated for the household as a whole, which is what Forms 122A-2 and 122C-2 ask for. They are not broken out per debtor on the forms.
- Deduction lines the paystubs do not answer are left blank. A blank line is not a calculated zero — check it against the case before filing.
- Deduction figures appear only after the organizer recalculates. An organizer that has not been recalculated since these lines existed shows them empty; recalculate it to fill them.

## Related Features

- [Income Organizer](./README.md)
- [Income Calculation Modes](./calculation-modes.md)
- [Schedule I](./schedule-i.md)
- [Including and Excluding Income Records](./including-excluding-records.md)
- [Questionnaires](../questionnaires/README.md)
