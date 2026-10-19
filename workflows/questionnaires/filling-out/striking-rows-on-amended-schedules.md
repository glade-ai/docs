# Striking Rows on Amended Schedules

## Overview

When you amend a schedule, the court needs to see what left it. Instead of deleting a creditor, property, or other list entry, your team can strike the row. A struck row stays on the questionnaire and keeps printing on the amended schedule, crossed out, with its values and line number. Every total, calculation, and downstream use of the list treats it as gone. Attorneys and paralegals preparing amended schedules use this.

## Key Behaviors

### How to strike a row

Staff strike a row from the row's ⋮ (more actions) menu with **Amend: Strikethrough**, and choose it again to clear the strike (**Amend: Bold, Italicize, Underline** on the same menu marks a row as added). The same option appears in the bulk-edit menu when several rows are selected; a bulk strike skips rows marked as duplicates. A struck row shows as **Marked as removed**. These controls are for staff only; clients do not see them.

The strike controls are being rolled out gradually and may not appear for every firm yet, and a strike already saved always displays and prints regardless.

- **The row still prints, crossed out.** A struck row keeps its values and its line number on the amended schedule. Rows after it are not renumbered.
- **It stops counting in totals.** Schedule totals and any other sum or count over the list leave the struck row out, both on screen and on the printed PDF. For example, a struck Schedule D creditor no longer adds to the Schedule D total.
- **Liens and equity.** A struck creditor no longer reduces the equity of the property it is linked to. If the struck creditor was a property's only lien, the property shows no lien. It does not go back to an older stored lien amount.
- **Exemptions and the property summary.** Struck properties and struck exemption claims are left out of the exemptions calculation and the property summary.
- **Validation and progress.** A struck row does not raise required-field or other validation findings, and it does not count toward section progress.
- **AI agents.** Agents do not read struck rows as input and never delete them. When an agent rebuilds a list, the struck rows already in that list are kept as they are.
- **Links.** A struck row is not offered when you choose an entry to link to, for example when you link an exemption to a property.
- **Creditor matrix and Chapter 13 plan.** Struck creditors are left out of the creditor matrix, and struck creditors, properties, and exemptions are left out of the Chapter 13 plan calculator.
- **Document uploads and AI review.** A struck row does not get a document upload slot, and the AI review does not look at it.
- **A list with a struck row is never hidden.** Many lists sit under a Yes/No question, such as "Do you own household goods?" If striking the only row turns that answer to **No**, the list still stays on screen with the struck row intact, so the row is not cleared. On the printed Schedule A/B Part 3, the line prints **No** with the struck row crossed out beneath it.
- **Case data is not changed.** Striking applies to the questionnaire only. The creditor or asset stays on the case record and is not deleted or flagged there.

## Configuration

No setup is needed. Striking is available on list rows of amended schedules.

## Edge Cases & Limitations

- **Duplicates.** You cannot strike a row that is marked as a duplicate of another row, because duplicates already count for nothing. You also cannot link a struck row as a duplicate, or mark another row as a duplicate of a struck row. Glade refuses the save. When case data sync would create one of these links, it skips that link.
- **Not every questionnaire supports striking yet.** **Amend: Strikethrough** is offered only on the Bankruptcy Schedules questionnaire, and only on rows of a top-level list. A list nested inside another list's row is struck together with its parent row, not row by row. On any other questionnaire — including client questionnaires — the option is not shown, though a row already struck there still shows struck and can be cleared. A new strike is accepted only on questionnaires whose totals are recalculated on the server; otherwise the save is refused and the row is not struck, because those totals would keep counting the row. Clearing a strike, or saving a row whose strike is unchanged, always works.
- **Totals saved before this change.** A total saved before struck rows were excluded can still include a struck row until the questionnaire recalculates.
- Striking is a questionnaire change only. To remove a creditor or asset from the case record, remove it there. See [Case Data Sync](../case-data/case-data-sync.md).

## Related Features

- [Working With Lists](./working-with-lists.md)
- [Creditors](../schedules/creditors.md)
- [Property](../schedules/property.md)
- [Exemptions Calculator](../schedules/exemptions-calculator.md)
- [Chapter 13 Plan Calculator](../schedules/chapter-13-plan-calculator.md)
- [AI Agents](../autofills/ai-agents.md)
- [Case Data Sync](../case-data/case-data-sync.md)
