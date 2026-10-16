# Paralegal Report

## Overview

The Paralegal Report shows per-paralegal workload metrics so a firm can see how many cases each paralegal has written, and how many of those were filed, dropped, or are still in preparation. It also shows how in-preparation cases break down by custom status.

## Key Behaviors

- Shows per-paralegal workload metrics: cases written, cases in preparation, cases filed, filing rate, dropped cases, paused cases, and archived cases.
- **A case counts as written when its schedule builder was started in the date range.** The report covers cases where the bankruptcy schedules questionnaire was first started in the selected period, not cases created in that period. Imported cases and cases where no one has started the schedules are left out. Previously the report counted every case created in the period, so a firm that imported a large number of cases saw them all as "in preparation" and a very low filing rate.
- Each written case falls into exactly one group, so cases written = cases filed + dropped cases + cases in preparation:
  - **Filed** if a filing date is recorded, even when the case was ended or canceled afterwards. Previously a filed case that was later ended counted as dropped.
  - **Dropped** if it was canceled or ended without being filed.
  - **In preparation** otherwise.
- **Filing rate** is cases filed divided by cases written.
- Paused cases, archived cases, and the per-status counts describe in-preparation cases only, so they add up with the other columns instead of mixing in filed and dropped cases.
- Shows how many written cases are Chapter 7 and how many are Chapter 13.
- Only main workflows are counted.
- CSV export includes a total row with summed columns and averaged filing rate.

> TODO: The report's download in the newer Glade dashboard adds a Total row that recalculates the filing rate from the column totals, and shows each chapter's share of written cases. Confirm which report view firms use, and whether the older dashboard's export still averages the filing rate.

## Configuration

- **Date range**: The report requires or accepts a start date and end date. An end date covers the whole of that calendar day in your firm's time zone. Previously cases from the last day of the range could be left out.

## Edge Cases & Limitations

- The new counting applies to every firm. Filing rate, cases in preparation, paused, archived, and the status columns keep their names, so figures from before this change are not directly comparable.
- A case whose schedules questionnaire has never been started does not appear in the report, however long ago the case was created.

## Related Features

- [Reporting](./README.md)
- [Documents Report](./documents-report.md)
- [Intake Status Report](./intake-status-report.md)
- [Staff Management](../staff-management.md) — the report segments by workflow role.
- [Settings](../settings.md) — custom statuses affect the status breakdown columns.
