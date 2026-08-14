# Income Organizer

## Overview

The Income Organizer is a tool in bankruptcy workflows that helps attorneys review and organize a client's income data for court form preparation. It collects income from paystubs and other sources, calculates monthly amounts, and feeds the results into bankruptcy schedules — Schedule I (Current Monthly Income of the Debtor) and the Chapter 7 means test, including the median income screen.

## Key Behaviors

### More Than One Organizer on a Case

A case can carry more than one income organizer — typically one for the primary debtor and a second for a joint debtor or a non-filing spouse. Every organizer on the case is now visible and usable, where previously only the first one could be reached.

- Where a questionnaire offers **Source Data** links, each organizer appears as its own labeled entry (for example, *Income Organizer · Pay Organizer (Debtor 1)*). Opening an entry takes you to that organizer. A case with only one organizer shows a single unlabeled link, exactly as before.
- On an organizer's detail page, a badge names whose income it holds — **Primary**, **Debtor 2**, or **Non-filing spouse**. The badge only appears when the case has more than one organizer, so single-organizer cases are unchanged.
- Importing income into a questionnaire is not limited to one organizer. The import pulls from every income organizer on the case, so a joint case fills both Schedule I columns from a single import.

Before this, an attorney could not see or add income for a non-filing spouse even after a second organizer existed on the case — the interface showed only the first one it found.

### Income Calculation Modes

Each income source (such as a paystub) can be set to one of these calculation modes:

- **Per-paycheck mode**: income amounts are taken directly from individual pay period values.
- **YTD (year-to-date) mode**: monthly amounts are derived by dividing the year-to-date totals by the number of pay periods elapsed. Use this mode when per-period figures are unavailable or less accurate than the running YTD totals.
- **YTD period method**: estimates average monthly income by comparing the year-to-date totals on the paystubs that bracket a chosen six-month period, then dividing the bracketed gross by six. You pick a **filing (test) month**, and Glade treats the six full months before that month as the period to measure. Use this mode to base the figure on a defined window rather than on the full running year-to-date total.

### Period Method Preview

When you choose the YTD period method, a preview shows how the figure is built before you apply it: the filing month you selected, the six-month period that falls before it, how many paystubs were used as the start and end anchors, the breakdown rows that make up the calculation, and the resulting monthly gross. The filing month defaults to the month after the latest paystub that carries year-to-date data, and you can change it.

If you also apply the period method to the means test, a warning banner flags it as a non-standard calculation method so you can confirm it against the case's requirements before relying on it.

### Schedule I Contributions Preview

From within the income organizer, you can open a **Schedule I Contributions** preview that shows how the collected income will appear on Schedule I before the form is generated.

When a paystub is in YTD mode and includes overtime pay:

- **Wages / Salary** and **Overtime** appear as separate line items, showing the monthly breakdown derived from YTD data.
- A **Gross Income** summary row shows the total (wages + overtime), so the additive relationship is visible at a glance.
- This matches what will be reported on Schedule I, where wages and overtime are listed separately.

In per-paycheck mode, amounts are taken directly from the pay period figures.

### How the Schedule I Monthly Figure Is Averaged

Schedule I reports a monthly figure, so Glade groups the collected income by calendar month and averages the monthly totals — it does not divide the total by the number of paystubs collected.

- For a client paid every two weeks, the two (or three) paychecks that fall in the same month are added together first, and the monthly figure is the average of those monthly totals. Previously the figure was the total divided by the paystub count, which reported roughly one paycheck as a month of income and understated Schedule I for anyone not paid monthly.
- Non-employment income is grouped the same way. When more than one document is attached to the same non-employment source, the amounts for that source are added together within each month rather than treated as separate sources.
- Clients paid monthly are unaffected — one paystub per month means the two methods produce the same figure.

If you have reviewed a Schedule I figure that was calculated before this change, re-check it against the paystubs on the case: the corrected figure is generally higher for clients paid weekly, biweekly, or semi-monthly.

### Including and Excluding Income Records

Each income record carries its own switches for whether it counts toward Schedule I and whether it counts toward the means test. Turning one off is a deliberate choice your team makes about that record, and Glade preserves it:

- Excluding a record stays excluded when the underlying document is read again — for example after a re-upload, a re-run of the extraction, or an automatic background retry. Previously any re-read of the document silently switched the record back to counted, in both the income organizer and the means test, so a record your team had deliberately left out could reappear in the totals without anyone changing it.
- A first-time extraction still starts with the record counted, and a document Glade could not read keeps its record out of the totals until a later successful read.

### Income Records and Their Source

Every income record is tied to an income source (an employer or a non-employment source) on the case. A record that is not tied to a source contributes $0 to Schedule I and the means test and shows as having incomplete details.

- When a paystub is read before its income source exists on the case — for example, the client uploads before the employer has been added, or the source is configured later — the record is linked to the source as soon as the source appears. Previously the record stayed unlinked indefinitely, quietly contributing nothing to the totals.
- If you see an income record flagged as having incomplete details, confirm the matching income source exists on the case.

### Means Test Income Window

For the Chapter 7 means test, a debtor's Current Monthly Income is the average of income across the six full calendar months before the month the case is filed. Glade anchors this six-month window to the **last completed calendar month**, so a month that is still in progress is never included.

- A pay stub dated in the current (still-running) month does not pull the window forward or drop the earliest month. For example, a case worked in June averages December through May, not January through June.
- Cases whose most recent pay stub already falls in a prior month are unaffected — the window is not forced to add empty current-month figures, so the average is not artificially lowered.
- Income sources that do not count toward the means test — Social Security and government assistance (such as welfare or food stamps) — are left out of the six-month average. They also do not anchor the window, so a benefit entry dated in the current (still-running) month does not pull the window forward and drop an earlier month. Previously a current-month government-assistance entry could shift the window forward and drop the earliest month's paychecks, understating the gross monthly income; excluded sources no longer affect the window. These sources still count where they belong elsewhere, such as on Schedule I.

This applies to the standard six-month means test calculation. You can still choose to apply a single employer's year-to-date figures, or the YTD period method, to the means test instead; see [Document Collection](./document-collection.md).

### Chapter 7 Median Income Screen

The median income screen compares the client's annualized current monthly income directly against the household median income for their state and family size — deductions are not subtracted from this comparison. The result is shown clearly:

- A green check with the amount the client is **under** the median, per month, when income is below median.
- A red X with the amount the client is **over** the median, per month, when income is above median.
- The corresponding annual over/under amount is shown alongside the monthly figure.

Amounts of zero display as `$0.00` rather than a dash. When income or median data is missing, the screen shows a neutral state instead of a pass or fail.

### Paystub Data Extraction

When a paystub document is uploaded to a case, Glade extracts income fields automatically. YTD fields (such as year-to-date gross pay and year-to-date overtime) are used when the income source is set to YTD mode.

On paystubs that print current-period and year-to-date figures side by side, the two columns are kept apart: the pay-period gross is read from the current-period column and the year-to-date gross from the YTD column. Previously a year-to-date total could be recorded as the pay-period gross while the YTD figure was left blank, which showed income amounts that did not match the paystub and could overstate the monthly averages carried onto Schedule I and the means test.

### Correcting and Removing Income Sources

- **Correcting an extracted value**: When you edit a paystub field in the Income Organizer that was originally filled by automatic document extraction, your correction becomes the current value for that field. It is no longer flagged as a conflict against the extracted figure, so you don't have to open the conflict view to record a trusted correction. If a later document extraction reads a value that disagrees with your entry, that new value is still held for your review rather than silently overwriting your correction.
- **Removing a paystub**: When you delete a paystub from the Income Organizer, the income data that came from it is removed along with it. A removed paystub no longer lingers as a leftover row in the client's income data.
- **Closing the Add Income Source window**: Adding an employment income source and then closing the window discards the new source only when nothing has been uploaded to it. Once a paystub has been uploaded — or is still uploading — closing the window keeps the source and its paystubs.
  - **Back** is disabled once paystubs exist or are in flight, and hovering it explains why. Use **Close** instead; the source and its paystubs are kept.
  - Closing after an upload refreshes the organizer so the source you just added is visible in the list without a reload.
  - Upload controls are briefly unavailable while Glade confirms what has been uploaded. If that check cannot complete, the source is kept rather than discarded.
  - Previously, closing or going back after uploading paystubs deleted the source and its files without warning. On joint cases this most often hit the second debtor's employment source: the upload appeared to succeed, and the source and its paystubs were gone afterwards with no indication anything had been removed. If your team has lost a Debtor 2 employment source this way, re-add it — the files have to be uploaded again.

### Documents With No Extractable Data

Some uploads are classified as a type the Income Organizer cannot pull income figures from — for example, a profit-and-loss statement dropped into an income slot. These rows settle into a clear terminal state instead of showing a spinner indefinitely:

- The row shows a muted **"No extracted data"** label with a short explanation, and the processing animation stops.
- Numeric cells show a dash (**—**) rather than **$0.00**, so an empty row is not mistaken for a real zero.
- The **Include in Monthly Totals** and **Include in Means Test** checkboxes are disabled and there is no **Edit** button, so a blank row cannot be pulled into the income or means-test calculations.

Regular paystub rows are unaffected — they still show extracted values, a spinner while processing, and editable, selectable controls.

### Automatic Re-extraction on Workflow Load

Some older income organizers may need their paystub data re-extracted (for example, after a backend improvement to how paystub data is read). Glade handles this automatically:

- When you open a workflow containing an income organizer that needs re-extraction, Glade kicks off the re-extraction in the background. You don't need to start it manually.
- A small **"Re-extracting paystubs..."** indicator appears in the corner of the income organizer while the work is in progress, so it's clear something is happening to the rows you're looking at.
- The indicator only shows when there are rows currently being processed. Once all rows finish, the indicator disappears and the updated data appears in the organizer.
- Only paystubs whose data has not already been extracted are re-processed. Paystubs that already have income data are left alone, so opening a workflow does not cause unnecessary re-work.
- If re-extraction fails for any reason, the organizer is left flagged for another attempt — opening the workflow again will retry. You can keep working in the meantime; the re-extraction runs in the background and does not block the rest of the workflow.

## Configuration

| Setting | Description |
|---------|-------------|
| Calculation mode | Per-paycheck, YTD, or YTD period method, set per income source |
| Filing (test) month | For the YTD period method, sets the month whose preceding six full months form the period being measured |
| Pay frequency | Used to convert YTD amounts to monthly figures (e.g., weekly = 52 periods/year) |
| Count toward Schedule I | Whether an individual income record is included in the Schedule I figure. Set per record; preserved when the document is read again |
| Count toward means test | Whether an individual income record is included in the means test. Set per record; preserved when the document is read again |

## Edge Cases & Limitations

- If a paystub does not include YTD overtime data, overtime shows as $0 in YTD mode — no error is shown. This is expected for clients without overtime.
- The Schedule I Contributions preview reflects the current saved state of the income sources. If you have made changes without saving, save first before reviewing the preview.
- YTD calculations depend on accurate pay period counts. If the number of pay periods elapsed is incorrect, monthly figures will be off proportionally.
- Paystubs extracted before the current/year-to-date column handling was corrected are not re-read automatically. If an existing row shows a year-to-date figure in its pay-period gross, re-run extraction on that row or correct the extracted data by hand.
- The debtor badge on an organizer's detail page only appears when the case has more than one income organizer. A single-organizer case shows no badge, which is not an indication that the organizer is unlabeled.
- The YTD period method needs paystubs whose year-to-date sections bracket the chosen period. If there aren't enough anchoring paystubs, the method can't be applied and you'll be prompted to upload paystubs that bracket the window. The method always divides the bracketed gross by six months. Periods that cross a calendar-year boundary, and a July filing month, are handled as special cases.

> TODO: Document how to open the Income Organizer from a workflow, how to add income sources, and how to mark the organizer complete.

## Related Features

- [Questionnaires](./questionnaires.md)
- [Exemptions Calculator](./exemptions-calculator.md)
