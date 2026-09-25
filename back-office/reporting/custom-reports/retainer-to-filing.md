# Time from Retainer to Filing

## Overview

A case report can measure how long each case took to get from its first signed retainer to the day it was filed, and roll those intervals up into an average and a median for the firm. The measurement can be broken down over time by week, month, or quarter.

## Key Behaviors

### Columns and measurement

- Two columns are available: **first retainer signed**, the date the earliest retainer on the case was signed, and **days to filing**, the number of calendar days from that date to the date the case was filed. Both are included in the report's CSV export when you select them.
- The interval is measured in **calendar days**, including weekends and court holidays. A case retained and filed on the same day counts as **0 days**, not as blank.
- The starting point is the **earliest** retainer signature across every workflow linked to the case, not the retainer on the row you are looking at. A client who signed one retainer at consultation and another when a second matter was opened is measured from the first signature.
- The earliest signature is found regardless of how you have filtered the report. Narrowing a report to a particular retainer type changes which cases are returned, not which signature each case is measured from.
- The measurement belongs to the case rather than to a workflow, so a case is counted once however many linked workflows sit under it.
- A retainer that was deleted, or one whose signing step was skipped, is not counted. The earliest remaining signed retainer is used.
- The filing date is the one recorded on the case, the same date the report's filed column shows.
- Days are counted in your firm's time zone, so the interval matches the dates your team sees on the case. A firm with no time zone configured falls back to UTC — see [Settings](../../settings.md).

### Average, median, and breakdowns

- Alongside the columns, the report gives an **average** and a **median** number of days with a count of the cases behind them, both overall and broken down by **month** or by **quarter**. Cases fall into a month or quarter by the date they were filed.
- The overall average and median are calculated across the cases themselves rather than by averaging the monthly figures, so a month with three cases does not carry the same weight as a month with three hundred.
- The report can be narrowed to **only the cases that have a measured interval**, which is how you get to the case list behind an average without a mix of measured and unmeasured cases in it.

Two groups of cases are counted and reported separately instead of being folded into the average:

- **Cases missing one of the two dates** — no signed retainer, or no filing date. This is what keeps cases imported into Glade already filed out of the figure: they carry a filing date but no retainer signed in Glade, so there is no interval to measure. A firm that migrated a back catalogue of filed cases sees them in this count rather than distorting its average.
- **Cases whose filing date falls before the retainer was signed.** A negative interval is a data problem rather than a fast filing, so it is excluded.

Both counts sit next to the average, so you can see how much of the case list the figure actually covers before quoting it.

> TODO: Confirm where the retainer-to-filing average appears in the interface — the label on the "measured cases only" filter, and how the average is added to a dashboard.

### Weekly breakdown

Alongside the monthly and quarterly breakdowns, the figure can be grouped **by week**.

- **A week runs Monday to Sunday**, and a case falls into the week its filing date lands in.
- Weekly grouping is what makes a single month readable as a trend. A month viewed monthly is one bar; viewed weekly it is four or five points, so a firm can see turnaround moving within the month rather than only comparing one month against the next.
- **A week that straddles the edge of the period you are looking at is cut to the period.** Filter to a single month and the first and last weeks cover only the days inside that month, so no case outside your date range is counted.
- Everything else about the measurement is unchanged — which retainer signature is used, which cases are excluded, and the time zone the days are counted in all work exactly as they do for the monthly and quarterly views.

> TODO: Confirm where the weekly grouping is chosen on the report, and whether it is available on dashboard widgets as well as the report itself.

## Configuration

- **Retainer-to-filing breakdown**: Week, month, or quarter. Weeks run Monday to Sunday and are cut to the report's date range. Nothing else to configure. The dates are read from the retainer signatures on the case and from the case's recorded filing date; day counting follows your firm's configured time zone, falling back to UTC if none is set.

## Edge Cases & Limitations

- **Days to filing** is blank on a case that has no signed retainer, on a case with no filing date, and on a case whose filing date falls before its retainer signature. These cases are counted in their own totals rather than being averaged in, so an average never quietly includes or guesses at them.
- Cases imported into Glade already filed are not measured for time to filing, because the retainer behind them was never signed in Glade. There is no way to supply a retainer date for them after the fact.
- A case with no filing date is counted in the overall totals but falls into no month or quarter, because the breakdown is keyed to the filing date. The monthly and quarterly counts therefore add up to less than the overall count on a firm with unfiled cases in the report.
- Time to filing is a calendar-day count. There is no business-day measure, so an interval spanning a holiday weekend reads longer than the working days it took.
- Weekly retainer-to-filing figures are read from partial weeks at the edges of your date range, so the first and last points on a monthly view cover fewer days than the ones between them. Compare the middle of a month rather than its edges when reading a trend.
- The weekly breakdown covers only cases that have been filed, since it is keyed to the filing date. Cases still in progress are not in any week's figure, the same as in the monthly and quarterly views.

## Related Features

- [Custom Reports](./README.md)
- [Columns](./columns.md)
- [Dashboards](../dashboards.md)
- [Custom Terms](../../../workflows/custom-terms.md) — retainer agreements are the signatures the time-to-filing measurement starts from.
- [Settings](../../settings.md) — firm timezone
