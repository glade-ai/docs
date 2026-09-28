# Profit & Loss Statements

## Overview

A business or rental income source holds its own profit & loss statements, and the figures on those statements feed the business income line of Schedule I (line 8a). A profit & loss statement for a business or a rental is recorded the way the document prints it — one entry per printed line, filed under the accounting category it belongs to — together with the period it covers and the totals printed on it. It is no longer folded into a handful of pre-summed figures as it is read.

## Key Behaviors

### Uploading and reading a statement

- **Adding a business or rental income source creates a place to upload its statements.** Each source is recorded as a business in its own right, and each statement uploaded against it is kept as its own record of the period it covers.
- **An uploaded statement is read automatically.** Glade records the statement's income and expense lines as they are printed, the period the statement covers, and the totals printed on it, then sorts the expense lines into the itemized expense categories Schedule I asks for. Previously a profit & loss statement could not be read at all — it settled as a document with no extractable data, and the itemized expense lines had no source anywhere on the case, so they had to be entered by hand.
- **Nothing is computed from the statement by the reader.** The monthly figures Schedule I needs are worked out from the recorded values afterwards, so the numbers on the statement stay exactly as the client's bookkeeper printed them.
- Every statement uploaded against a source is kept. A newer statement does not replace an earlier one.
- Each parsed record shows which uploaded document it came from.
- **Business and rental sources are labeled separately**, so the two can be told apart in the organizer.

### Line-by-line figures

- **Each printed line can be corrected on its own.** Previously the figures were added up as the statement was read, so correcting a single line meant retyping the whole bucket it had been summed into, and there was no record of what the document itself said.
- **The lines feed Schedule I line 8a.** Each accounting category is mapped onto the line 8a it belongs to and converted to a monthly figure, which is what the Schedule I section of the bankruptcy schedules questionnaire shows.
- **A dash or a blank amount on a line is read as zero.** Bookkeepers commonly print a dash (`-` or `—`) or leave the amount cell empty to mean nothing was earned or spent on that line. Glade records such a line as $0, so the business's gross income and the totals built on it resolve normally. Previously a dash was treated as an unreadable amount, and the business's **Gross income** — and every total that sums over it — showed as `—`.
- **A line Glade cannot read is withheld rather than guessed at.** Where a row cannot be resolved — no amount on it, a figure whose sign or units cannot be determined, or a row that does not fall under any category — the 8a lines that row would have contributed to are held back instead of publishing a total that is short by the unreadable amount. The lines that did resolve still publish, and the reason a line was withheld is recorded against the statement.
- **Some placements are a judgment, and are flagged for review.** Where mapping an accounting category onto a line of the form is a decision rather than a rule — depreciation, cost of services, contract labor and advertising are the recurring ones — the placement is marked for an attorney to confirm rather than being applied silently.
- **A business with no statement, or a statement whose period cannot be determined, contributes nothing rather than a zero.** A zero would read as a business that earned nothing, which is a different claim from one whose figures are not in yet.

### Correcting and deleting statements

- **Correcting a statement updates Schedule I straight away.** Edit the statement's recorded values — or delete a statement that should not be counted — and the monthly figures follow on their own. Previously nothing watched these values: the organizer's own panel read correctly while the questionnaire kept serving the earlier figures until someone happened to open the calculator.
- **Deleting the uploaded file removes its figures.** Deleting a profit & loss statement's file from the document checklist removes the statement and its lines, and Schedule I line 8a recalculates without it. Restoring the file brings the statement back. An organizer that is already open updates line 8a on its own after a delete or restore — there is no need to reload the page. Previously the file disappeared from the checklist while its figures stayed on the income table and on line 8a, with nothing that would remove them.
- **Deleting a business takes its statements with it.** Removing a business or its income source removes the statements bound to it, and restoring the business brings back only the statements that went with it — a statement your team had deleted on its own stays deleted.
- **The figures survive re-opening the workflow.** Once a statement has produced business income, opening the case again no longer resets Schedule I line 8a and the means test's business lines. Previously the figures showed correctly until the next time the workflow was loaded, when they fell back to zero with nothing on screen to explain it.

### Statements recorded before line-by-line storage

**Statements recorded before this change were converted.** An existing profit & loss statement keeps the line 8a figures it already produced — nothing has to be re-entered. Because the conversion had to place lines the newer model has no direct equivalent for, re-check line 8a on a case whose figures matter before relying on them.

> TODO: Confirm where profit & loss statements are uploaded from and where the parsed statement is reviewed and corrected, so those steps can be documented here.

## Edge Cases & Limitations

- Business and rental sources that were on a case before profit & loss statements were supported are brought across by a one-off setup Glade runs. Contact Glade if an older source has no place to upload its statements.
- Statements read before dashes were treated as zero keep showing `—` on the affected line 8a figures until the statement is re-read. Re-run extraction on a statement whose gross income shows `—` because of a dashed line.
- A profit & loss statement dropped into a paystub slot rather than onto a business or rental source settles as a row with no extracted data — see [Upload Processing Status](../processing-status.md).

## Related Features

- [Business and Rental Income](./README.md)
- [Schedule I Line 8a](./schedule-i-line-8a.md)
- [Matching Statements to Businesses](./matching-statements-to-businesses.md)
- [Adding Business and Rental Sources](./adding-business-sources.md)
- [Income Organizer](../README.md)
