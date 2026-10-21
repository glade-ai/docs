# SOFA Other Income (Part 2, Question 5)

## Overview

Statement of Financial Affairs Part 2, question 5 asks for income the debtor received from sources other than employment or business. The questionnaire records it as one list per debtor, with one income source per row, so a paralegal can enter as many sources and years as the case needs. Form 107 prints the rows grouped by year.

## Key Behaviors

- **One list per debtor, one source per row.** Each row records:
  - the **calendar year** the income was received, as a four-digit year;
  - the **source** of the income;
  - a **description**, when the source is "Other Income";
  - the **gross amount**.
- **No cap on sources or years.** Previously the question had three fixed tables, one per year, each with room for three sources per debtor, which limited a case to three sources a year and three years in total. Sources had to be merged to fit. A row can now name any year, so earlier years can be reported when the case calls for it.
- **Spouse's Income is a source option.**
- **The "When did you receive other income?" checkboxes are removed.** They existed only to show the per-year tables. Both lists show when question 5 is answered "Yes"; the Debtor 2 list also requires a joint filing.
- **Form 107 groups each debtor's rows by year.**
  - The three official year blocks — the current year, the year before, and the year before that — always print, and the year is printed in each block's year slot.
  - A year with many sources gets a taller block rather than being cut off.
  - Rows for years earlier than the three official blocks print as additional year blocks.
  - Amounts line up with their source, including where a long source name wraps onto a second line.
- **Upgraded questionnaires keep their answers.** When a questionnaire that used the old tables is upgraded to a template version with the lists, each answered source becomes a row in that debtor's list, dated with the year of its table. See [Template Upgrades](../case-data/template-upgrades.md).
- Questionnaires still on a template version with the old tables keep the tables, and Form 107 prints them as before.

## Edge Cases & Limitations

- When old table answers are moved into the lists on upgrade, "current year" means the year the answers were last saved, not the year of the upgrade. A questionnaire last saved in an earlier year carries its rows under that earlier year — check the years after upgrading an older questionnaire.
- Only years that were ticked under the old "When did you receive other income?" question are carried across on upgrade. A table for an unticked year was hidden, and anything left in it is not carried.
- Empty $0 amounts the old tables filled in by default are not carried across as rows.

> TODO: Confirm whether firms with their own Client Questionnaire template receive the lists automatically or need the template converted and published.

## Related Features

- [Schedule Tools](./README.md)
- [Schedule I and Income](./income.md)
- [Working with Lists](../filling-out/working-with-lists.md)
- [Template Upgrades](../case-data/template-upgrades.md)
- [Field Behaviors](../filling-out/field-behaviors.md) — free-text dates on the Statement of Financial Affairs.
