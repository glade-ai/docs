# How Autofills Work

## Overview

Autofills populate field values from external data sources, AI inference, or computed expressions. AI autofills allow AI to infer field values from uploaded documents or prior responses. This page covers when an autofill writes to a field, how autofills that combine several values behave, calculated table totals, and autofills that draw on reference data.

## Key Behaviors

### When an autofill may overwrite an answer

An answer someone typed by hand is protected — an autofill does not replace it. Two situations are treated as *not yet an answer*, so an autofill fills them:

- **The field is empty.** A field left blank, holding only spaces, or holding an empty value counts as unanswered even if a person was the last to touch it.
- **The field says No and the computed result is Yes.** A Yes/No field answered "No" is upgraded to "Yes" once the data behind it says yes — for example, a Schedule A/B category answered "No" before anything was entered on the Master Property List is upgraded once matching assets are added there.

Both situations previously blocked the autofill for good, so a Schedule A/B category answered early — left blank, or answered "No" — never picked up assets added later and the generated schedule shipped without them. If your team has been re-checking Schedule A/B by hand for assets that failed to carry over, that is no longer necessary. Free text someone has actually written is still never overwritten.

For how hand-entered values are protected across saves and in list rows, see [Manual Overrides](./manual-overrides.md). Locked fields are the exception — see [Locked Fields](./locked-fields.md).

### Autofills That Combine Several Values

An autofill that draws from a list can join every matching row into a single answer instead of taking only the first one — for example collecting the descriptions of a client's assets onto a single line of a court form. This matters on Schedule A/B lines that ask for one brief description covering several items — several tax refunds, or several claims — where previously only the first row's description reached the field and the rest were dropped without any indication. Amounts can be totalled the same way. The joined text carries through to the generated PDF as well, so a schedule that previously printed a single description now prints all of them.

- The values are separated by a **semicolon and a space**, not a comma. Free-text entries such as asset descriptions routinely contain commas of their own, which made a comma-separated line impossible to read as a list.
- Lines filled before this change may still use commas. Re-run the autofill on the field to re-join it with semicolons.
- **Every row's description is carried onto the form, not only the first.** Some Schedule A/B description lines were joining only the first row in a category, so a client with three deposit accounts or three business interests had two of the descriptions dropped from the generated petition. All of the rows in the category are now joined. Where a **Describe** field on Schedule A/B had no autofill attached to it at all, one is set up, so the descriptions reach the form instead of being captured on the questionnaire and going no further.
- **Where the printed form has no separate description slot, the description is combined with the name.** Line 17 of Schedule A/B (deposits of money — checking, savings, and similar accounts) has nowhere on the official form to print a brief description, so the description is printed alongside the institution name in the one field the form provides. Firms had been typing the institution and the description into the name field together as a workaround; that is no longer necessary. An entry with no brief description prints the institution name on its own, as before.
- Petitions generated before these corrections keep the text they were generated with. Re-generate the petition on a case whose Schedule A/B descriptions should appear on the filed copy.

### Totals Calculated From Other Cells in a Table

A calculated cell in a table that adds up other cells in the same table — such as Schedule I line 10, which is line 7 plus line 9 — is now worked out after the cells it reads, so it always reflects their current values.

- Previously such a total could be calculated before the lines it adds up, using what those lines held before your latest edit. Schedule I line 10 could show a stale figure, zero, or an amount from an earlier edit — it was effectively one edit behind.
- If you reviewed a Schedule I line 10 figure that did not match lines 7 and 9, edit either line again or re-check the total; it now updates to match.

### Autofills From Reference Data

Some autofills fill a field from reference data Glade already holds for the case rather than from a document or an AI inference — the IRS standard deduction amounts on the Chapter 7 means test (Form 122A-2) are the common example.

These fields populate when you open the questionnaire, with no action needed from you. Previously they arrived empty and only filled in after you triggered them by hand, which was easy to miss and left the means test showing no deductions. You can still re-run one of these autofills at any time to pick up changed case data, and a value you have entered or corrected by hand is not overwritten.

The national standard deduction amounts — including food and clothing — are selected using the debtor's state and household size together. An amount that was filled in before this behavior was corrected may have used another state's figure, so re-check the deductions on any means test prepared earlier and re-run the autofill to refresh them.

**These fields were being blanked when they were refreshed away from the form.** An autofill of this kind runs in two places: on screen while you have the questionnaire open, and away from the form when the case's data changes or the questionnaire is upgraded. The second of those was not being given the reference data at all, so it worked the figure out from nothing — and because these are single fields rather than cells inside a list, an empty result *cleared* the field rather than leaving it alone. A correct figure the questionnaire had filled in could be replaced with a blank or a zero without anyone touching it.

- On the current Bankruptcy Schedules template this affected 24 fields. They cover the IRS and Census means-test standards — median income, food and clothing, out-of-pocket health care, housing, and transportation — as well as court reference data such as the court division and the court multipliers. The exemptions tables and Chapter 13 district variables are held the same way.
- Both routes now reach the same value, so a figure refreshed away from the form matches what the questionnaire computes on screen.
- **Re-check these fields on any case prepared before this.** A means test deduction or a court division field sitting blank or at $0.00 is the symptom. Re-run the autofill on the field to fill it in correctly.

## Edge Cases & Limitations

- Reference-data autofills that were blanked before the correction are not repaired automatically. Nothing on the field records that it was cleared rather than never filled, so a blank means-test deduction or court division field needs its autofill re-run to tell the difference.
- When using "Autofill from Glade questionnaire" on a list field, date entries that contain only a descriptive placeholder (no actual date value) are skipped — the destination date field is left blank rather than filled with invalid text. You can fill these fields manually after autofill completes.
- When an autofill fills a currency field but cannot work out an amount, the field is set to **$0.00** — see [Field Behaviors](../filling-out/field-behaviors.md#currency-field-behavior).

## Related Features

- [Questionnaires](../README.md)
- [Autofills](./README.md)
- [Autofill Status Indicators](./status-indicators.md)
- [Manual Overrides](./manual-overrides.md)
- [Locked Fields](./locked-fields.md)
- [AI Agents](./ai-agents.md)
- [Means Test](../schedules/means-test.md)
