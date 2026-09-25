# Upload Processing Status

## Overview

Uploaded income documents move through processing states in the Income Organizer — queued for analysis, extracted, settled with no extractable data, or failed. This doc covers how each upload reaches a clear final state, how documents the organizer cannot read are shown, and how older organizers are re-extracted automatically when a workflow is opened.

## Key Behaviors

### Documents With No Extractable Data

Some uploads are classified as a type the Income Organizer cannot pull income figures from — a profit & loss statement dropped into a paystub slot rather than onto a business or rental source, for example. These rows settle into a clear terminal state instead of showing a spinner indefinitely:

- The row shows a muted **"No extracted data"** label with a short explanation, and the processing animation stops.
- Numeric cells show a dash (**—**) rather than **$0.00**, so an empty row is not mistaken for a real zero.
- The **Include in Monthly Totals** and **Include in Means Test** checkboxes are disabled and there is no **Edit** button, so a blank row cannot be pulled into the income or means-test calculations.
- **The row records what the document was recognized as.** Where Glade identified the document but cannot read income figures out of it in that slot, the row keeps the recognized type — so it can be presented as an unsupported document rather than sharing one blank label with a paystub the reader simply could not make out. Rows that settled before this change carry no type; re-run AI on the row to record it.

Regular paystub rows are unaffected — they still show extracted values, a spinner while processing, and editable, selectable controls.

### An Upload Left on "Queued for Analysis"

An upload now leaves the queued-for-analysis state however its reading ends, rather than only when it produces paystub income records.

- **A profit & loss statement settles.** Its figures were read and recorded, but the upload kept showing as pending analysis indefinitely, so the income table looked as though nothing had happened.
- **A read that fails settles too**, as an error you can act on rather than as work that never finished.
- A read that completes with no income figures on it is reported as such instead of being left pending.
- **An upload from someone who belongs to more than one firm reaches the case.** A file uploaded into a document checklist is recorded against the firm that owns the case, not whichever firm the person uploading was working in at the time. Previously that mismatch caused a fully read paystub or profit & loss statement to be discarded after extraction — the figures never reached the income table and nothing on screen said why. If your team has staff who work across more than one firm and uploads that produced nothing, those files are worth re-uploading.

### Automatic Re-extraction on Workflow Load

Some older income organizers may need their paystub data re-extracted (for example, after a backend improvement to how paystub data is read). Glade handles this automatically:

- When you open a workflow containing an income organizer that needs re-extraction, Glade kicks off the re-extraction in the background. You don't need to start it manually.
- A small **"Re-extracting paystubs..."** indicator appears in the corner of the income organizer while the work is in progress, so it's clear something is happening to the rows you're looking at.
- The indicator only shows when there are rows currently being processed. Once all rows finish, the indicator disappears and the updated data appears in the organizer.
- Only paystubs whose data has not already been extracted are re-processed. Paystubs that already have income data are left alone, so opening a workflow does not cause unnecessary re-work.
- If re-extraction fails for any reason, the organizer is left flagged for another attempt — opening the workflow again will retry. You can keep working in the meantime; the re-extraction runs in the background and does not block the rest of the workflow.

## Related Features

- [Income Organizer](./README.md)
- [Paystub Extraction](./paystub-extraction.md)
- [Editing Income Records](./editing-income-records.md) — editing a row that is still queued for analysis
- [Profit & Loss Statements](./business-and-rental-income/profit-and-loss-statements.md)
