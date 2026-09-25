# Manual Overrides

## Overview

An answer a person typed is treated as an input to the form, not as something Glade works out. This page covers how hand-entered values are protected from autofills and calculations — on ordinary fields, inside list and table rows, and on the Schedule I and Means Test lines the Income Organizer calculates — and how to hand a field back to its autofill.

## Key Behaviors

### A Value You Typed Is Not Re-Derived

No automatic run — a calculation, an autofill, or a value mirrored from another field — replaces an answer a person typed.

- **An override survives a save and a reload.** Previously the protection only held for as long as you had the form open. Once the questionnaire had been saved, a correction read as an ordinary value again, and the next time anything it depended on changed, the calculation took the field back: the figure changed, the indicator flipped from **Manually overridden** back to autofilled, and nothing recorded that a person had ever typed there.
- The clearest case was a total over a long list. A paralegal correcting the Schedule J monthly expense total would keep their figure until somebody edited any one of the 35 expense lines underneath it — at which point the total was silently recalculated over the correction. The same shape applied to any calculated field with an override on it.
- **Re-run is how you ask for the calculation back.** Using the re-run control on the field deliberately replaces your value with the current derived one and hands the field back to the autofill, exactly as before. That is the only way an automatic value now lands on a field somebody typed into.
- **A field nobody has answered is unaffected.** Empty fields autofill as normal — the protection applies to answers that were actually supplied.
- **A locked field is still the exception.** Locking declares the field to belong to its autofill, so a locked field keeps updating regardless — see [Locked Fields](./locked-fields.md).

Two related problems were fixed at the same time, both of which could quietly freeze a field:

- **Saving the form no longer marks untouched fields as hand-entered.** A save re-sends the whole form, and fields whose answers had not moved were being recorded as though someone had typed them. A field marked that way would never autofill again, without anyone having touched it.
- **A sync that produces no value no longer writes anything.** Bringing case data into the form used to stamp a field even when it had nothing to put there, with the same effect.

If a field on an older case is not autofilling and you cannot see why, re-run the autofill on it.

### Autofills and Values You Typed in List and Table Rows

Glade does not replace a value you entered by hand with an autofilled one. That protection applies to fields inside list and table rows — creditors, properties, income lines — as it does everywhere else on the form. It had stopped working there:

- **An autofill could overwrite a value your team typed into a list or table row.** Glade failed to recognise the row's existing value as manually entered and treated the field as empty and therefore safe to fill. Every list and table field was affected. A figure a paralegal had corrected could be quietly replaced by an autofilled one, with nothing in the form to indicate the correction had been lost.
- **A value calculated for one row could be written into a different row.** With a row's detail view open, an autofill computed for another row could land on the open row's field instead, overwriting whatever was there — including a manually entered value, which was never checked before the write. Values computed for any row other than the one you have open are now skipped rather than redirected, so a value never lands on a row it was not calculated for.

Both were silent. If your team reviewed list or table data and found figures that did not match what was entered, the values are worth re-checking against the source documents; nothing was flagged at the time.

Manual edits to fields in a list also stick when an AI agent auto-runs after rows have been added, removed, or reordered — see [AI Agents](./ai-agents.md).

### Overriding a Schedule I or Means Test figure the calculator produced

The Schedule I and Means Test lines the Income Organizer calculates are handled differently from ordinary case data sync fields, because an attorney's correction to one of them needs to survive the next recalculation.

- These fields name the calculator as their source rather than reading **Synced with case data**.
- **A figure you type over sticks.** The field reads **Manually overridden**, and a later Income Organizer recalculation leaves it alone. Previously the most recent recalculation won, so a correction an attorney made could be replaced without warning the next time income figures changed.
- **Re-run is always available on these fields**, whether or not you have edited them. Using it puts the calculator's current output back on the field and hands the line back to the calculator, so a later recalculation updates it again.
- Because these figures are calculated rather than stored on the case record, the re-run control replaces the case data view on them — there is no case record entry behind the line to open.
- Ordinary case data sync fields are unchanged: editing one still leaves it on case data with the usual revert option.

The deduction lines on the long-form means test — Form 122A-2 (Chapter 7) and Form 122C-2 (Chapter 13) — name the **long form means test calculator** as their source, separately from the current monthly income lines on Forms 122A-1 and 122C-1, which name the means test calculator. The two are different calculations and reading which one filled a line matters when you are checking a figure against the paystubs. These lines previously read **Synced with case data**, which pointed at a case record entry that does not exist for them. A figure you type over on one of them reads **Manually overridden** and still names the calculator behind it, and **Re-run** behaves as it does on the other calculator lines.

**Import Data from Income Organizer** deliberately overrides hand-edited calculator figures — see [Schedule I and Income](../schedules/income.md#importing-income-organizer-figures).

## Edge Cases & Limitations

- A figure that was overwritten on an earlier case, before overrides were protected across saves, is not restored. Nothing on the field recorded the value that was replaced. Re-check calculated totals on cases where a correction was made and may have been lost.
- Re-saving a form does not, on its own, un-freeze a field that an older save had marked as hand-entered. Re-run the autofill on the field to hand it back.
- Locking a field is the one case where an autofill overwrites an answer someone typed. See [Locked Fields](./locked-fields.md).

## Related Features

- [Questionnaires](../README.md)
- [Autofills](./README.md)
- [How Autofills Work](./how-autofills-work.md)
- [Autofill Status Indicators](./status-indicators.md)
- [Locked Fields](./locked-fields.md)
- [Schedule I and Income](../schedules/income.md)
- [Means Test](../schedules/means-test.md)
- [Income Organizer](../../income-organizer/README.md)
