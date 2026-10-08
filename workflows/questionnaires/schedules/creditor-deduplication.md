# Creditor Deduplication

## Overview

Glade automatically links creditor rows that are the same debt, so a creditor that comes in from both the credit report and the client's answers is listed once on the schedules and the creditor matrix. The linked copy is marked as a duplicate of the row that stays. This page covers when deduplication runs, which rows it links, and which row it keeps.

## Key Behaviors

### When it runs

- On the case record, deduplication runs when a credit report is imported and when a questionnaire is completed. It also runs when someone clicks **Remove duplicates**.
- On a questionnaire, it runs when the questionnaire is created and when someone clicks **Run Deduplicator** on a creditor list.
- Both use the same rules, so the case record and the questionnaire agree.
- **Links are worked out again on every run.** A change to the rules applies to a case's existing links the next time deduplication runs on it.

### Which rows are linked

The guiding rule is that **no debt should be lost**. A wrong link takes a debt off Schedules D and E/F and off the creditor matrix, so that creditor never gets notice. When the rules can't be sure, they leave the rows separate.

- **Same account number:** linked when the claims are within $100 of each other. Spaces and dashes don't matter, so `4147 2020 1234 5678` and `4147-2020-1234-5678` are the same number.
- **Same account number, one claim missing:** linked when the creditor names match.
- **Neither row has an account number:** linked when the creditor names match and, where both rows have a claim, the claims are within $1. A row with no claim still links on the name alone. Placeholders such as `N/A`, `UNKNOWN`, `NONE` or `0000` count as no account number.
- **Not linked by the rules:**
  - two rows that show only the same masked number, such as `XXXX5678` on both;
  - a row with an account number and a row without one;
  - a masked number and a full number.
- **Two different accounts are never put in one group.** A masked or shortened number has to agree with every digit it shows. `XXXX5678` or `5678` can join a group with the full number ending in 5678. `XXXX1234`, or a number one digit off, never can.
- **Claims are checked across the whole group, not just each pair.** A row with no account number or no claim can't join two rows that don't match each other. For example, a client row "Dept of Education, $3,500" no longer merges two separate loans. A chain of same-number rows whose amounts drift more than $100 from one end to the other ($500, $580, $660) is split where the tolerance breaks.

### Which row is kept

The row that stays on the schedules is the one that can best stand for the debt:

1. the row with the most complete account number (a full number, then a masked number that still shows the last digits, then none);
2. then a row that has a claim amount;
3. then the row that comes first in the list.

Previously a client row with no balance could be kept over the credit report's row and hide the amount.

## Edge Cases & Limitations

- **Some existing groups may come apart.** Two rows with the same name, no account numbers, and claims more than $1 apart are now treated as different debts. Two Department of Education loans of $3,500 and $5,500, for example, are no longer merged. Firms will see these rows come back as separate creditors the next time deduplication runs.
- **Some near-duplicates still need a person.** Rows that differ in how the name or address is written ("DFCU" and "Dearborn Federal Credit Union"), or where only one row has the account number, are not linked by the rules. Mark them as duplicates by hand. See [Creditor Duplicate Status](./creditors.md#creditor-duplicate-status).
- **Stale links are cleared.** A questionnaire whose only duplicate group no longer qualifies has its links removed. Previously those links could stay behind.
- Short account numbers that are identical (for example `1234` on both rows) still link on matching claims alone.

## Related Features

- [Creditors](./creditors.md)
- [Working With Lists](../filling-out/working-with-lists.md)
- [Chapter 13 Plan Claims](./chapter-13-plan-claims.md)
- [Duplicate Creditors check](../../../integrations/efiling/pre-filing-review/duplicate-creditors.md)
- [Importing Creditors from a Credit Report](../../../intake/credit-reports/importing-creditors.md)
