# Paystub Extraction

## Overview

When a paystub document is uploaded to a case, Glade extracts income fields automatically. This doc covers how the reader handles paystub layouts — current-period versus year-to-date columns, itemized breakdowns, two-column deductions, separately listed bonuses, net pay labels — and how multiple paystubs with the same pay date are kept.

## Key Behaviors

YTD fields (such as year-to-date gross pay and year-to-date overtime) are used when the income source is set to YTD mode.

On paystubs that print current-period and year-to-date figures side by side, the two columns are kept apart: the pay-period gross is read from the current-period column and the year-to-date gross from the YTD column. Previously a year-to-date total could be recorded as the pay-period gross while the YTD figure was left blank, which showed income amounts that did not match the paystub and could overstate the monthly averages carried onto Schedule I and the means test.

When Glade reads a paystub on its own — on upload, on a re-read, or during a background catch-up — the itemized breakdown it extracts is kept. Individual earnings lines and individual deduction lines stay as separate entries. Previously an automatic read also wrote its column totals back over that breakdown, collapsing the itemized lines into a single total and sometimes leaving a stray "other" post-tax deduction entry that was not on the paystub. Figures your team enters or corrects by hand — including months and income items you add yourself — continue to update the income data as before.

**Deductions printed in two columns.** Some paystubs — government back-pay stubs are the common case — list each deduction twice, once as the current pay period amount and once as an adjusted amount. Glade adds the two together for each deduction rather than reading only the current column. Previously the adjusted column was ignored, which understated the client's total deductions and, on the Chapter 7 means test, overstated the income remaining after them.

**Year-to-date gross when a bonus is listed separately.** On paystubs that print a bonus on its own line outside the year-to-date earnings subtotal, the year-to-date gross is taken as the subtotal shown on the stub. Previously the pay period's bonus could be added on top of a subtotal that already accounted for it, inflating year-to-date gross — and, for any employer set to YTD mode, every monthly figure derived from it.

**Take-home pay is read from the net pay line, not the gross.** Stubs that label take-home as **Net Pay ACH**, **Net Pay Check**, or **Direct Deposit** rather than plainly as *Net Pay* had their **Gross Earnings** figure recorded as net, overstating monthly take-home by a wide margin — around 27% on the stubs where this was reported, which was enough to hold up a Chapter 7 filing.

- Those labels are now recognized, and where a stub prints both an ACH and a check amount the two are added together.
- As a check on the result, the net figure is re-worked from the gross less the deductions actually printed on the stub when it comes out at or above the gross, **or** when it differs from that gross-less-deductions figure by more than $50. The same check runs on the year-to-date net. Deduction categories the stub does not print are left empty rather than being recorded as $0.00.
- The second condition catches stubs where the reader picked up a printed **earnings subtotal** — regular, holiday, vacation, and similar pay added together — as net pay. That subtotal sits below gross, so the first check alone let it through and the organizer showed inflated take-home. On the stub where this was reported, an earnings subtotal of $2,159.59 was recorded as net against a true take-home of $2,076.58. A printed net within $50 of gross less deductions is left as printed.
- **Schedule I still uses gross pay** — it always did. What was wrong was the net column, and anything reading from it.
- Re-read an affected paystub to correct it. A stub whose net figure looks close to its gross is the symptom worth checking on income entered earlier.

**Values still awaiting your review are not counted.** When a figure read from a document disagrees with what is already on the case, it is held for your team to review rather than applied (see [Document Collection](../document-collection/README.md)). The Income Organizer's figures use confirmed values only — a value sitting in review, or one your team has already rejected or replaced with a correction, does not feed the totals. Previously the organizer could pick up a pending value while the rest of the case used the confirmed one, so the same figure read differently in two places.

### Two Paystubs With the Same Pay Date

A client can have more than one distinct paystub carrying the same pay date — a regular check plus a bonus, or a correction issued the same day. All of them are kept.

- Each uploaded document appears as its own row. Previously only one of them survived, and the others stayed in the queued-for-analysis bucket indefinitely even though Glade had already read them.
- Because the row that survived was picked afresh on each load, Schedule I figures could change on their own from one refresh to the next. They no longer do.
- Re-reading the same document still updates its existing row rather than adding a second one, so a re-upload or a re-run of the extraction does not double a month.

If your team has an organizer where paystubs stayed stuck on **Queued for analysis** after extraction finished, re-open it — the affected stubs appear as ordinary rows, and the month's Schedule I figure should be re-checked, since it was previously calculated from only one of them.

## Edge Cases & Limitations

- Paystubs extracted before the current/year-to-date column handling was corrected are not re-read automatically. If an existing row shows a year-to-date figure in its pay-period gross, re-run extraction on that row or correct the extracted data by hand.
- The earnings-subtotal net correction also applies only to paystubs uploaded or re-read after it was introduced. A stub read beforehand keeps its net figure until it is re-read.
- The same applies to the two-column deduction and year-to-date bonus corrections: rows extracted beforehand keep the figures they were read with. On a case where the client's paystubs carry an adjusted deduction column or a separately-listed bonus, re-run extraction on those rows before relying on the deduction totals or the year-to-date gross.

## Related Features

- [Income Organizer](./README.md)
- [Upload Processing Status](./processing-status.md)
- [Editing Income Records](./editing-income-records.md)
- [Income Calculation Modes](./calculation-modes.md)
- [Document Collection](../document-collection/README.md)
