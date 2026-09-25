# Schedule I and Income

## Overview

Schedule I reports the debtor's income, and on bankruptcy cases most of its figures come from the case's Income Organizer. This page covers importing Income Organizer figures into the questionnaire and itemizing the individual sources behind Schedule I lines 8f and 8h.

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
- On a case that does not use case data sync, the summed amounts still fill but the item lists stay empty.

> TODO: Confirm the label on the cell button, and which firms' templates carry the 8f/8h item lists — the lists and the buttons are added to a template in the questionnaire editor rather than being present on every template.

The Schedule I line 8a business statement is covered under [PDF Fill Mappings](../templates/pdf-fill-mappings.md#supplemental-and-local-court-forms).

## Edge Cases & Limitations

- **Import Data from Income Organizer** is the one action that overrides hand-edited calculator figures. There is no way to import while keeping a particular correction — re-enter the correction after importing.
- The **Specify** box on Schedule I line 8h, shown once "Other monthly income" has a figure in it, is validated like any other required field (see [Conditional Visibility](../templates/conditional-visibility.md)).

## Related Features

- [Questionnaires](../README.md)
- [Schedule Tools](./README.md)
- [Means Test](./means-test.md)
- [Manual Overrides](../autofills/manual-overrides.md)
- [Layout and Navigation](../filling-out/layout-and-navigation.md) — opening the Income Organizer from Source Data
- [Income Organizer](../../income-organizer/README.md)
