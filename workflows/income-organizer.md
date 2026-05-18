# Income Organizer

## Overview

The Income Organizer is a tool in bankruptcy workflows that helps attorneys review and organize a client's income data for court form preparation. It collects income from paystubs and other sources, calculates monthly amounts, and feeds the results into bankruptcy schedules — primarily Schedule I (Current Monthly Income of the Debtor).

## Key Behaviors

### Income Calculation Modes

Each income source (such as a paystub) can be set to one of two calculation modes:

- **Per-paycheck mode**: income amounts are taken directly from individual pay period values.
- **YTD (year-to-date) mode**: monthly amounts are derived by dividing the year-to-date totals by the number of pay periods elapsed. Use this mode when per-period figures are unavailable or less accurate than the running YTD totals.

### Schedule I Contributions Preview

From within the income organizer, you can open a **Schedule I Contributions** preview that shows how the collected income will appear on Schedule I before the form is generated.

When a paystub is in YTD mode and includes overtime pay:

- **Wages / Salary** and **Overtime** appear as separate line items, showing the monthly breakdown derived from YTD data.
- A **Gross Income** summary row shows the total (wages + overtime), so the additive relationship is visible at a glance.
- This matches what will be reported on Schedule I, where wages and overtime are listed separately.

In per-paycheck mode, amounts are taken directly from the pay period figures.

### Paystub Data Extraction

When a paystub document is uploaded to a case, Glade extracts income fields automatically. YTD fields (such as year-to-date gross pay and year-to-date overtime) are used when the income source is set to YTD mode.

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
| Calculation mode | Per-paycheck or YTD, set per income source |
| Pay frequency | Used to convert YTD amounts to monthly figures (e.g., weekly = 52 periods/year) |

## Edge Cases & Limitations

- If a paystub does not include YTD overtime data, overtime shows as $0 in YTD mode — no error is shown. This is expected for clients without overtime.
- The Schedule I Contributions preview reflects the current saved state of the income sources. If you have made changes without saving, save first before reviewing the preview.
- YTD calculations depend on accurate pay period counts. If the number of pay periods elapsed is incorrect, monthly figures will be off proportionally.

> TODO: Document how to open the Income Organizer from a workflow, how to add income sources, and how to mark the organizer complete.

## Related Features

- [Questionnaires](./questionnaires.md)
- [Exemptions Calculator](./exemptions-calculator.md)
