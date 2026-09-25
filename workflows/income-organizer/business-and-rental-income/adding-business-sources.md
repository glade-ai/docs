# Adding Business and Rental Sources

## Overview

Business and rental income sources can be added by your team from the Income Organizer or by the client from an income document request in the client portal. Adding one creates a business record on the case alongside the income source, collects the business's details in the same dialog, and records which contact the business or rental belongs to.

## Key Behaviors

### Business Details When You Add an Income Source

Adding a business or rental income source collects the business's details as part of the same dialog, and those details are saved onto the business record on the case as entered by your team.

- Because a business record is created alongside the income source, the details you enter land on it directly rather than needing to be filled in separately afterwards.
- The details are checked before anything is created, so a problem with what you entered is reported without leaving a half-created income source on the case.
- **The business's name and income type are not entered here** — they come from the income source itself, so renaming the source keeps the business record in step rather than leaving the two to drift apart.
- This applies to business and rental sources. Other income sources do not collect business details.
- **Everything the dialog saves is recorded as coming from the Income Organizer.** Case data records where each value came from, and a business added this way used to split across two sources — the couple of fields Glade worked out were attributed to the Income Organizer while the ones your team typed on the same form were recorded as manual entries. One business, one action, two answers. They now all read as Income Organizer.
- Values your team typed are still protected from being overwritten by a later document read, exactly as before. The change is what the source column says, not what is protected.

### Clients Adding a Business or Rental Source

When a client adds a business or rental income source from an income document request in the client portal, a two-step dialog collects the source the same way your team adds one. The source it creates looks the same on your side as one your team created.

- **Step 1 — details.** For a business, the client enters the business details: name, EIN, address, category, whether it is a sole proprietorship, dates, accountant, and the nature of the business. For a rental, only the property name is asked for.
- **Step 2 — income.** The client either **uploads documents** for the source, or **enters the figures manually** as a profit & loss statement — the period, gross income, expenses, and optionally the net figure printed on their statement.
- **Going back or closing before anything is saved** removes the draft source, so an abandoned attempt does not leave an empty source on the case.
- **Once a document has uploaded (or is uploading) or a manual statement is saved,** **Back** is disabled. Closing the dialog keeps the source and what has been saved.
- Other income types — employment, Social Security, and the rest — still use the existing add-source form.

### Which Contact a Business or Rental Belongs To

A business or rental on the case records which contact it belongs to — the **primary** or the **secondary** contact — the same way an asset or a creditor records its owner. Previously there was no way to say, even on a joint case where the organizer already knew which contact the income belonged to.

- **The contact is filled in from the income source** when the business or rental is created from the Income Organizer, so a source already tied to a filing contact does not have to be assigned again.
- **A source that is not tied to a filing contact is left unassigned** rather than guessed at.
- **A choice your team makes by hand is the one that is kept**, including clearing it back to unassigned. It is not replaced the next time the case's income data is refreshed.
- Businesses and rentals recorded before this can be assigned by hand; nothing is assigned for them retroactively.
- This records who the business or rental belongs to. It does not move income sources between organizers and does not change any income calculation.

## Edge Cases & Limitations

- Business details entered when an income source is created are saved on a best-effort basis alongside the source itself. If the source is created but the details do not appear on the business record, open the business and enter them there.
- Business fields recorded before the source labels were unified still read as manual entries. The label is corrected going forward rather than rewritten across existing cases — contact support if a firm needs its existing rows relabeled.

> TODO: Confirm where a profit and loss statement is uploaded against a business source, and where the business's own details are viewed and edited on the case.

## Related Features

- [Business and Rental Income](./README.md)
- [Profit & Loss Statements](./profit-and-loss-statements.md)
- [Matching Statements to Businesses](./matching-statements-to-businesses.md)
- [More Than One Organizer on a Case](../multiple-organizers.md)
- [Income Organizer](../README.md)
