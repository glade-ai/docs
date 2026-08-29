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
- **Latest paystub**: bases Schedule I on the current-period figures from one representative paystub, scaled up to a monthly amount using the client's pay frequency. Use this mode when a single recent paystub reflects the client's income better than an average across all stubs or a running year-to-date total — for example after a raise or a change of job.

### Latest Paystub Mode

Latest paystub mode is offered first in the list of calculation methods on an employment income source.

- Glade uses the current-period column of the paystub — gross earnings and every deduction — and converts each figure to a monthly amount from the pay frequency you select. A client paid every two weeks has each current-period figure multiplied by 26 and divided by 12.
- By default the most recent paystub on the case is used. Because the latest stub is sometimes unrepresentative — a short first week, a bonus period, an unpaid absence — you can choose a different paystub as the source instead. A paystub you pick explicitly is eligible even if it carries no date.
- **Pay frequency is required.** Until you select one, no figure is calculated and **Apply** stays disabled. Glade does not assume a frequency.
- A monthly preview shows the resulting figure before you apply it, so you can sanity-check it against the paystub.
- **The means test is not affected.** The Chapter 7 means test always uses the standard six-month calculation, whichever Schedule I mode the source is set to.
- **Existing income sources are not changed.** A source that was already configured keeps the calculation method it was set to. Latest paystub applies to sources you set it on and to new sources created after the firm default is set.

### Firm Default Calculation Method

Your firm can set the calculation method that new employment income sources start with, under **Petition Settings**. New sources are created with that method; existing sources are untouched. The in-organizer checkbox for setting the firm default from the calculator you are working in is still available.

### Where to Set the Calculation Mode

The calculation mode is set from an **Income calculation** action in the income organizer header, available while table view is open. It was previously a small **Calculation:** button tucked inside the Employer cell of each row, which meant opening table view and then finding the right row for something that is set on most cases.

- The header action names the mode currently in effect — for example **Calculation: All Paystubs** or **Calculation: YTD**. When the case's employment sources are set to different modes, it reads **Calculation: Mixed**.
- If the case has more than one employment income source, opening the action asks which source you are setting before showing the settings. With a single employment source it opens straight onto that source's settings.
- Changes are applied with **Apply Changes**, as before. If you switch to a different income source with unapplied changes, Glade asks whether to discard them — declining leaves you on the source you were editing.
- Only employment income sources are listed. Non-employment income (Social Security, rental income, and similar) does not use these modes and is not offered.

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
- **Clearing the switches holds on the first try.** Turning **Include in Monthly Totals** or **Include in Means Test** off — for a whole income source or for one record — sticks, including on organizers with many paystubs and while AI is still reading uploaded documents in the background. Previously rows could re-check themselves moments after being cleared, so the same action had to be repeated several times before it held; that only happened on busy organizers, which is why it looked intermittent. If a change cannot be saved, the switch returns to its previous position and an error message appears, rather than appearing to save and then reverting on the next refresh.

### Feeding Schedule I and the Means Test Questionnaire

An income organizer's calculated results flow into the case's Schedule I and Means Test questionnaire fields, so the figures your team settles in the organizer are the ones the questionnaire shows.

- **New organizers do this from the moment they are created.** Previously a new organizer was created switched off, and its results sat in the organizer without ever reaching the questionnaire until someone had it turned on — so a case could show a complete income organizer alongside blank or stale Schedule I and Means Test answers.
- Organizers created before this change keep whatever setting they are on. If an existing organizer's figures are not reaching the questionnaire, ask Glade support to switch it on for that organizer.
- Only income organizers feed the questionnaire this way. An ordinary document request — a checklist of files to collect — does not.
- A figure the questionnaire has picked up this way can still be overridden by hand on the questionnaire, and the override is kept (see [Questionnaires](./questionnaires.md)).

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

### Means Test Income Window

For the Chapter 7 means test, a debtor's Current Monthly Income is the average of income across the six full calendar months before the month the case is filed. Glade anchors this six-month window to the **last completed calendar month**, so a month that is still in progress is never included.

- A pay stub dated in the current (still-running) month does not pull the window forward or drop the earliest month. For example, a case worked in June averages December through May, not January through June.
- Cases whose most recent pay stub already falls in a prior month are unaffected — the window is not forced to add empty current-month figures, so the average is not artificially lowered.
- Income sources that do not count toward the means test — Social Security and government assistance (such as welfare or food stamps) — are left out of the six-month average. They also do not anchor the window, so a benefit entry dated in the current (still-running) month does not pull the window forward and drop an earlier month. Previously a current-month government-assistance entry could shift the window forward and drop the earliest month's paychecks, understating the gross monthly income; excluded sources no longer affect the window. These sources still count where they belong elsewhere, such as on Schedule I.

This applies to the standard six-month means test calculation. You can still choose to apply a single employer's year-to-date figures, or the YTD period method, to the means test instead; see [Document Collection](./document-collection.md).

### Long-Form Means Test Deductions

The means test deduction lines — taxes, involuntary deductions, life insurance, court-ordered payments, health care and HSA contributions, and (on Chapter 13) mandatory retirement — are calculated from the paystubs on the case instead of being typed in by hand. The figures reach the deduction lines of **Form 122A-2** (Chapter 7) and **Form 122C-2** (Chapter 13).

- The amounts are worked out from the same paystubs the organizer already holds, averaged by month the way Schedule I figures are. Records excluded from the means test, and non-means-test income such as Social Security, are left out.
- Figures appear on the forms after the organizer recalculates. Adding a paystub or correcting one and recalculating brings the deduction lines with it.
- This is separate from the current monthly income calculation that fills Forms 122A-1 and 122C-1. That calculation is unchanged; the deduction lines are what is new.
- **Mandatory retirement is counted once.** It is applied to the deduction line for it and is not also subtracted further down the Chapter 13 form, so disposable income is not reduced twice for the same contribution.
- On the questionnaire, these fields name the long form means test calculator as their source. Overriding one by hand sticks through later recalculations — see [Questionnaires](./questionnaires.md).

Lines the paystubs cannot answer are left blank rather than filled with `$0.00`, so a line you still need to answer is visibly unanswered instead of reading as a zero somebody meant.

### Two Paystubs With the Same Pay Date

A client can have more than one distinct paystub carrying the same pay date — a regular check plus a bonus, or a correction issued the same day. All of them are kept.

- Each uploaded document appears as its own row. Previously only one of them survived, and the others stayed in the queued-for-analysis bucket indefinitely even though Glade had already read them.
- Because the row that survived was picked afresh on each load, Schedule I figures could change on their own from one refresh to the next. They no longer do.
- Re-reading the same document still updates its existing row rather than adding a second one, so a re-upload or a re-run of the extraction does not double a month.

If your team has an organizer where paystubs stayed stuck on **Queued for analysis** after extraction finished, re-open it — the affected stubs appear as ordinary rows, and the month's Schedule I figure should be re-checked, since it was previously calculated from only one of them.

### Chapter 7 Median Income Screen

The median income screen compares the client's annualized current monthly income directly against the household median income for their state and family size — deductions are not subtracted from this comparison. The result is shown clearly:

- A green check with the amount the client is **under** the median, per month, when income is below median.
- A red X with the amount the client is **over** the median, per month, when income is above median.
- The corresponding annual over/under amount is shown alongside the monthly figure.

Amounts of zero display as `$0.00` rather than a dash. When income or median data is missing, the screen shows a neutral state instead of a pass or fail.

### Paystub Data Extraction

When a paystub document is uploaded to a case, Glade extracts income fields automatically. YTD fields (such as year-to-date gross pay and year-to-date overtime) are used when the income source is set to YTD mode.

On paystubs that print current-period and year-to-date figures side by side, the two columns are kept apart: the pay-period gross is read from the current-period column and the year-to-date gross from the YTD column. Previously a year-to-date total could be recorded as the pay-period gross while the YTD figure was left blank, which showed income amounts that did not match the paystub and could overstate the monthly averages carried onto Schedule I and the means test.

When Glade reads a paystub on its own — on upload, on a re-read, or during a background catch-up — the itemized breakdown it extracts is kept. Individual earnings lines and individual deduction lines stay as separate entries. Previously an automatic read also wrote its column totals back over that breakdown, collapsing the itemized lines into a single total and sometimes leaving a stray "other" post-tax deduction entry that was not on the paystub. Figures your team enters or corrects by hand — including months and income items you add yourself — continue to update the income data as before.

**Deductions printed in two columns.** Some paystubs — government back-pay stubs are the common case — list each deduction twice, once as the current pay period amount and once as an adjusted amount. Glade adds the two together for each deduction rather than reading only the current column. Previously the adjusted column was ignored, which understated the client's total deductions and, on the Chapter 7 means test, overstated the income remaining after them.

**Year-to-date gross when a bonus is listed separately.** On paystubs that print a bonus on its own line outside the year-to-date earnings subtotal, the year-to-date gross is taken as the subtotal shown on the stub. Previously the pay period's bonus could be added on top of a subtotal that already accounted for it, inflating year-to-date gross — and, for any employer set to YTD mode, every monthly figure derived from it.

**Values still awaiting your review are not counted.** When a figure read from a document disagrees with what is already on the case, it is held for your team to review rather than applied (see [Document Collection](./document-collection.md)). The Income Organizer's figures use confirmed values only — a value sitting in review, or one your team has already rejected or replaced with a correction, does not feed the totals. Previously the organizer could pick up a pending value while the rest of the case used the confirmed one, so the same figure read differently in two places.

### Custom Types in the Income Breakdown

When you edit an income record's breakdown — the individual earnings and deduction lines behind a paystub — each line's type is chosen from a list of the types Glade recognizes for that column.

- Where a column offers more than one type to choose from, the list also includes an **Other (custom)** option. Choosing it reveals a text box so you can type a type that is not on the list — a deduction a particular employer names in its own way, for example.
- The type you type is saved as entered and appears on the breakdown line. Re-opening the record shows your custom type selected, so it is not lost on a later edit.
- A custom type that duplicates a type already used on the record is rejected, so the same deduction cannot be entered twice under two spellings.
- Columns that recognize only a single type keep a fixed list with no custom option, and columns with no predefined types remain free text as before.

Free-text entry was unavailable for a period after the breakdown editor moved to picking from lists. If your team worked around it by folding an unusual deduction into another line, you can record it under its own name again.

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

### Working Behind the Edit Income Data Panel

**Edit income data** opens as a floating panel you can drag aside, so you can read a paystub or the organizer's own table while entering figures. It behaves that way from the moment it opens: the page behind it scrolls and responds to clicks straight away.

Previously the panel blocked everything behind it until you grabbed its **Drag to move** handle. Until you did, the income table would not scroll and the application read as frozen — with no indication that dragging the panel was what released it. If your team learned to grab the handle first, or avoided the panel on longer income tables, neither is necessary now.

This applies to Glade's draggable panels generally, including the PDF preview panel, all of which are meant to be moved aside and worked alongside rather than dismissed.

### Automatic Re-extraction on Workflow Load

Some older income organizers may need their paystub data re-extracted (for example, after a backend improvement to how paystub data is read). Glade handles this automatically:

- When you open a workflow containing an income organizer that needs re-extraction, Glade kicks off the re-extraction in the background. You don't need to start it manually.
- A small **"Re-extracting paystubs..."** indicator appears in the corner of the income organizer while the work is in progress, so it's clear something is happening to the rows you're looking at.
- The indicator only shows when there are rows currently being processed. Once all rows finish, the indicator disappears and the updated data appears in the organizer.
- Only paystubs whose data has not already been extracted are re-processed. Paystubs that already have income data are left alone, so opening a workflow does not cause unnecessary re-work.
- If re-extraction fails for any reason, the organizer is left flagged for another attempt — opening the workflow again will retry. You can keep working in the meantime; the re-extraction runs in the background and does not block the rest of the workflow.

### Who Can Edit an Organizer

Editing an income organizer is open to your firm's staff, not only to whoever opened the case. Firm-side team members and anyone explicitly assigned as a collaborator on the workflow can:

- open the **Income calculation** and **Calculators** controls in the table view header;
- edit an extracted paystub row and the breakdown behind a value; and
- change the per-record **Count toward Schedule I** and **Count toward means test** settings.

Clients, and members of a client organization who have access to the case, stay read-only. They can see the organizer but cannot change extracted figures or calculation settings.

Previously these controls were limited to the case's creator, so a paralegal assigned to the case could open the organizer but had no way to correct a misread figure — the work had to go back to whoever created the case.

## Configuration

| Setting | Description |
|---------|-------------|
| Calculation mode | Per-paycheck, YTD, YTD period method, or latest paystub, set per employment income source from the **Income calculation** action in the organizer header (table view) |
| Default calculation mode for new sources | Set firm-wide under Petition Settings. Applies to employment income sources created afterwards; existing sources keep their own setting |
| Filing (test) month | For the YTD period method, sets the month whose preceding six full months form the period being measured |
| Source paystub | For latest paystub mode, which paystub the current-period figures are read from. Defaults to the most recent stub on the case |
| Pay frequency | Used to convert YTD amounts to monthly figures (e.g., weekly = 52 periods/year) |
| Count toward Schedule I | Whether an individual income record is included in the Schedule I figure. Set per record; preserved when the document is read again |
| Count toward means test | Whether an individual income record is included in the means test. Set per record; preserved when the document is read again |

## Edge Cases & Limitations

- If a paystub does not include YTD overtime data, overtime shows as $0 in YTD mode — no error is shown. This is expected for clients without overtime.
- The Schedule I Contributions preview reflects the current saved state of the income sources. If you have made changes without saving, save first before reviewing the preview.
- YTD calculations depend on accurate pay period counts. If the number of pay periods elapsed is incorrect, monthly figures will be off proportionally.
- Paystubs extracted before the current/year-to-date column handling was corrected are not re-read automatically. If an existing row shows a year-to-date figure in its pay-period gross, re-run extraction on that row or correct the extracted data by hand.
- The debtor badge on an organizer's detail page only appears when the case has more than one income organizer. A single-organizer case shows no badge, which is not an indication that the organizer is unlabeled.
- Latest paystub mode produces no figure at all when the pay frequency is missing, rather than assuming one. Select the frequency to calculate.
- Latest paystub mode affects Schedule I only. It is not available for the means test, which always uses the standard six-month calculation.
- Income sources configured before latest paystub mode existed continue to use the method they were set to. They are not migrated automatically.
- The same applies to the two-column deduction and year-to-date bonus corrections: rows extracted beforehand keep the figures they were read with. On a case where the client's paystubs carry an adjusted deduction column or a separately-listed bonus, re-run extraction on those rows before relying on the deduction totals or the year-to-date gross.
- **Net pay per period is not recalculated after an edit the way gross is.** Editing the earnings lines behind a paystub updates the pay-period gross; the net figure keeps the value it was read or entered with. Check it against the paystub after a substantial edit.
- Switching a new income organizer's results through to the Schedule I and Means Test questionnaire happens automatically only for organizers created from this point on. Older organizers are not switched on retroactively.
- The YTD period method needs paystubs whose year-to-date sections bracket the chosen period. If there aren't enough anchoring paystubs, the method can't be applied and you'll be prompted to upload paystubs that bracket the window. The method always divides the bracketed gross by six months. Periods that cross a calendar-year boundary, and a July filing month, are handled as special cases.
- **A July filing month is measured against the end of June.** The six-month window for a July filing is January through June, and because year-to-date figures have not reset by then, the whole window can be read off a single paystub. Glade uses the last June paystub's year-to-date gross for this. Where there is no June paystub to read, it works back from the latest July stub by removing **every** July pay period from the year-to-date figure. Previously only one July pay period was removed, so on a case with more than one July paystub — biweekly pay, most often — the earlier July paychecks stayed inside the January-to-June total and the monthly gross on Schedule I came out too high. Organizers calculated before this was corrected keep the figures they were given; re-run the calculation on an affected July source to pick up the corrected figure.

- The long-form means test deduction lines are calculated for the household as a whole, which is what Forms 122A-2 and 122C-2 ask for. They are not broken out per debtor on the forms.
- Deduction lines the paystubs do not answer are left blank. A blank line is not a calculated zero — check it against the case before filing.
- Deduction figures appear only after the organizer recalculates. An organizer that has not been recalculated since these lines existed shows them empty; recalculate it to fill them.

> TODO: Document how to open the Income Organizer from a workflow, how to add income sources, and how to mark the organizer complete.

## Related Features

- [Questionnaires](./questionnaires.md)
- [Exemptions Calculator](./exemptions-calculator.md)
