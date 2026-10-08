# Chapter 13 Plan Claims

## Overview

The Chapter 13 plan builds its list of claims from the creditors on the case's Bankruptcy Schedules questionnaire. This page covers which questionnaire the plan reads and how creditors marked as duplicates are kept off the plan.

## Key Behaviors

### Duplicate creditors are left off the plan

- **A creditor marked as a duplicate on the Master Creditor List does not become a claim.** Only the creditor it was linked to stays on the plan, so each creditor is listed once. This applies to the draft plan preview, to finalizing, and to the claims list in the calculator.
- These are the same rows the Master Creditor List hides as duplicates. See [Creditor Duplicate Status](./creditors.md#creditor-duplicate-status).
- Previously a linked duplicate could still become its own claim, sometimes with a different amount, so the same bank could appear twice on the plan.

### The plan reads the questionnaire the calculator uses

- **The plan uses the same Bankruptcy Schedules questionnaire as the calculator.** Your claim treatments and overrides belong to that questionnaire's creditors, so the plan has to read the same one.
- Previously, a case with a second, hidden Bankruptcy Schedules questionnaire could have the plan read the hidden copy instead. This could happen when someone opened the Schedules card before its step was sent. None of your treatments matched that copy, so every creditor table on the plan form printed empty. The draft preview, the finalized plan, and the collateral details on the plan were all affected.
- For a draft saved before this change, the plan uses the questionnaire attached to a workflow step, the same way the calculator picks it, before falling back to the most recently updated one.

## Edge Cases & Limitations

- **Draft plans pick up these corrections the next time they load.** A plan that was already finalized keeps the output from its last finalize until it is finalized again. Re-finalize any plan that listed a creditor twice or printed empty creditor tables.

## Related Features

- [Chapter 13 Plan Calculator](./chapter-13-plan-calculator.md)
- [Chapter 13 Attorney Fees](./chapter-13-attorney-fees.md)
- [Creditors](./creditors.md)
- [Creditor Deduplication](./creditor-deduplication.md)
