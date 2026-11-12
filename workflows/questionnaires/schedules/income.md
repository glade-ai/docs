# Schedule I and Income

## Overview

Schedule I reports the debtor's income, and on bankruptcy cases most of its figures come from the case's Income Organizer. This page covers importing Income Organizer figures into the questionnaire, itemizing the individual sources behind Schedule I lines 8f and 8h, and line 8h as the locked sum of its sources.

## Key Behaviors

### Importing Income Organizer Figures

**Import Data from Income Organizer** takes its figures from the results stored on the income organizer — the same numbers the organizer's own table shows.

- Previously the import worked the figures out separately from the organizer, so the button could fill in numbers that disagreed with the organizer it claimed to be importing from. The two now agree because they come from the same place.
- **The import replaces figures you have edited by hand.** The confirmation prompt has always warned that importing will overwrite changes made in the questionnaire, and that is now what it does. A calculator figure a paralegal typed over is replaced with the organizer's value and shown as coming from the case record. Editing a figure by hand normally protects it from being refreshed automatically, so the import is the one action that deliberately overrides that — which is why it asks first.
- Imported figures stay put. Reloading the questionnaire shows what was imported rather than reverting to what was on the form before.
- **If the organizer has nothing calculated yet, the import tells you so** rather than reporting success while filling in nothing. It reads *"No income organizer data available to import yet."*
- Both places the import is offered — the button in the Schedule I section and the one on the questionnaire's details — behave the same way.

For how hand-edited Schedule I and Means Test calculator figures are otherwise protected, see [Manual Overrides](../autofills/manual-overrides.md#overriding-a-schedule-i-or-means-test-figure-the-calculator-produced). Schedule I line 8 values synced from the Income Organizer are covered under [Case Data Sync](../case-data/case-data-sync.md#case-data-sync-fields).

### Itemizing Other Income on Schedule I Lines 8f and 8h

Schedule I reports other government assistance on line 8f and other monthly income on line 8h, and the official form has room for one description and one amount per debtor. A client often has several sources behind that one figure. The income table keeps the summed amount, and a button on the cell opens the list of the individual sources behind it.

- Each debtor's column has its own button opening its own list, so sources stay separated by debtor and by line — an 8f source never turns up under 8h.
- The list opens over the form, where rows can be added and edited as on any other list. The table's summed amount is still what the form's amount line uses.
- These lists do not appear as extra lists underneath the income table, and they do not count toward the section's completion progress.
- The sources come from the case's income organizer. Removing a source there, or taking it off Schedule I, removes its row here.
- A questionnaire created or upgraded to a new template version after sources are already in the organizer starts with those rows filled in, for both debtors on a joint case. Before, the lists stayed empty until the organizer next changed. This applies only to that questionnaire. Other questionnaires on the case aren't changed. A questionnaire with case data sync turned off still starts empty.
- On a case that does not use case data sync, the summed amounts still fill but the item lists stay empty.

### Line 8h Is the Sum of Its Income Sources

On the current Bankruptcy Schedules template, Schedule I line 8h ("Other monthly income") is no longer typed in. It is calculated as the total of the debtor's 8h income-source list and is locked, so the amount printed on line 8h always adds up to the sources listed under it.

- **Enter or change other income in the 8h source list.** Add, edit, or remove a source there and line 8h, the line 9 and line 12 totals, and the figures that read them update to match. The **Show income sources** button on line 8h opens the list.
- **The "8h. Other monthly income. Specify" field is removed.** Each source in the list carries its own description, and those are what print, so a separate Specify line is no longer needed.
- Each debtor's 8h is summed from that debtor's own list. On a joint case, Debtor 2's 8h is filled only when the case has a Debtor 2 column.
- A source that has been removed or struck through on an amended schedule does not count toward 8h.
- Previously 8h was filled from the Income Organizer and could be typed over, while its sources were listed separately, and nothing tied the two together. A typed 8h total could disagree with its listed sources, so the printed Schedule I showed the sources with a blank or different 8h while line 9 carried the typed figure.

**Upgrading a questionnaire keeps a typed 8h amount.** When a questionnaire is upgraded to a template version with the locked 8h:

- **An 8h amount someone typed by hand is moved into the list.** If the list already holds less than the typed amount, a new source is added for the difference, described with the old Specify text — or "Other monthly income" when Specify was blank — so 8h keeps its total. Nothing is added when the list already covers the typed amount; differences under 5 cents are treated as rounding.
- **An 8h amount that came from the Income Organizer is not moved.** The organizer's own 8h sources fill the list after the upgrade, so 8h is the organizer's total as before. On a case with case data sync turned off, those sources are not sent and 8h becomes the total of whatever the list already held.
- If the typed 8h was lower than the list's total, 8h rises to the list's total after the upgrade, and lines 9 through 12 follow.
- A questionnaire that stays on an earlier template version keeps the typed 8h and Specify field until it is upgraded.

Line 8f is unchanged and can still be typed.

> TODO: Confirm the label on the cell button, and which firms' templates carry the 8f/8h item lists — the lists and the buttons are added to a template in the questionnaire editor rather than being present on every template.

The Schedule I line 8a business statement is covered under [PDF Fill Mappings](../templates/pdf-fill-mappings.md#supplemental-and-local-court-forms).

## Edge Cases & Limitations

- **Import Data from Income Organizer** is the one action that overrides hand-edited calculator figures. There is no way to import while keeping a particular correction — re-enter the correction after importing.
- On questionnaires still on a template version that has it, the **Specify** box on Schedule I line 8h, shown once "Other monthly income" has a figure in it, is validated like any other required field (see [Conditional Visibility](../templates/conditional-visibility.md)). Current template versions no longer have this box — see [Line 8h Is the Sum of Its Income Sources](#line-8h-is-the-sum-of-its-income-sources).
- Line 8h cannot be typed over on current template versions. To change it, change its source list.

## Related Features

- [Questionnaires](../README.md)
- [Schedule Tools](./README.md)
- [Means Test](./means-test.md)
- [SOFA Other Income](./sofa-other-income.md)
- [Manual Overrides](../autofills/manual-overrides.md)
- [Layout and Navigation](../filling-out/layout-and-navigation.md) — opening the Income Organizer from Source Data
- [Income Organizer](../../income-organizer/README.md)
