# Schedule A/B Property

## Overview

Schedule A/B lists the debtor's real and personal property. On the Bankruptcy Schedules questionnaire, properties are entered on the Master Property List and linked to the secured creditors that hold liens against them. This page covers liens and equity, the Property summary, values marked Unknown, and how Part 3 and line 19 print on the generated petition.

## Key Behaviors

### Property Liens on Schedule A/B

On a Schedule A/B property, you can attach more than one lien to the same property. The property's lien field lets you search for and select existing secured creditors from the Master Creditor List, and you can add as many as apply.

- As you select liens, the property's **total claim amount** updates automatically to the sum of the selected creditors' balances.
- A summary below the selector shows the **total liens** (with a count of how many) and the **equity after liens** — the property's value minus the total liens, which never goes below zero.
- The same creditor can't be selected twice on one property: liens already chosen drop out of the remaining choices, and the option to add another lien is disabled once every available lien is selected or while an empty selection is open.
- A selected creditor with a blank or zero balance adds nothing to the total.

The Exemptions Calculator uses the summed total of the selected liens when calculating equity available to exempt. If no liens have been selected for a property, it falls back to the single lien amount entered directly on the property.

**Moving a creditor's collateral to a different property clears the old one.** When you change which property a secured creditor is attached to, the creditor is removed from the property it used to be on as well as added to the new one.

- Previously the creditor could be left on **both** properties' lien lists, so the same secured claim counted against two assets. On a case where that happened, both properties understated their equity — and because equity after liens feeds the Exemptions Calculator, the Texas exemptions schedule, the Chapter 13 liquidation analysis, and the total claim amount on Schedule A/B, the error carried through to all of them.
- The old behavior depended on how the property and creditor lists were linked together in your firm's template, so it affected some cases and not others with no way to tell them apart from the form.
- **Re-check any case where collateral was moved between properties.** Open each property's lien list and confirm the creditor appears only against the property that actually secures it; the corrected equity figures are higher than the ones shown before.

> TODO: A separate problem can stop a lien change from reaching the property's lien list at all — the creditor's own collateral field saves correctly, but the property-side list, and the lien total and equity derived from it, can stay as they were. Confirm whether this has since been corrected before relying on the property-side figures.

### Property Summary

A **Property summary** button on the Schedule A/B property section opens a summary of the case's properties side by side, with each property's value, equity, the exemption claimed against it, and any unexempt amount.

- The **Equity** column is the property's value minus the liens attached to it, and never goes below zero. Previously it showed the property's value before liens — so a residence worth $520,000 against a $519,000 mortgage read as $520,000 of equity, and a vehicle that was fully underwater read as though it had positive equity. The summary now agrees with the lien detail on the property row and with the Exemptions Calculator.
- An exemption claimed at 100% of fair market value claims the equity remaining after liens, not the property's full value.
- The **Unexempt** column never goes below zero. A $15,000 homestead exemption claimed against $1,000 of real equity shows as fully exempt rather than as a negative amount.

If your team reviewed a property summary before this correction, re-check the equity figures on any case with liened property — the corrected figures are lower, and a property that appeared to hold equity may hold none.

### Marking a Value as Unknown

On bankruptcy Schedule A/B, an asset's current value can be marked **Unknown** (or overridden with custom text) instead of a dollar amount. When that value feeds a calculated line — for example, a figure carried onto another line or copied to Schedule C — the calculated line now shows **Unknown** (or the entered text) rather than $0.00. This matches how the value already appears in the answer view, and it carries through to both the live preview and the generated and filed petition. Section and part totals that are meant to stay numeric continue to show a dollar amount.

### Personal Property on Schedule A/B Part 3

Part 3 of Schedule A/B asks the debtor to describe their personal property under nine headings — household goods and furnishings, electronics, collectibles, sporting goods, firearms, clothes, jewelry, non-farm animals, and other items. On the generated petition, each item the case holds under a heading now prints on its own line under that heading, with its own description and its own value.

- **Previously every item under a heading printed as one run of text in a single box.** A case with a sofa, a bed, a dining set, and a washer showed all four crammed into the household-goods description with one combined value, so the court copy did not show what each item was worth.
- **The items come from the case's property list.** Whatever your team enters there under a category is what prints on that category's line, and each line prints only the items belonging to it — sporting goods do not appear under electronics.
- **The total line is unchanged.** Part 3's total, and the yes/no answers on each heading, work as before.
- **Adding or removing an item on the property list changes the printed rows** the next time the petition is generated. There is nothing to configure and no separate list to maintain for the form.

This applies to cases on the current schedules template. **A case already in progress on an older version of the template keeps printing the way it did** — one combined row per heading, with the values it already had. Nothing is lost or blanked on those cases, but the itemized layout does not appear on them until the questionnaire is upgraded to the current template. See [Template Upgrades](../case-data/template-upgrades.md).

If a Part 3 heading on a case you have already reviewed shows one combined entry, check which template version the questionnaire is on before treating it as a problem with the property list.

> TODO: Confirm whether personal property a client enters on the client questionnaire arrives as separate property-list items, or whether it is still combined into one entry per category when it reaches the schedules.

### Business and other interests on Schedule A/B line 19

Line 19 of Schedule A/B asks for the debtor's interests in businesses that are not publicly traded. The generated petition prints the **name recorded on the entry together with the brief description** entered alongside it, on the one line the form provides.

Previously only the name reached the form and the brief description was dropped, so a line that had been filled in on the questionnaire printed as a bare name with no indication of what the interest actually is. Entries with no brief description print the name on its own, as before.

Petitions generated before this change are not rebuilt. Re-generate the petition on a case whose line 19 entries carry a description if the filed copy should show it.

For how descriptions on other Schedule A/B lines (including line 17 deposits) are combined onto the form, see [Autofills That Combine Several Values](../autofills/how-autofills-work.md#autofills-that-combine-several-values).

## Edge Cases & Limitations

- Itemized rows on Schedule A/B Part 3 appear only on cases whose schedules questionnaire is on the current template. A case in progress on an older version still prints one combined entry per heading. There is no way to switch a single case over other than upgrading its questionnaire, and upgrading carries the other behaviors described under [Template Upgrades](../case-data/template-upgrades.md).
- Petitions already generated are not rebuilt. A draft or signature copy produced before the case was upgraded keeps the combined Part 3 entries it was printed with; generate the petition again to pick up the itemized rows.

## Related Features

- [Questionnaires](../README.md)
- [Schedule Tools](./README.md)
- [Exemptions Calculator](./exemptions-calculator.md)
- [Creditors](./creditors.md)
- [How Autofills Work](../autofills/how-autofills-work.md)
- [PDF Fill Mappings](../templates/pdf-fill-mappings.md)
- [Chapter 13 Plan Calculator](./chapter-13-plan-calculator.md)
