# Fields, Lists, and Tables

## Overview

Fields define individual form inputs on a questionnaire template. This page covers the field types available, select options, linked and referenced fields, and how list fields are displayed as tables.

## Key Behaviors

### Fields

Fields define individual form inputs. Each field belongs to a section and has properties including label, type, required flag, placeholder, hint, validation rules, options (for select fields), and display configuration.

Supported field types include: short text, long text, numeric, number, currency, date, phone number, SSN, name, US address, international address, single select, multi-select, list, table, percent, and domain-specific types like creditor select, court division select, bankruptcy statute select, median income, and means test summary.

The **means test summary** field is a read-only display field rather than an input. Instead of collecting an answer from the client, it shows a consolidated summary of the case's means test information. A single field type serves all four Means Test forms — the Chapter 7 forms (B122A-1 and B122A-2) and the Chapter 13 forms (B122C-1 and B122C-2) — and displays the summary appropriate to the form it appears on.

Currency fields support a **Default to blank** setting in the template editor. When enabled, the field starts empty instead of showing $0.00 when first loaded. This is useful for optional amounts where a $0.00 default would be misleading. See [Field Behaviors](../filling-out/field-behaviors.md#currency-field-behavior).

### Field Options

Select-type fields define their options as a list of choices, each with a label, key, default flag, and optional PDF fill key.

### Linked Fields

Linked fields let one field's value automatically propagate to another field within or across sections, keeping data synchronized. Changes propagate in real time as clients fill out the form.

### Referenced Lists

Fields can reference other list fields to create cross-references between data sets. For example, a creditor select field can reference a creditor list so clients choose from items they have already entered.

When you choose a creditor from a referenced creditor list — for example, in the SOFA Part 3 "creditors paid over $600" selection or other creditor dropdowns — each option is identified by the creditor's **account number** underneath the name. This makes creditors that share a name distinguishable: a client with several accounts at the same bank shows one option per account number, instead of several identical-looking entries labeled with an internal identifier. Referenced lists other than creditors are unaffected.

### Table Columns

List fields can be displayed in table view. Table columns have settings for editability and visibility, controlling how the data appears and whether clients can modify values inline. The "Visible in table view" setting is available for all fields within a list, including fields nested inside explanation sections at any depth.

Table columns are sortable. Currency and percent columns sort by their numeric value; date columns sort chronologically. This means sorting a currency column orders rows from lowest to highest dollar amount (or vice versa), not alphabetically by the displayed text. Sort order is preserved when you switch between the default view and full screen view — sorting a column in full screen keeps that ordering when you return to the standard view.

A list's display toggles — for example **Show duplicates** and **Show zero'd accounts** on the creditor list — are available in full screen view as well as the standard view. They appear in the full screen toolbar and share their setting with the standard view, so a toggle you change in full screen still reflects that state when you exit. Previously these toggles sat underneath the full screen overlay and could not be reached without leaving full screen first.

Dropdowns that list options alphabetically sort without regard to capitalization, so a list of names reads `Aaron, alice, bob, Zack` rather than putting every capitalized entry ahead of the lowercase ones.

### Flipping a table's rows and columns

A table normally runs its fields **down** the visual rows. A **flip rows and columns** setting on the table turns that around, so each field becomes a visual column and the table reads the conventional way — one column per question, one row per entry. Firms that were reproducing a court form or an internal worksheet with a fixed column layout previously had to work against the default orientation.

- The setting is on the table itself and is available on tables only. Lists that are not displayed as a table are unaffected.
- **It changes the layout, not the answers.** Turning it on or off rearranges how the table is drawn; answers already recorded stay attached to the same questions and are neither moved nor cleared. A questionnaire part-way through being filled in can be flipped without losing anything.
- Everything else about the table behaves as before — saving as you type, validation, live updates between people working on the same form, and how the answers land on a generated PDF.
- New tables are created unflipped, so nothing changes for a template nobody edits.

> TODO: Confirm the exact label of the setting in the template editor and where it sits among the table's other settings.

## Edge Cases & Limitations

- List fields that use referenced lists depend on both the referencing and referenced fields existing in the same questionnaire template.
- Deduplication of list items is available but requires specifying the field.
- List fields that are linked as destinations — populated automatically from another list in the questionnaire at filing time (for example, Schedule D Creditors mirroring the Creditors list, or a Schedule D creditors list that auto-populates from a master creditor list) — are not independently validated or counted as incomplete during validation. Only the source list needs to be filled; the destination list does not need to be filled out separately.

## Related Features

- [Questionnaires](../README.md)
- [Building Templates](./README.md)
- [Validation Rules](./validation-rules.md)
- [Conditional Visibility](./conditional-visibility.md)
- [Working With Lists](../filling-out/working-with-lists.md)
- [Creditors](../schedules/creditors.md)
