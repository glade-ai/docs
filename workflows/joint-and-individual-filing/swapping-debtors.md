# Swapping Debtors

## Overview

On a joint case, the debtor swap trades the two debtors' roles, so the person entered as Debtor 1 (the primary) becomes Debtor 2 (the spouse) and the other way around. Staff use it when the debtors were entered in the wrong order. The swap moves each debtor's information to the other role on the case record and on the Bankruptcy Schedules questionnaire, rather than requiring it to be retyped.

## Key Behaviors

- **Run from the workflow's settings** with **Swap primary and spouse**. A confirmation dialog lists anything to be aware of before you confirm.
- **Each debtor's information moves with them.** Answers recorded for Debtor 1 move to Debtor 2 and the reverse — on the case record and on the schedules questionnaire, including questionnaires that have already been submitted.
- **Every part of a debtor's row moves.** On the schedules, the swap moves all of a debtor's answers, wherever they sit:
  - paired Debtor 1 and Debtor 2 lists, such as each debtor's other names (AKAs), move row by row, including answers nested under an explanation within a row;
  - tables with one entry per debtor, such as the Schedule I income table, trade their entries between the debtors, nested answers included;
  - Debtor 1 and Debtor 2 columns inside a list trade their values.

  Previously answers nested under an explanation inside a list or table were left behind: they stayed attached to the original debtor, or were not swapped at all.
- **Shown and hidden questions are re-evaluated after the swap.** Questions whose visibility depends on a swapped answer, and answers that moved into the other debtor's column, are shown or hidden according to their new position straight away. Previously a question could stay hidden or shown according to the pre-swap answers until the questionnaire was next saved.
- **Answers about the debtors together are kept.** Petition answers that describe the case as a whole — such as prior bankruptcies and the estimated number of creditors — stay as they are rather than being cleared.
- **Warnings before you confirm:**
  - when the debtors' names on the case record already appear to be under the opposite roles — for example, because names were swapped by hand on the schedules while other details were not. The swap moves everything as it stands, so it carries that mismatch across rather than fixing it;
  - when the case is part of a group of linked workflows. The swap applies to the workflow you run it from.

## Edge Cases & Limitations

- A swap cannot run while a conversion between joint and individual filing is in progress on the case, and the reverse.
- **A swap is refused when a paired Debtor 1 / Debtor 2 list contains a list of its own inside each row**, because moving the rows would separate the inner list's entries from their row. Where a per-debtor table contains a nested list, that list is left in place and the swap reports it.
- **Some calculated figures can keep their pre-swap value.** A calculated answer that reads a Debtor 1 input with no Debtor 2 counterpart is not recalculated by the swap. Check calculated totals after swapping.
- The swap cannot tell a deliberate hand correction from correct data. Fix names typed into the wrong role by hand before swapping, or the swap carries the error to the other debtor.

> TODO: Confirm whether the swap is offered only on joint workflows, whether it is blocked once a case is filed, and what is shown when a swap cannot run.

## Related Features

- [Joint and Individual Filing](./README.md)
- [Converting Between Joint and Individual Filing](./converting-filing-type.md)
- [Case Data Sync](../questionnaires/case-data/case-data-sync.md)
- [Conditional Visibility](../questionnaires/templates/conditional-visibility.md)
