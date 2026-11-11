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
- **Commitment period** follows the plan term the calculator shows.
- **Every claim table** repeats one row per claim, and prints the court's blank row when it has none.

## Configuration

There is no per-firm setting. The district's recorded figures include a $4,500 no-look attorney fee cap (LR 2084-3(b)(2)), a 10% Chapter 13 trustee fee, a deduction for the hypothetical Chapter 7 trustee fee, and pro-rata payment with interest on secured claims in (C)(5)(a). The plan summary's trustee line uses that 10%.

## Edge Cases & Limitations

Parts the form has no source for, or no place for, print blank with a warning rather than being guessed. Check these before filing:

- the arrearage "through" dates;
- the (C)(5)(b) valuation method;
- a non-mortgage secured claim the debtor pays directly;
- a cure without a conduit (LR 2084-4(b));
- a (C)(5)(c) lien avoided only in part — the form says the remainder "will be paid in full as a secured claim under the plan", but the plan does not pay it;
- a "wholly unsecured" (C)(4)(a) mortgage that still has a secured remainder.

Other limits:

- (C)(2)(b) additional services, (C)(2)(c), the (C)(5)(a) codebtor block, and the "Nonstandard Provisions. See Section (H)." boxes are not recorded in Glade and print as the court's blanks.
- A plan whose calculator figures were saved before Arizona was added has no non-exempt equity or Chapter 7 trustee fee saved, so (J)(1)(a) and (c) print blank with a warning. Re-save the calculator to fill them.

## Related Features

- [Chapter 13 Plan Districts](./chapter-13-plan-districts.md)
- [Chapter 13 Plan Calculator](./chapter-13-plan-calculator.md)
- [Schedule Tools](./README.md)
- [Chapter 13 Plan Status](../../../integrations/efiling/filing-packet/chapter-13-plan-status.md)
