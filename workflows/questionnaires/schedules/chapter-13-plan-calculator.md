# Chapter 13 Plan Calculator

## Overview

On Chapter 13 questionnaires, a **Plan Calculator** button appears in the questionnaire header toolbar. Clicking it opens the Chapter 13 Plan Calculator in a new tab alongside the questionnaire, pre-loaded with the current case. The calculator uses case data to help attorneys model plan payments, trustee fees, creditor treatments, and liquidation analysis, classify claims, and prepare the repayment plan without leaving the questionnaire workflow.

## Key Behaviors

### Opening the calculator

The Plan Calculator button only appears on questionnaires identified as Chapter 13. If the button is not visible on a Chapter 13 questionnaire, contact support to confirm the feature is enabled for your firm.

> TODO: Confirm exact tab behavior and whether feature-flag gating is still in place once the calculator is fully released.

### Plan Elections

Some entries on the Chapter 13 plan are choices the calculator does not compute for you. You set these directly in the calculator, and they appear on the generated plan:

- **Vesting of estate property** — when property of the estate vests back in the debtor (for example, at plan confirmation or at discharge).
- **Plan payment method** — how the debtor makes plan payments to the trustee.
- **Tax-refund treatment** — how the debtor's tax refunds are handled during the plan.
- **Amended sections** — the list of plan sections being amended, when you are filing an amended plan.

Each election offers the standard choices plus an **Other** option with a free-text box for anything outside the preset list. These elections are optional — a plan with one left blank still generates, and the calculator flags any blank election so you can fill it before filing. If the list of amended sections is longer than the space on the form, the calculator warns you that it will not all fit.

On the **Northern District of Ohio** plan, an unanswered plan payment method is now flagged the same way it already was on the Northern District of Georgia plan. Previously that section printed blank with no warning at all, so a plan could go out with no payment method elected and nothing to indicate it. An **Other** election whose description is left empty is treated as unanswered and raises the same warning, since a blank "Other" prints identically to no election. Choosing payroll deduction, direct payment, or **Other** with a description clears the warning. The unanswered election also appears in the plan's completeness report.

### Lump-Sum Payments

Alongside the regular monthly plan payment, you can schedule one-time lump-sum contributions to the trustee — a tax refund, a bonus, or the proceeds of a sale, for example. Each entry records:

- The **amount** of the payment.
- The **date** the payment is anticipated, as a calendar date.
- A short **description** of where the money comes from, so the plan says what the payment is.

How lump sums are used:

- They count toward the plan's total funding, its payment schedule, and the trustee fee. The figures on a finalized plan match what the calculator shows, so the printed plan and the calculator no longer disagree about total funding.
- On the Northern District of Georgia plan, each lump sum prints on the "additional payments to the trustee" line as the amount, the date, and the description — for example, `$4,500 on 10/15/2026 (tax refund)`. The description is left off when you have not entered one. Entries print in date order, earliest first.
- That section of the form has room for two lines. If you enter more lump sums than fit, the calculator warns you that they will not all print.
- An entry with no amount, or with a date before the plan's start date, is left off the plan.
- Lump sums recorded before dates and descriptions were available still print in their original form, showing the amount and the plan month it falls in rather than a calendar date.

### Amounts Promised to Unsecured Creditors

The plan's general-unsecured section states a minimum the plan will pay to unsecured creditors. That figure now prints the amount the plan actually delivers to unsecured creditors after every other treatment is funded, rather than the ceiling your firm set on the unsecured pool.

- Previously the printed figure was the pool ceiling. On a plan whose funding does not reach that ceiling, the form promised more than the plan pays — a plan paying $11,700 to unsecured creditors could print "at least $50,000".
- The two figures are the same on a plan funded to the ceiling, so plans that were fully funded are unchanged.
- This applies to both the Northern District of Georgia and Northern District of Ohio plans.

If your firm filed a plan with an unsecured pool ceiling set on it before this correction, check the stated minimum against what the plan actually pays.

**A plan that pays nothing to unsecured creditors states the plain remainder.** On the Northern District of Georgia plan, the general-unsecured section offers two elections: pay whatever funds remain, or pay the larger of a stated dollar figure and the funds remaining. Where your firm has set a ceiling on the unsecured pool and nothing actually reaches general unsecured creditors, the plan now takes the first election.

- Previously setting any ceiling took the second election regardless of amount, so a plan delivering nothing to the pool printed a promise to pay "the larger of the sum of $0.00 and the funds remaining" — a statement that says nothing and reads as an unfinished form.
- This covers both ways the pool can come to nothing: a ceiling entered as $0, and a positive ceiling that the plan's funding never reaches.
- Plans that do deliver a positive amount to unsecured creditors are unchanged and keep the stated-figure election.

This affects the Northern District of Georgia plan only.

#### Unsecured Creditor Pool on the Ohio Northern Plan

The unsecured creditors section of the Northern District of Ohio plan shows one figure, not two:

- If you have entered a pool amount by hand, that amount is used and the liquidation minimum is not also shown. Your entry takes priority.
- If you have not entered one, the liquidation minimum — the amount unsecured creditors would receive in a Chapter 7 liquidation — is shown as the reference figure.

Previously both could appear, which left the plan stating a minimum that your manual figure was meant to replace.

### Lien Avoidance and Collateral Value

When a secured claim is treated as a lien avoidance, the plan's lien-avoidance worksheet and the secured amount the plan schedules for that creditor now use the same numbers.

- Glade derives the claim's collateral value from the worksheet entries you fill in — the lien amount, other liens against the property, the exemption claimed, and the property's value — using the same impairment test the worksheet itself applies.
- Previously the worksheet and the plan's secured split were computed from separate inputs, so a worksheet showing a lien as fully avoided could sit alongside a plan that still scheduled a secured payment to that creditor.
- A collateral value you enter directly as an override still wins over the value derived from the worksheet.

### Secured Claims With an Arrearage Cure

When a secured creditor — for example a mortgage servicer — is both maintained going forward and has past-due arrears to cure, the generated plan lists that creditor as a **single line** in the secured-claims section. The ongoing payment and the arrearage cure amount appear together on that one line rather than as two separate rows for the same creditor.

- You can set the arrearage cure's own **first and last payment months** — the months the cure payments start and stop — separately from the ongoing payment. When you set these in the calculator, they carry through to the generated plan.
- Clearing an override field back to blank — collateral value, contract payment, or interest rate — restores the value from the questionnaire for that creditor rather than leaving it empty, so a cleared field no longer wipes the underlying figure.
- On the **Northern District of Ohio** plan form, the ongoing installment and the arrearage cure are combined onto one line per creditor, as that district's form requires. The arrearage amount, its interest rate, and the monthly cure payment all appear on the creditor's own line, and no separate arrearage row is listed. The **current installment** on that line is the payment from the plan's payout schedule rather than the contract payment, so it reflects what the plan actually pays. The trustee-payments exhibit continues to count both the ongoing payment and the cure.
- On the **Northern District of Georgia** plan form, a claim with an arrearage prints **once** in §3.1, as its cure row — the creditor name followed by "(arrearage)", with the arrearage amount, interest rate, and monthly cure payment. Previously the same creditor could also print on a second row with a blank arrearage and a monthly payment that did not belong there. A claim with no arrears prints on its own row as before.
- **Long-term secured claims paid outside the plan now print in §3.1 of the Northern District of Georgia plan.** A claim treated as "Secured, long term, outside plan" — a mortgage or HUD lien the debtor pays directly, for example — previously appeared nowhere on that district's plan form, whatever its arrears. It now appears in §3.1 with its arrearage amount, including an arrearage of $0, and does not appear in §3.6. Regenerate the plan on any Northern District of Georgia case where such a claim was missing.

### Generated Plan Document

When you finalize a Chapter 13 plan, Glade regenerates the plan PDF and stores it, so the workflow's Documents tab reflects the version you just finalized instead of an out-of-date copy.

- Every finalized version of the plan is kept in the Documents tab as chronological version history. The most recent version is the one used for court filing; earlier versions stay available for reference rather than being replaced.
- All finalized versions appear together under a single **Chapter 13 Plans** folder, listed as individual files. Each version is no longer split out into its own separate folder, so you can see the full version history of the plan in one place.
- Interest rates on the generated plan display as percentages — for example, a 9% rate prints as `9.00%` rather than `0.09%`.
- A claim whose treatment does not carry interest — a pro-rata secured treatment, for example — prints a blank interest rate rather than a figure. On the Northern District of Ohio plan form, changing a claim to one of these treatments used to leave the rate from the treatment you selected before it sitting in the §3.2 and §3.3 rate cells, so the plan showed an interest rate for a claim that pays none.
- **The interest rate printed is the rate the plan pays.** On the Northern District of Georgia, Middle District of Florida, Eastern District of Louisiana, and Southern District of Illinois plans, each claim's interest rate column now shows the rate its treatment is calculated at: a cramdown prints the district's Till rate (or the Till rate you set on the plan), a priority tax claim prints the §511 rate, and a pro-rata claim prints blank. Previously these columns printed the claim's contract rate whatever the treatment, so a plan could state a rate its payments were not calculated at. Claims paid at the contract rate print as before. Regenerate any plan in these districts that has a cramdown or priority tax claim.
- **Dollar signs come from the value, not the form.** A money entry that holds a number prints with a dollar sign — `$1,234`. A money entry you have **overridden with text** prints exactly the text you typed, so `TBD` prints as `TBD` rather than `$TBD`. A money entry with no value at all prints as an empty cell rather than a lone `$`.
- Every amount in the plan's payment schedule carries a dollar sign, including the first one. Previously the first amount in a schedule printed bare while the rest were marked.
- **The purchase date prints beside the collateral in §3.2 of the Northern District of Georgia plan.** That section's column is headed "Collateral and date of purchase", so each row now reads as the collateral description followed by the purchase date entered on the claim — for example, `Bedding 05/01/2022`. Previously only the collateral description printed. A claim with no purchase date prints the description alone, and §3.3, which has its own purchase-date column, is unchanged.
- District and court-level figures are locked to the version you finalized. The values the plan is built from — the no-look attorney fee cap, the filing fee, the trustee's name, the prime rate and other applicable rates — are recorded with each finalized version. If the district later changes one of those figures, re-opening or regenerating an already-finalized plan still shows the figures that were in effect when you finalized it, so a filed plan does not silently change after the fact. Any per-case adjustments you entered by hand are kept with the version as well and continue to apply.
- Versions finalized after a district change pick up the new figures. When you start the next version of a plan, it tracks the district's current values rather than inheriting the locked figures from the previous version. An amended plan therefore reflects the figures in effect at the moment you finalize it.

### Plan-Generation Districts

Chapter 13 plans can be generated on the local plan forms of a growing list of districts. The districts, and the parts of each form that need checking by hand, are listed in [Chapter 13 Plan Districts](./chapter-13-plan-districts.md).

### Plan Form Explanation

The plan preview's **Explanation** view describes what each field on the plan form means. Those descriptions are grouped under a heading for each part of the plan document — the case caption, then each numbered part, and the trustee-payments exhibit where the district's form has one — so you can collapse the parts you are not working on and find the field you are looking at. Previously every description arrived as one unbroken list under a single heading.

- Grouping is available on the plan forms for the **Northern District of Georgia** and the **Northern District of Ohio**.
- Only parts of the form that have mapped fields get a heading. A part that is fixed text with nothing to fill in — for example vesting on the Northern District of Georgia form — has no heading rather than an empty one.

## Edge Cases & Limitations

- Several district forms have sections the calculator does not fill; these print blank (usually with a warning) and must be completed by hand before filing. See [Chapter 13 Plan Districts](./chapter-13-plan-districts.md).
- A finalized plan keeps the district figures in effect when it was finalized, even when re-opened or regenerated; only the next version picks up changed figures.

## Related Features

- [Questionnaires](../README.md)
- [Schedule Tools](./README.md)
- [Exemptions Calculator](./exemptions-calculator.md) — equity used in the liquidation analysis
- [Schedule A/B Property](./property.md)
- [Creditors](./creditors.md)
- [Chapter 13 Plan Districts](./chapter-13-plan-districts.md) — which districts can generate a plan, and what to check on each form
- [PACER](../../../integrations/pacer/README.md)
