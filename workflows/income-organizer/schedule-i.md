# Schedule I

## Overview

The Income Organizer's calculated results feed Schedule I (Current Monthly Income of the Debtor). This doc covers how the monthly Schedule I figure is averaged, how it can be previewed, how Social Security and other non-employment income are reported on their lines, and how organizer results reach the Schedule I and Means Test questionnaire fields. Business and rental income (line 8a) is covered in [Business and Rental Income](./business-and-rental-income/README.md).

## Key Behaviors

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

### Social Security Benefit Types

When you add a Social Security income source, Glade asks which benefit it is — retirement, SSDI, SSI, survivor, spousal, child, disabled adult child, or other. The type is required: the button that creates the source stays disabled until one is chosen.

- Recording the type keeps several Social Security benefits on the same case distinguishable, so a client drawing both a retirement benefit and a survivor benefit reads clearly in the organizer rather than showing two entries with the same name.
- **The figures do not change.** Every Social Security source still adds into the single Schedule I line for Social Security (line 8e), and all of it stays out of the means test.
- Sources recorded before benefit types existed keep working as they are. They carry no type and continue to report on the same Schedule I line.

### Government Assistance and Other Income on Schedule I Lines 8f and 8h

Schedule I reports other government assistance on line 8f and other monthly income on line 8h, each as a single description and amount per debtor. Alongside those totals, Glade records each source behind them individually, so the bankruptcy schedules questionnaire can show the list of sources a line is made up of.

- One entry per source that counts toward Schedule I, kept separately for each debtor and each line. Changing a source from other income to government assistance moves its entry to the line it now belongs to.
- **The totals are unchanged.** Lines 8f and 8h, the Schedule I totals, and the means test still read the same summed figures they always did.
- Deleting a source, or turning it off for Schedule I, removes its entry.
- See [Questionnaires](../questionnaires/README.md) for how the list appears on the form.

### Feeding Schedule I and the Means Test Questionnaire

An income organizer's calculated results flow into the case's Schedule I and Means Test questionnaire fields, so the figures your team settles in the organizer are the ones the questionnaire shows.

- **New organizers do this from the moment they are created.** Previously a new organizer was created switched off, and its results sat in the organizer without ever reaching the questionnaire until someone had it turned on — so a case could show a complete income organizer alongside blank or stale Schedule I and Means Test answers.
- Organizers created before this change keep whatever setting they are on. If an existing organizer's figures are not reaching the questionnaire, ask Glade support to switch it on for that organizer.
- Only income organizers feed the questionnaire this way. An ordinary document request — a checklist of files to collect — does not.
- A figure the questionnaire has picked up this way can still be overridden by hand on the questionnaire, and the override is kept (see [Questionnaires](../questionnaires/README.md)).

## Edge Cases & Limitations

- The Schedule I Contributions preview reflects the current saved state of the income sources. If you have made changes without saving, save first before reviewing the preview.
- The individual Schedule I 8f and 8h entries are recorded only on cases that use case data sync. The summed amounts on those lines fill either way.
- Switching a new income organizer's results through to the Schedule I and Means Test questionnaire happens automatically only for organizers created from this point on. Older organizers are not switched on retroactively.

## Related Features

- [Income Organizer](./README.md)
- [Income Calculation Modes](./calculation-modes.md)
- [Means Test](./means-test.md)
- [Including and Excluding Income Records](./including-excluding-records.md)
- [Business and Rental Income](./business-and-rental-income/README.md)
- [Questionnaires](../questionnaires/README.md)
