# Chapter 13 Plan Districts

## Overview

The [Chapter 13 Plan Calculator](./chapter-13-plan-calculator.md) generates a plan on the district's own local plan form for the districts listed here. For each district, this page notes which form is used and the parts of that form the calculator does not fill in or cannot decide for you, so attorneys and paralegals know what to check before filing.

## Key Behaviors

- **Northern District of Ohio** cases can generate a Chapter 13 plan. The district's plan form is available from the calculator, and the generated plan is built from the district's own figures — the trustee fee percentage, the no-look attorney fee cap, and the applicable interest rate — in the same way as other plan-generation districts. There is no per-firm setting to switch on.
- **Western District of Washington** cases can generate a Chapter 13 plan on the district's Local Bankruptcy Form 13-4. It works the same way as the other plan-generation districts: the form is available from the calculator, the plan is built from the district's own recorded figures, and there is no per-firm setting to switch on. Cases in this district previously reported that plan generation was not available for them.
- **Eastern District of Washington** cases can generate a Chapter 13 plan on the district's Local Form 2083. As with the other plan-generation districts, the form is available from the calculator and there is no per-firm setting to switch on. Two points need checking by hand on this district's form until they are resolved:
  - **A contract the debtor is assuming but paying directly has nowhere correct to go.** Local Form 2083 pays assumed contracts through the trustee, and the form treats a contract not listed as assumed as rejected — whether or not it appears anywhere else on the plan. Choosing to assume a contract while paying it outside the plan therefore does not say what you mean on this form. Review any such contract before filing.
  - The district's **no-look attorney fee cap and trustee fee percentage** are still the national defaults rather than figures recorded for this district. The fee cap prints on the plan and is what the plan's attorney-fee section is checked against, so confirm both before relying on a generated plan.
- **District of Colorado** cases can generate a Chapter 13 plan on the district's Local Bankruptcy Form 3015-1.1, on the same terms — available from the calculator, built from the district's own recorded figures, with no per-firm setting to switch on. Colorado's plan form has sections the calculator does not work out for you; fill those in from the plan calculator's own inputs before finalizing, as they print blank otherwise.
- **Eastern District of Louisiana** cases can generate a Chapter 13 plan on the district's Model Plan — a local court form rather than Official Form 113. It works the same way as the other plan-generation districts: the form is available from the calculator, the plan is built from the district's own recorded figures, and there is no per-firm setting to switch on.
- **Southern District of Illinois** cases can generate a Chapter 13 plan on the district's Uniform Chapter 13 Plan, on the same terms as the other plan-generation districts. Parts of the form Glade has no source for print blank with a warning so you fill them in by hand — for example, every domestic support obligation prints in §7A, and one owed to a government unit has to be moved to §7B by hand.
- **Southern District of Florida** cases can generate a Chapter 13 plan on the district's Local Form LF-31, on the same terms. Parts the calculator does not work out print blank with a warning rather than being guessed: creditor addresses and account numbers, which valued items are vehicles (valued personal property is listed together, and vehicles need moving to their own part by hand), the principal residence, student loans, the stay-relief box, the tax-return provision where the case's division is unknown, the attorney fee when it has not been entered, and the amendment number.
- **Central District of California** cases can generate a Chapter 13 plan on the district's mandatory form F 3015-1.01 (Chapter 13 Plan), reproduced word for word across the form's 16 pages. It works on the same terms as the other plan-generation districts: the form is available from the calculator and there is no per-firm setting to switch on. Where the plan depends on a judgment the calculator cannot make, it prints its best reading and raises a warning for you to check before filing:
  - long-term secured claims on real property are placed in Class 2 on the assumption that the property is the principal residence;
  - the Section I.B election on how much unsecured creditors receive;
  - a lien-avoidance claim whose kind of lien has not been set, which decides whether it prints in Section IV.A with Attachment A or in Section IV.B;
  - an arrearage cure sitting under a Class 3 claim;
  - trustee payments the plan's funding does not cover;
  - creditors with no account number;
  - a Class 5C special-class claim that the plan does not fund.
- **Middle District of Florida** cases can generate a Chapter 13 plan on the district's Chapter 13 Model Plan. As with the other plan-generation districts, the form is available from the calculator, the plan is built from the district's own recorded figures, and there is no per-firm setting to switch on. Two points need checking by hand on this district's form:
  - The Section A notices for **student loans** and for **reinstating an amended automatic stay** always print as "Not Included", because Glade does not yet have a source for either answer. The calculator raises a warning on every plan so you can check both notices yourself before filing.
  - Sections **C.5(c)** and **C.5(k)** have no claim treatments assigned to them yet, so those tables print empty on the generated plan.

## Configuration

There is no per-firm setting. A case can generate a plan when its district is on the list above; the district is taken from the case.

## Edge Cases & Limitations

- Sections a district's form asks for that the calculator does not work out print blank, usually with a warning, and must be completed by hand before filing.
- District figures such as the trustee fee percentage and the no-look attorney fee cap are recorded per district. Where a district was switched on before its own figures were confirmed, the entry above says so — check those figures before relying on a generated plan.

> TODO: Confirm the trustee name, no-look attorney fee cap, and trustee fee percentage recorded for the Southern District of Illinois and the Southern District of Florida. Both districts were switched on while those figures were still flagged for confirmation.

> TODO: Confirm the Central District of California's recorded trustee fee percentage and no-look attorney fee cap. The district was switched on while those figures were still the national defaults (a 10% trustee fee against the 11% the district's form states).

> TODO: Confirm the Eastern District of Washington's actual no-look attorney fee cap and trustee fee percentage once the district's own figures are recorded, and remove the caveat above.

> TODO: Confirm which claim treatments belong in §7.2.c of the Eastern District of Louisiana Model Plan. The section was switched on with no treatments assigned to it, so a claim that belongs there may not print on the generated plan.

> TODO: Confirm the Western District of Washington's recorded no-look attorney fee cap and trustee fee percentage before firms rely on a generated plan — these were still carrying placeholder values when the district was switched on, and the fee cap prints on the plan itself.

## Related Features

- [Chapter 13 Plan Calculator](./chapter-13-plan-calculator.md)
- [Schedule Tools](./README.md)
- [Chapter 13 Plan Status](../../../integrations/efiling/filing-packet/chapter-13-plan-status.md)
- [PACER](../../../integrations/pacer/README.md)
