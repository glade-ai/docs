# Schedule I Line 8a

## Overview

Schedule I reports business, professional, and rental income on one line (line 8a). Where a business or rental source has a profit and loss statement — uploaded as a document or typed in by hand — that statement is what the line uses for that source. The line totals every business the debtor holds.

## Key Behaviors

- **A statement takes precedence over the month-by-month entries for the same source.** Previously the line was derived only from the month entries, so a statement reached the per-business detail behind the line while the line itself ignored it. The organizer could show a figure built from a statement and a Schedule I line that disagreed with it.
- **Precedence is decided per income source.** A business with a statement uses the statement; another business on the same case with only month entries carries on using those. Both still add into the same Schedule I line.
- A source that has a statement and no month entries is still counted. It is no longer dropped for having nothing month-by-month behind it.
- This matches how the organizer already treats year-to-date figures, where a document that summarizes a period supersedes the individual rows for that source.
- The change takes effect the next time a case's figures are recalculated. Cases whose businesses have no statements are unaffected, and nothing needs re-running on them.
- **Every business on the case reaches Schedule I.** The business income line totals every business the debtor holds, and each business also carries its own figures for the per-business attachment the form asks for. Previously only one business's figures reached the questionnaire, and a debtor with two businesses had one business's numbers presented as the whole of the line — an understated income figure on a form signed under penalty of perjury. **Re-check the business income line on any case with more than one business or rental source.**

### Choosing which statement counts

Each profit and loss statement on a business has its own **Schedule I** checkbox, the same control a paystub has. It decides whether that statement can be used for the business's line 8a figure.

- **Statements are included by default.** Nothing changes on a case until someone unchecks a statement.
- **The business averages every included statement.** Where a business has several checked statements, line 8a adds up the totals of all of them and divides by the number of months they cover together. A month that ran at a loss lowers the figure, the order the statements were entered in makes no difference, and a quarterly statement counts three times as much as a monthly one. Previously only the most recent checked statement was used, so a business with six monthly statements showed the last month's figures alone and earlier loss months had no effect.
- **Undated statements are left out of the average.** A statement with no known period is not averaged in, though it still appears in the business's list of statements. If every statement on a business is undated, the business has no statement figure.
- **One incomplete statement holds back the whole business.** If any averaged statement has lines that can't be counted — a missing amount, an unclear direction, unknown units, or an older-format statement — the business shows no figure until those lines are resolved. Glade shows no number rather than a wrong one. Each "needs review" reason now names the statement it belongs to, since the figure no longer comes from a single statement.
- **The means test follows the average.** The business income lines on Form 122A-1 (lines 5–6) read the same figure, so they also use the average rather than the latest statement.
- **An unchecked statement contributes nothing.** It does not reach line 8a, and because the means test's business income figure comes from the same calculation, it does not reach the means test either.
- **A business with every statement unchecked has no statement figure.** It contributes nothing from its statements to line 8a.

> TODO: Confirm whether a business with every statement unchecked falls back to its month-by-month entries for line 8a, or contributes nothing at all.

If your team has reviewed a Schedule I line 8a figure on a case where a business has a profit and loss statement, re-check it — the line now reflects the statement.

Existing cases switch to the averaged figure the next time their figures are recalculated. Re-check line 8a, and the means test business lines, on any case where a business has more than one statement.

## Configuration

| Setting | Description |
|---------|-------------|
| Schedule I checkbox on a profit and loss statement | Whether that statement can be used for its business's line 8a figure. On by default; the business averages all of its checked statements |

## Edge Cases & Limitations

- A profit and loss statement wins over the month entries for the same source on Schedule I line 8a. Where a business has both, the month entries are not added on top and are not shown as excluded — they are simply not what the line is built from. Remove the statement if the month entries are the figures you want.
- **Overlapping statements are not reconciled.** Each checked statement counts on its own, weighted by the months it covers. If a business has, say, a January–September year-to-date statement and monthly statements for April–September, the overlapping months are counted twice. Uncheck the redundant statement to remove the overlap.
- The average covers every checked statement, with no time window. Where the statements span more than six months, the means test business lines use that longer average rather than exactly the six-month lookback period.
- Unchecking a statement's Schedule I box does not delete it. The statement stays on the business and can be checked again.
- Only a limited number of businesses get their own per-business attachment detail on Schedule I. A debtor holding more than that still gets a correct business income total; the individual breakdowns beyond the limit are not carried onto the form. Contact Glade if a case needs more.

> TODO: Confirm the number of businesses that receive their own Schedule I attachment breakdown, and what a firm sees when a case exceeds it.

## Related Features

- [Business and Rental Income](./README.md)
- [Profit & Loss Statements](./profit-and-loss-statements.md)
- [Matching Statements to Businesses](./matching-statements-to-businesses.md)
- [Schedule I](../schedule-i.md)
- [Including and Excluding Income Records](../including-excluding-records.md)
- [Income Organizer](../README.md)
