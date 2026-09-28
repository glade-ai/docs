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
- **The business uses its latest included statement.** Where a business has several statements, the most recent one that is still checked is the one line 8a is built from. Uncheck a newer statement to fall back to the one before it.
- **An unchecked statement contributes nothing.** It does not reach line 8a, and because the means test's business income figure comes from the same calculation, it does not reach the means test either.
- **A business with every statement unchecked has no statement figure.** It contributes nothing from its statements to line 8a.

> TODO: Confirm whether a business with every statement unchecked falls back to its month-by-month entries for line 8a, or contributes nothing at all.

If your team has reviewed a Schedule I line 8a figure on a case where a business has a profit and loss statement, re-check it — the line now reflects the statement.

## Configuration

| Setting | Description |
|---------|-------------|
| Schedule I checkbox on a profit and loss statement | Whether that statement can be used for its business's line 8a figure. On by default; the business uses its latest checked statement |

## Edge Cases & Limitations

- A profit and loss statement wins over the month entries for the same source on Schedule I line 8a. Where a business has both, the month entries are not added on top and are not shown as excluded — they are simply not what the line is built from. Remove the statement if the month entries are the figures you want.
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
