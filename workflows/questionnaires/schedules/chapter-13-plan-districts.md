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
- **Eastern District of Kentucky** cases can generate a Chapter 13 plan on the district's Local Form 3015-1(a), *Chapter 13 Plan*, revised 02/25. This is a local court form, not Official Form 113. It works the same way as the other plan-generation districts: you open the form from the calculator, and there is no per-firm setting to switch on. How claims are placed on this form:
  - The form has no separate direct-payment section, so secured claims the debtor pays directly print in §3.1 with the "Disbursed by Debtor(s)" box ticked.
  - Secured claims paid in full go in §3.3. A claim in §3.2 or §3.3 paid without interest prints a rate of 0.00, because the form reads a blank rate as "WSJ Prime + 2".
  - Lien avoidance that strips a mortgage prints in §3.2 as a valuation at $0. Every other lien avoidance goes in §3.4 with the § 522(f) worksheet filled in.
  - The §4.3 attorney fee follows the plan's attorney fee election: (b) when the fee is by application, otherwise (a) with the fee, the amount paid before filing, and the balance. An (a) fee above the district's no-look cap raises a warning.
  - §4.4 prints a single estimate, using the domestic support obligation estimate the attorney entered where there is one. The manual special-class list prints in §5.3. §5.2 always prints "None".
  - Lump sums raise a warning that they belong in Part 8.
- **Northern District of Alabama** cases can generate a Chapter 13 plan on the district's LR 3015-1 A, *Chapter 13 Plan*. This is a local court form, not Official Form 113. You open the form from the calculator, and there is no per-firm setting to switch on. The district's four divisions fill parts of this form differently, so the plan reads the **court division** recorded on the case:
  - **When the fixed monthly payments begin:** left blank in the Northern Division (Huntsville), "Confirmation" in the Eastern Division (Anniston), and "Month N After Confirmation" in the Western Division (Tuscaloosa). The Southern Division (Birmingham), and a case with no division recorded, print the calculator's first payment month.
  - **Priority claims:** print "N/A" for the fixed payment in the Southern Division. In the Northern Division a tax claim takes no fixed payment.
  - **§5.2 (unsecured creditors):** 100% when unsecured creditors are paid in full. Otherwise "Pot" in the Western Division and "Base" in the other divisions. The percentage option is never chosen.
  - Warnings are raised for amounts that are not whole dollars, payments below the $15 floor, a mortgage paid through the trustee in the Northern Division, and a case with no division recorded — set the division on the case before generating the plan.

  How claims are placed on this form:
  - The form has no separate direct-payment section, so secured claims the debtor pays directly print in §3.1. Because §3.1 has the trustee pay every listed arrearage, an arrearage the debtor pays prints its balance with no monthly payment or start date, and raises a warning.
  - Secured claims paid in full go in §3.3. Claims in §3.2 and §3.3 carry their own adequate-protection payment, and a claim paid without interest prints a rate of 0.00.
  - Lien avoidance that strips a mortgage prints in §3.2 as a $0 secured claim. Every other lien avoidance goes in §3.4, as Total Avoidance or on the Partial Avoidance chart (lines a–h). The chart assumes the debtor owns the property alone.
  - §4.3 always ticks the administrative-order box. The manual special-class list prints in §5.5, and rejected contracts in §6.2.

  Parts Glade has no source for print blank, or are left unticked, so check them by hand before filing:
  - the Southern Division's "six months from the petition month" start, which is not worked out — the calculator's first month prints instead;
  - months in arrearage and lease terms, which print blank with a warning;
  - the §4.5 box for a domestic support obligation paid less than in full, and the §5.3 and §5.4 boxes, which are never ticked.

  In the Western Division, the start prints as "Month N After Confirmation" but the monthly amounts are still the calculator's, spread from the first month. Starting later leaves fewer payments, so a claim can come up short of what the plan says it pays. No warning is raised for this — check Western Division plans before filing.
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
- **Northern District of Texas** cases can generate a Chapter 13 plan on the district's local form BTXN222, *Debtor's(s') Chapter 13 Plan (Containing a Motion for Valuation)*, revised 5/12/21. This is a local court form, not Official Form 113. It works the same way as the other plan-generation districts: you open the form from the calculator, and there is no per-firm setting to switch on. How claims are placed on this form:
  - Mortgages go in Part D. Arrearage cures paid through the trustee go in D.(1), unless the cure belongs to a claim listed elsewhere on the plan. A long-term secured claim paid through the trustee goes in D.(2). Secured claims paid in full through the trustee go in Part E, and a cure split off one of those claims prints beside it marked "(arrears)".
  - A Part E claim marked as paid outside the plan prints in Part G (direct payments), not as trustee-paid.
  - Surrendered collateral goes in Part F. Domestic support obligations and priority taxes print one row per payment amount. The manual special-class list prints in Part I. Part J shows the unsecured pool total and payout percentage. Assumed and rejected contracts go in Part K.

  Parts Glade has no source for print blank with a warning, so you can fill them in by hand before filing:
  - the Part D dates, and the D.(3) post-petition arrearage;
  - the Part C attorney-fee type boxes, which are left unticked (the fee amounts are filled in);
  - the special-class term in Part I;
  - the term and treatment of assumed contracts in Part K, and the Part J creditor rows (the total and percentage are filled in);
  - the § 1325(a)(4) liquidation value when the case is above median, and monthly disposable income when it has not been entered;
  - a cramdown claim paid through the trustee that has no value entered.

  Lien avoidance is never listed, because this form states that it avoids no liens. A warning is raised when the case has a lien-avoidance claim.

  Two more warnings flag places where the calculator's figures disagree with the form:
  - Interest on a Part H priority claim. The form pays priority claims without interest, but priority taxes are calculated with interest.
  - A Part E pay-in-full claim whose stated value is below the claim. The value prints as entered, and the valuation box is left unticked.

  Plan-modification forms and the district's other companion forms are not generated.

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

> TODO: Confirm the Eastern District of Kentucky's recorded no-look attorney fee cap. The district was switched on with a $2,500 cap where the local rule (LBR 2016-2(a)) sets $4,500, so until it is corrected the §4.3(a) warning also appears for fees between $2,500 and $4,500.

> TODO: Confirm the Northern District of Alabama's recorded trustee fee percentages and no-look attorney fee cap. The district was switched on with the national defaults (the local rule's cap is $4,500). The form prints no trustee fee, so this affects the calculator's figures only. Also confirm with the pilot firm whether Western Division monthly amounts should be spread from the "Month N" start.

> TODO: Confirm the Northern District of Texas's recorded no-look attorney fee cap and trustee fee percentage. The district was switched on while those figures were still the national defaults.

## Related Features

- [Chapter 13 Plan Calculator](./chapter-13-plan-calculator.md)
- [Schedule Tools](./README.md)
- [Chapter 13 Plan Status](../../../integrations/efiling/filing-packet/chapter-13-plan-status.md)
- [PACER](../../../integrations/pacer/README.md)
