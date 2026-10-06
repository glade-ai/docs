# Chapter 13 Attorney Fees

## Overview

A generated Chapter 13 plan pays the debtor's attorney through the trustee. This page covers how much of the attorney fee the plan pays when part of it was paid before filing, and the extra attorney fees the Middle District of Florida plan supports: the mortgage modification mediation (MMM) fee and the monitoring fee.

## Key Behaviors

### The plan pays the balance, not the full fee

- **The attorney's payment through the plan is the fee minus what was paid before filing.** If the fee is $2,700 and $1,000 was paid prepetition, the plan pays the attorney $1,700. If the prepaid amount covers the whole fee, the plan pays the attorney nothing. It never goes below zero.
- Previously generated plans paid the full fee, while the calculator paid the balance. A plan could print "Balance Due $1,700" and still schedule $2,700 to the attorney, and the extra $1,000 came out of what other creditors received.
- **What prints on the form:**
  - Forms that print the amount paid to the attorney through the plan now show the balance.
  - Forms that print the fee, the amount paid before filing, and the balance due (such as the Middle District of Florida's Section C.1) are unchanged.
  - The **Western District of Washington** plan asks for the *total* fee estimate in Section IV.A.3, so that line prints the balance plus the prepaid amount.

### Middle District of Florida: MMM and monitoring fees

The Middle District of Florida calculator has fields for two more attorney fees. Each one is paid through the plan as its own payment, at the same priority as attorney fees, and is left off when it comes to zero.

- **MMM fee.** Enter the mortgage modification mediation fee and the amount paid before filing. The plan pays the unpaid balance. Section C.1 prints the MMM fee, the total paid prepetition, and the balance due. All three print blank when there is no MMM fee.
- **Monitoring fee.** Enter the monthly fee and the number of whole months to deduct (zero or more). The plan pays the monthly fee for every month of the plan term except the deducted months. For example, $50 a month over a 36-month plan with no deduction pays $1,800. Section C.1's "Estimated Monitoring Fee at $___ per Month" prints the monthly figure only. The total over the plan is not printed.
- **The attorney fee line stays separate.** "Attorney's Fees Payable Through Plan" on Section C.1 still shows the attorney fee alone. The MMM and monitoring fees are not added to it.

## Configuration

| Setting | Description |
|---------|-------------|
| Attorney fee | The total fee for the case |
| Amount paid prepetition | What counsel received before filing. The plan pays the fee minus this amount |
| MMM fee and amount paid (Middle District of Florida only) | The plan pays the unpaid balance |
| Monitoring fee per month and months deducted (Middle District of Florida only) | The plan pays the monthly fee for the plan term less the deducted months |

## Edge Cases & Limitations

- **Plans in progress may change.** A plan that already has a prepaid amount now pays the attorney that much less through the trustee. This affects plans in the Northern District of Florida, the Northern and Western Districts of Texas, the Eastern District of Kentucky, the Northern District of Alabama, the District of South Carolina, the District of Colorado, the Eastern District of Washington, and the Southern District of Illinois. Check the attorney fee on any plan you are still working on in these districts.
- The MMM and monitoring fee fields appear only in the Middle District of Florida calculator. Other districts are unaffected.

> TODO: Confirm whether a plan that was already finalized keeps paying the full fee until it is finalized again, or whether reopening it applies the balance immediately.

## Related Features

- [Chapter 13 Plan Calculator](./chapter-13-plan-calculator.md)
- [Chapter 13 Plan Districts](./chapter-13-plan-districts.md)
- [Chapter 13 Plan Claims](./chapter-13-plan-claims.md)
