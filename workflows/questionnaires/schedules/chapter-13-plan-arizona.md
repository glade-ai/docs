# Chapter 13 Plan — District of Arizona

## Overview

District of Arizona cases can generate a Chapter 13 plan from the [Chapter 13 Plan Calculator](./chapter-13-plan-calculator.md) on the district's Local Form 2084-4 (5/26), which the court requires for cases filed on or after June 1, 2026. This is a local court form with its own sections (A) through (J), not Official Form 113. This page covers how the generated plan fills the form and what attorneys and paralegals need to check by hand before filing.

## Key Behaviors

- **Same terms as the other plan-generation districts.** The form is available from the calculator, the plan is built from the district's recorded figures, and there is no per-firm setting to switch on.
- **Claim placement:**
  - Long-term claims the debtor pays directly with no cure go in (C)(4)(b). Everything the trustee pays or cures goes in (C)(4)(c), with the cure on its claim's row.
  - A conduit mortgage with no arrears prints $0 rather than a blank.
  - Lien avoidance that strips a mortgage goes in (C)(4)(a). Every other avoided lien goes in (C)(5)(c), with the § 522(f) worksheet printed as the form's narrative.
- **Plan summary (I).** Each line totals what the trustee pays on it, and lines (1)–(7) add up to line (8).
- **§ 1325 analysis (J).** Line (J)(1)(a) prints the non-exempt equity and (J)(1)(c) the hypothetical Chapter 7 trustee fee, both as saved in the calculator. (J)(1)(c) is left blank rather than $0 when no Chapter 7 trustee fee is deducted.
- **Arrearage "owed through" dates.** In (C)(3)(a) and (C)(4)(c), a prepetition arrearage is shown as owed through the case's filing date. Until the case has a filing date on record — an original plan is usually generated before filing — the cell reads "Petition date" in words. A $0 arrearage shows no date. Previously these cells always printed blank with a warning.
- **Commitment period** comes from the means test, not the plan term: 60 months for an above-median debtor and 36 months for a below-median debtor (§ 1325(b)(4)), unless a period is stated on the plan. A below-median debtor on a 60-month plan therefore prints 36. With no means test on the case, the period prints blank with a warning rather than a guessed figure.
- **Attorney fee box.** When no fee election is made, the plan ticks the box Local Rule 2084-3(b)(2) calls for: the flat fee when the attorney fee is at or under the no-look cap, and a fee application when it is above. An election you make still wins. A warning is raised when the flat fee is elected for a fee above the cap, and for any flat fee above the rule's $5,500. Previously neither box was ticked when no election was made.
- **Vesting (E).** With no vesting election, the plan shows property vesting in the debtor on confirmation, as section (E) itself provides. Only an "other" election with no text still warns.
- **A real-property claim the debtor pays directly prints in (C)(4).** A claim on "Secured, paid by debtor" whose collateral is real property — for example a homeowners' association — prints in (C)(4)(b) with no cure, or (C)(4)(c) with a cure. A cure is counted on line (I)(4)(b) and warns like any directly paid cure. The claim's real-property box is pre-ticked from the linked Schedule A/B property. Previously such a claim was left off the plan, and its warning did not say a claim was missing.
- **Every claim table** repeats one row per claim, and prints the court's blank row when it has none.

## Configuration

There is no per-firm setting. The district's recorded figures include a $4,500 no-look attorney fee cap (LR 2084-3(b)(2)), a deduction for the hypothetical Chapter 7 trustee fee, and pro-rata payment with interest on secured claims in (C)(5)(a).

## Edge Cases & Limitations

Parts the form has no source for, or no place for, print blank with a warning rather than being guessed. Check these before filing:

- the commitment period, when the case has no means test;
- the (C)(5)(b) valuation method;
- a secured claim the debtor pays directly that is not on real property — it is left off the plan, and the warning says so and how to list it;
- a cure without a conduit (LR 2084-4(b));
- a (C)(5)(c) lien avoided only in part — the form says the remainder "will be paid in full as a secured claim under the plan", but the plan does not pay it;
- a "wholly unsecured" (C)(4)(a) mortgage that still has a secured remainder.

Other limits:

- (C)(2)(b) additional services, (C)(2)(c), the (C)(5)(a) codebtor block, and the "Nonstandard Provisions. See Section (H)." boxes are not recorded in Glade and print as the court's blanks.
- A plan whose calculator figures were saved before Arizona was added has no non-exempt equity or Chapter 7 trustee fee saved, so (J)(1)(a) and (c) print blank with a warning. Re-save the calculator to fill them.

- Nothing in the plan records that the debtor is a business, so the no-look cap does not rise on its own for a business case. Set the plan's fee cap to $5,500 yourself for a business debtor.
- Plans already generated are not changed; regenerate a plan to pick up these defaults.

> TODO: Confirm where the real-property box for a directly paid secured claim appears in the plan calculator, and that Form Details shows the Arizona defaults above.

> TODO: Confirm the District of Arizona's recorded trustee fee percentage before firms rely on a generated plan.

## Related Features

- [Chapter 13 Plan Districts](./chapter-13-plan-districts.md)
- [Chapter 13 Plan Calculator](./chapter-13-plan-calculator.md)
- [Schedule Tools](./README.md)
- [Chapter 13 Plan Status](../../../integrations/efiling/filing-packet/chapter-13-plan-status.md)
