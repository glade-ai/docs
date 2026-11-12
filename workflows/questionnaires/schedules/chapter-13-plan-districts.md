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
  - **§7.6 prints what the plan pays unsecured creditors.** The dollar figure in "distributions equal to $X or Y% of their allowed claims" is the amount the plan pays unsecured nonpriority creditors — the same figure as the calculator's "Paid to unsecured nonpriority" total — so it agrees with the percent beside it. Previously the dollar figure was the total of all allowed unsecured claims. Previews and newly finalized plans print the corrected figure; a plan finalized before the fix keeps its stored PDF, so re-finalize it to get a corrected copy for filing.
- **Southern District of Illinois** cases can generate a Chapter 13 plan on the district's Uniform Chapter 13 Plan, on the same terms as the other plan-generation districts. Parts of the form Glade has no source for print blank with a warning so you fill them in by hand — for example, every domestic support obligation prints in §7A, and one owed to a government unit has to be moved to §7B by hand.
  - **Section 1 payment method.** ePay and TFS are payment methods of their own, alongside payroll (a wage order) and direct payment. Exactly one of the Wage Order Required boxes — Yes, No, ePay, or TFS — is ticked, matching the plan's payment method; "No" is not ticked beside ePay or TFS. A plan with none of them chosen warns. Previously the ePay and TFS boxes could never be ticked.
  - **Employer under a wage order.** The employer details typed on the plan print first. When none are typed, a single filer's plan with a wage order prints the employer named on the client's record, with a warning to add the employer's address and phone. A joint plan prints no employer, because Glade cannot tell whose wages the order is on; a wage order that still names no employer warns. Previously a wage-order plan printed "Yes" with a blank employer line and no warning.
  - **Section 3A, "by the Debtor(s) or Co-Obligor".** The plan records who pays the 3A mortgage directly — the debtor or a co-obligor — and ticks the matching box when 3A lists a mortgage. Until it is chosen, both boxes stay blank with a warning; Glade does not guess "Debtor(s)". The 3A start and end dates are part of the existing row-details warning.
  - In the calculator's **Form details**, **Payment method** lists **ePay (online payment)** and **TFS (bank withdrawals)** along with payroll and direct payment. **Direct payments made by** is there too, with **Debtor(s)** and **Co-obligor**. It prints only when the plan lists a mortgage paid directly; left unset, neither box is ticked and the plan warns.
- **Southern District of Florida** cases can generate a Chapter 13 plan on the district's Local Form LF-31, on the same terms. What the generated plan fills in for you:
  - **Account numbers and addresses.** Every claims table with a "Last 4 Digits of Account No." column prints the creditor's last four digits from the Master Creditor List, and Section III prints each creditor's address from the creditor list on one line. A creditor with no account number or address on the list prints blank there.
  - **Typed payout schedules.** Where you typed a claim's payout schedule in the calculator ("Override with text"), the plan prints your text as written in place of the computed payments. This applies to every trustee-paid payout line: the II.B attorney fees, III.A, III.B, and IV.A through IV.D. A cure split off a claim prints the schedule typed for the cure, not the parent claim's. Previously the typed text was ignored and the computed amounts printed.
  - **Vehicles in III.B.2.** A valued claim secured by a vehicle prints in III.B.2 with the 910-day box ticked. Other valued personal property prints in III.B.3 with its one-year box ticked. Glade tells a vehicle from the item's category on Schedule A/B: cars, vans, trucks, SUVs and motorcycles are vehicles; watercraft, aircraft, motor homes and ATVs are left for you to decide. The boxes count back from the filing date (or, before the case is filed, from the day the plan is generated) to the date the debt was incurred: the purchase date entered on the claim, otherwise Schedule D's "Date debt was incurred". Exactly 910 days, or exactly one year, ticks the "or more" box. Previously every valued car loan printed in III.B.3 with both pairs of boxes blank.
  - **Attorney fees (II.B).** Total fees include any additional attorney fees added in the calculator, itemized under Local Rule 2016-1. A plan with no additional fee prints as before. Previously additional fees were paid through the plan but appeared nowhere on it.
  - **Mortgage modification mediation (III.A and IX).** A mortgage the debtor is taking to mortgage modification mediation (MMM) prints as one. Its III.A payment line reads "MMM Adequate Protection", the plan pays the claim's adequate protection payment in place of the contract installment, and no arrears are cured, so "Arrearage/ Payoff on Petition Date" is blank. Section IX ticks Mortgage Modification Mediation and lists each MMM claim's lender, loan number and property address. The loan number shows only the last four digits behind a mask (for example `xxxxxx7821`), and is blank when the creditor list has no account number. Section IX's NONE box is no longer ticked when the plan has an MMM referral. Previously both parts printed blank, and the plan paid the mortgage its contract installment plus a cure.
  - **V.B** is ticked when the unsecured payout is set to "Paid in full (100%)".
  - **Section VI (student loans)** is ticked NONE, because Section VI is the court's Student Loan Program, which Glade does not prepare filings for. A warning is raised when the petition lists a student loan.

  Parts the calculator cannot decide print blank with a warning rather than being guessed:
  - a valued personal-property claim Glade cannot sort as a vehicle or not prints in III.B.3, and III.B.2's NONE box stays unticked while one exists, so the plan never tells the court there are no vehicles;
  - a III.B.2 or III.B.3 claim with no incurred date on or before the petition date leaves its boxes blank;
  - the principal-residence and taxes-and-insurance boxes in III.A and III.B.1 stay unticked until the claim's answers are filled in;
  - payment addresses in IV.C and IV.D, which differ from the creditor's notice address (support is usually paid through the State Disbursement Unit, and taxes at the agency's payment address);
  - account numbers on separately classified claims (V.C), which are typed by hand rather than linked to a claim;
  - all of II.B when the attorney fee has not been entered. A $0 fee ticks NONE and also warns. The PRO BONO box is never ticked;
  - an MMM claim with no adequate protection payment, or one whose III.A line prints a different monthly amount (a monthly payment fixed by hand, a priority shortfall, or a stepped schedule), raises a warning. A payout schedule you typed yourself is not compared;
  - the stay-relief box, the tax-return provision where the case's division is unknown, and the amendment number.

  The claim inputs these boxes read are in the calculator. On a valued personal-property claim (III.B), **Collateral type** (Vehicle / Other personal property) starts from the property's category on Schedule A/B and can be changed; choosing **Vehicle** shows a **VIN** field. The petition does not collect VINs, so III.B.2 prints the VIN blank until you enter it. The claim's Collateral section also shows **Date incurred on Schedule D:** when no purchase date is entered. On a real-property claim, **Principal residence** (Debtor's principal residence / Other real property) and **Taxes and insurance** (Escrow is included in the payment / Debtor pays the taxes directly / Debtor pays the insurance directly / Debtor pays the taxes and insurance directly) start at **Not answered**, and the boxes stay unticked until you answer. The unsecured payout tile offers **Paid in full (100%)**, which ticks V.B.

  A long-term mortgage paid through the plan is marked for MMM, with its adequate protection payment, on the claim itself. A marked mortgage you move to paid outside the plan or not in the plan is not treated as MMM and is paid as usual; this applies on the Middle District of Florida plan as well. On a Southern District of Florida case, the MMM election and the adequate protection payment appear on "Secured, long term, in plan" real-property claims in the calculator, as on Middle Florida. The payment defaults to the lesser of the contract payment and 31% of gross monthly income; a mortgage answered **Other real property** for Principal residence gets no default, so enter the payment yourself.

- **District of Arizona** cases can generate a Chapter 13 plan on the district's Local Form 2084-4 (5/26). See [Chapter 13 Plan — District of Arizona](./chapter-13-plan-arizona.md) for how claims are placed on the form and what to check by hand.
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

  Every "Last Four Digits of Acct. No." column on this form, including C.5(a) secured long-term claims, prints the creditor's account last four digits from the Master Creditor List. Glade uses the creditor's last-four field, or failing that the last four letters or digits of its account number ("9779-1211-C203" prints "C203"). A creditor with neither prints blank. These columns used to print blank on every plan, so regenerate a plan to fill them in.
- **Northern District of Illinois** cases can generate a Chapter 13 plan on the district's Form 13-6, *National Chapter 13 Plan (Official Form 113) - Expandable and Calculating*. The form is Official Form 113 word for word, with the court's Exhibit of estimated trustee payments at the end. It works the same way as the other plan-generation districts: you open the form from the calculator, and there is no per-firm setting to switch on. How the plan is filled:
  - The running header carries Debtor 1's full name, as the court's form prints it, and is marked for a joint case.
  - §2.4 lists one row per additional payment, with its source, amount, and date, in date order. Every priced lump sum prints, so the §2.5 total always matches the rows above it.
  - An arrearage cure split off a claim prints with that claim: in its §3.1 or §6.1 row, or added to the priority claim in §4.4. Each Exhibit line counts the cures from its own section. A standalone arrearage claim prints as its own §3.1 row.
  - The §3.1 **Distributed by** box follows who pays the ongoing installment. A mortgage the debtors pay directly reads as debtor-paid even when the trustee cures the arrearage. A standalone arrearage claim has no installment, so neither box is ticked.
  - §4.5, §5.2, and §5.3 always print "None", because no claim treatment is assigned to them.
  - The §9.1 date is the plan date, or the day the plan was generated in Central time.
- **Western District of Texas** cases can generate a Chapter 13 plan on the district's Revised District Form Chapter 13 Plan, *Chapter 13 Plan and Motions for Valuation and Lien Avoidance* (effective February 3, 2025). This is a local court form, not Official Form 113. It works the same way as the other plan-generation districts: you open the form from the calculator, and there is no per-firm setting to switch on. How the plan is filled:
  - The caption's division comes from the case's court division (Austin, El Paso, Midland, San Antonio, or Waco). Any other division prints blank with a warning. The signature date is taken in Mountain time for El Paso and Central time elsewhere.
  - §2.1 "paid by" ticks Payroll Order or Direct as elected in the calculator. 3rd Party Epay is ticked only when the "Other" payment method text names ePay or TFS.
  - §3 vesting ticks "vests in the debtor" when property vests at confirmation, and "remains property of the estate" when it vests at discharge.
  - Every assumed contract is listed in §6.1. Contracts the trustee pays are also listed in §7.3 with their arrears and ongoing payment.
  - Surrendered collateral goes in §7.4 and debtor-paid claims in §7.5. Long-term claims go in §7.6, marked Trustee (Conduit) when the trustee pays them and Debtor (Direct) otherwise. Cures go in §7.7, and cramdown and pay-in-full claims in §7.8.
  - Lien avoidance is split by kind of lien: a mortgage strip goes in §7.9, and any other lien goes in the §7.10 motion.

  Parts Glade has no source for print blank with a warning, so you can fill them in by hand before filing:
  - the §7.1 payment method boxes, the §7.4 collateral location, and the §7.6 payment due date;
  - parts of a plan this form has no place for: a filing fee paid through the plan, lump sums, special classes, and assumed-contract arrears the trustee doesn't pay;
  - a §7.8 pay-in-full claim whose stated value is below the debt.
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
- **Eastern District of Wisconsin** plans print the elections the district's filed plans make:
  - **First payment due (§ 2.1.B).** Choose how the filing fee was paid (paid when filing, or in installments), then when the first plan payment is due under that choice. The form ticks exactly those two boxes, and prints a specific date you pick on the chosen branch's line. A due date with no filing-fee choice prints nothing, because the form has nowhere to put it. With nothing chosen the section stays blank, as the form's own text then makes the first payment due 30 days after the petition. A half-made choice raises a warning.
  - **Post-petition claims under § 1305 (§ 6.2).** The box you choose is ticked. A warning is raised only when no choice is made; previously both boxes always printed blank with a warning.
  - **Chapter 7 liquidation amount (§ 5.1).** The amount the calculator works out now prints at any income level, including for above-median debtors, where it used to print blank. A plan saved before this change prints it once the plan is saved again.
- **Western District of Wisconsin** plans print two more lines the filed plans carry:
  - **How the debtor pays (Section II.A).** The court's form assumes a wage order and has no box for anything else, so a line is added under the payment total: "Payments to be made debtor direct." for a direct-pay plan, or a line such as "Debtor will pay $173.08 Bi-Weekly for 60 months" for each payment step of a weekly, every-two-weeks, or twice-a-month payroll plan. The line appears once a payment method is chosen for the plan.
  - **Loans the debtor pays directly (Section IIIB).** The payoff prints as the filed claim amount, and the monthly payment shows the months it covers — for example "$603 /month (Months 1 to 60)". The months come from the plan's own schedule for that loan, which is the whole plan unless set otherwise. Previously the payoff was blank and no months printed.

  The court's own wording does not change on either Wisconsin form, and no other district's form is affected.

On an Eastern District of Wisconsin plan, both choices are on the calculator's **Form details** card. No other district's card shows them.

- **First plan payment** (§ 2.1.B). **Filing fee** is how the fee was paid. With **Paid in installments** selected, **First payment due** offers **30 days after last installment**, **30 days after confirmation**, **On a set date**, and **Leave blank**. **On a set date** adds **First payment date**. The due-date wording follows the filing-fee choice, and changing or clearing **Filing fee** clears the due date. Left unset, the card says the form's own rule applies: the first payment is due 30 days after the petition is filed.
- **§ 1305 post-petition claims** (§ 6.2). The choice to have the trustee pay is **Trustee pays the claim**. The card says that leaving it unset prints both boxes blank and raises a warning on the plan.

### Northern District of Georgia: §3.1 rows with no arrearage

On the Northern District of Georgia plan, a §3.1 (maintenance and cure) claim with a $0 arrearage now prints `$0` for the arrearage, the claim's arrearage interest rate (`0.00` if none was entered), and `$0` for the monthly payment. Previously only the arrearage cell was filled. The interest rate and monthly payment printed blank, which looks like a missing entry and can draw a trustee objection.

- The same applies to a maintained claim with no arrearage at all. Its contract rate used to print under "Interest rate on arrearage". It now prints `0.00`, because that column is the rate on the arrearage, not the loan.
- A free-text arrearage payment schedule you entered still prints as typed in the monthly column.
- Cure rows for claims with a positive arrearage are unchanged.
- Plans already generated keep the old output. Regenerate the plan to pick up the change.

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

> TODO: Confirm the Northern District of Texas's recorded no-look attorney fee cap and trustee fee percentage. The district was switched on while those figures were still the national defaults.

The calculator uses the Northern District of Illinois and the Western District of Texas recorded trustee fee and no-look attorney fee cap. Those figures are kept with the district rather than printed from the form. Check them against each district's local rule. Contact Glade support if the fee warning doesn't match.

## Related Features

- [Chapter 13 Plan Calculator](./chapter-13-plan-calculator.md)
- [Chapter 13 Plan — District of Arizona](./chapter-13-plan-arizona.md)
- [Schedule Tools](./README.md)
- [Chapter 13 Plan Status](../../../integrations/efiling/filing-packet/chapter-13-plan-status.md)
- [PACER](../../../integrations/pacer/README.md)
