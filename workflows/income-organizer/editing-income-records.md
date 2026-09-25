# Editing Income Records

## Overview

Your team can enter, correct, and remove the income records behind the Income Organizer — filling in rows the automatic reader has not handled, transcribing paystubs by hand, editing the itemized earnings and deduction lines, correcting extracted values, and removing paystubs or income sources. This doc covers how those edits are recorded and how they flow into the totals.

## Key Behaviors

### Editing a Row That Is Still Queued for Analysis

An uploaded paystub normally has its figures read automatically, but that read can lag, fail, or not have run yet — the row shows as queued for analysis in the meantime. Those rows are editable.

- Open the row and enter the figures from the paystub yourself. There is no need to wait for the automatic read or to re-upload the file. Previously these rows could not be edited at all, so a paystub the reader could not handle was a dead end on the case.
- If the automatic read later succeeds on the same file, it updates the row you filled in rather than adding a second row for the same paystub.
- The **Include in Monthly Totals** and **Include in Means Test** choices already recorded against that upload are carried over, so a file your team had excluded stays excluded.

### Hand-Entered Income Counts Toward the Totals

A month can hold both an automatically read paystub and a figure your team entered by hand — a stub the reader could not make out, for example.

- Records your team entered by hand now count toward Schedule I and the means test alongside the automatically read ones. Previously a hand-entered record was discarded whenever the same month also held an automatically read paystub, so the transcribed figure contributed $0 and both Schedule I and the means test came out low. If your team has transcribed a paystub by hand, re-check that month's figures.
- The same applied to a business or farm month recorded as expenses only, with no income line. Those months are counted too.
- Genuinely empty placeholder rows — no earnings, no overtime, no gross, no expenses — are still left out of the totals, so an empty row does not dilute a month's average.

### After You Edit an Income Record

When you change the individual earnings lines behind a paystub, the pay-period gross is recalculated from the lines you left in place. Everything that reads that figure — the organizer's own table, the income-remaining-after-deductions figure, and Schedule I — reflects the edit straight away. Previously the gross stayed at its pre-edit value, so a corrected paystub still reported the original figure everywhere the summary was used.

### Income Records and Their Source

Every income record is tied to an income source (an employer or a non-employment source) on the case. A record that is not tied to a source contributes $0 to Schedule I and the means test and shows as having incomplete details.

- When a paystub is read before its income source exists on the case — for example, the client uploads before the employer has been added, or the source is configured later — the record is linked to the source as soon as the source appears. Previously the record stayed unlinked indefinitely, quietly contributing nothing to the totals.
- If you see an income record flagged as having incomplete details, confirm the matching income source exists on the case.

### Custom Types in the Income Breakdown

When you edit an income record's breakdown — the individual earnings and deduction lines behind a paystub — each line's type is chosen from a list of the types Glade recognizes for that column.

- Where a column offers more than one type to choose from, the list also includes an **Other (custom)** option. Choosing it reveals a text box so you can type a type that is not on the list — a deduction a particular employer names in its own way, for example.
- The type you type is saved as entered and appears on the breakdown line. Re-opening the record shows your custom type selected, so it is not lost on a later edit.
- A custom type that duplicates a type already used on the record is rejected, so the same deduction cannot be entered twice under two spellings.
- Columns that recognize only a single type keep a fixed list with no custom option, and columns with no predefined types remain free text as before.

Free-text entry was unavailable for a period after the breakdown editor moved to picking from lists. If your team worked around it by folding an unusual deduction into another line, you can record it under its own name again.

### Correcting and Removing Income Sources

- **Correcting an extracted value**: When you edit a paystub field in the Income Organizer that was originally filled by automatic document extraction, your correction becomes the current value for that field. It is no longer flagged as a conflict against the extracted figure, so you don't have to open the conflict view to record a trusted correction. If a later document extraction reads a value that disagrees with your entry, that new value is still held for your review rather than silently overwriting your correction.
- **Re-entering a value that would not hold**: A figure read from a document can be set aside — superseded by a later reading or by a correction elsewhere — which could leave the field with no current value at all. Re-typing the same number then looked like it saved and the field was blank again after a refresh, because Glade treated the entry as identical to the set-aside figure and recorded nothing. Entering the number again now records it as the current value and it survives the refresh. If your team gave up on a field that would not keep what was typed into it, try it again.
- **Removing a paystub**: When you delete a paystub from the Income Organizer, the income data that came from it is removed along with it. A removed paystub no longer lingers as a leftover row in the client's income data.
- **Closing the Add Income Source window**: Adding an employment income source and then closing the window discards the new source only when nothing has been uploaded to it. Once a paystub has been uploaded — or is still uploading — closing the window keeps the source and its paystubs.
  - **Back** is disabled once paystubs exist or are in flight, and hovering it explains why. Use **Close** instead; the source and its paystubs are kept.
  - Closing after an upload refreshes the organizer so the source you just added is visible in the list without a reload.
  - Upload controls are briefly unavailable while Glade confirms what has been uploaded. If that check cannot complete, the source is kept rather than discarded.
  - Previously, closing or going back after uploading paystubs deleted the source and its files without warning. On joint cases this most often hit the second debtor's employment source: the upload appeared to succeed, and the source and its paystubs were gone afterwards with no indication anything had been removed. If your team has lost a Debtor 2 employment source this way, re-add it — the files have to be uploaded again.

### Working Behind the Edit Income Data Panel

**Edit income data** opens as a floating panel you can drag aside, so you can read a paystub or the organizer's own table while entering figures. It behaves that way from the moment it opens: the page behind it scrolls and responds to clicks straight away.

Previously the panel blocked everything behind it until you grabbed its **Drag to move** handle. Until you did, the income table would not scroll and the application read as frozen — with no indication that dragging the panel was what released it. If your team learned to grab the handle first, or avoided the panel on longer income tables, neither is necessary now.

This applies to Glade's draggable panels generally, including the PDF preview panel, all of which are meant to be moved aside and worked alongside rather than dismissed.

## Edge Cases & Limitations

- **Net pay per period is not recalculated after an edit the way gross is.** Editing the earnings lines behind a paystub updates the pay-period gross; the net figure keeps the value it was read or entered with. Check it against the paystub after a substantial edit.

## Related Features

- [Income Organizer](./README.md)
- [Who Can Edit an Organizer](./who-can-edit.md)
- [Including and Excluding Income Records](./including-excluding-records.md)
- [Paystub Extraction](./paystub-extraction.md)
- [Upload Processing Status](./processing-status.md)
- [Document Collection](../document-collection/README.md)
