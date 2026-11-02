# Swapping Primary and Spouse

## Overview

On a joint case, **Swap primary and spouse** trades the roles of the two debtors, so the person filed as Debtor 1 becomes Debtor 2 and the other way round. Firm staff use it when the debtors were entered in the wrong order. Before the swap is applied, a confirmation dialog previews what will change.

> TODO: Confirm where **Swap primary and spouse** is opened from on the case, and describe the full preview the confirmation dialog shows.

## Key Behaviors

- **Answers tied to a role move with the role.** Each debtor's details on the case record — names, Social Security numbers, dates of birth, and the other answers kept per debtor — move to the other role. The swap moves what is stored; it cannot tell a deliberate hand edit from correct data.
- **Answers about the debtors together stay put.** Five petition answers are asked of the debtors jointly and remain true when the roles trade, so the swap keeps them:
  - the estimated number of creditors;
  - whether there was a prior bankruptcy;
  - whether there was a court action in the last year;
  - whether property was repossessed in the last year;
  - whether there were previous addresses.

  Previously the swap cleared these five answers and nothing filled them back in, so they were lost from the case.
- **A warning when the names already look reversed.** If the debtors' first names on the case record are already under the opposite roles from the case's primary debtor and spouse — for example because someone retyped the Debtor 1 and Debtor 2 names by hand in the schedules but not the Social Security numbers or dates of birth — the confirmation dialog warns you. Swapping would carry that mismatch across rather than fix it, leaving the names still opposite to the other details.
  - The warning is advisory. You can still confirm the swap.
  - It compares first names only, because joint debtors often share a last name. It stays quiet when either first name is unknown or when the two first names are the same.

## Edge Cases & Limitations

- The swap cannot correct names that were hand-swapped on the case record. Fix the names (or the other details) so they agree before swapping, or after the warning appears.
- Cases swapped before the five joint answers were kept may have lost those answers. Check them on any recently swapped case and re-enter them if they are blank.
- The reversed-names warning does not catch two debtors with the same first name.

## Related Features

- [Case Data](./README.md)
- [Case Data Sync](./case-data-sync.md)
- [Re-opening and Re-syncing](./reopening-and-resync.md)
