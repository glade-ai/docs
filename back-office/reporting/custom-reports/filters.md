# Custom Report Filters

## Overview

Custom reports can be narrowed by attorney, workflow type, completion event, pending client tasks, court district, and date ranges, and then searched within. This doc covers how each filter behaves and how search and date boundaries interact with them.

## Key Behaviors

### Filtering a report

- **Attorney**: An **Unassigned** option returns only cases with no attorney assigned, so you can find cases that still need an attorney on them. It is an exclusive choice — selecting **Unassigned** returns unassigned cases only, rather than combining with specific attorneys you have also picked.
- The **Workflow type** filter lists only case types your firm can actually be working: a type appears if it has an active attorney-case template, or if at least one case has ever been opened under it.
  - This is a deliberate narrowing. The filter previously listed every workflow template that had ever existed on the firm, which included abandoned "New Workflow" drafts and per-service utility templates that were never used for client matters — one firm saw 52 options where roughly 30 were meaningful. If your list of workflow types is much shorter than it used to be, nothing has been deleted; the unusable entries are simply no longer offered.
  - **Archived case types that have real cases behind them remain selectable.** An archived "… with Filing" type that your firm filed cases under still appears, so historical reporting on it is unaffected.
  - Selecting a workflow type returns cases built on *every* version of that template, not just the version your firm is using today. Firms that edit a template regularly accumulate many versions, and cases started on an earlier version used to be left out — so a count of filed cases could come back far lower than the true figure.
- **Completion event**: A **Retainer not signed** option returns cases that have an active retainer still awaiting signature. It is the mirror of **Retainer signed** — a case with no retainer at all matches neither option.
- **Pending client tasks**: Segments cases by whether the client still has an incomplete task assigned to them. Both the "has pending" and "no pending" selections now return accurate results; previously selecting either could produce results that did not match the filter.
- **Court district**: The report can be narrowed to one or more court districts, so you can answer "which cases are filed in these districts?" rather than only seeing the district on each row. The filter applies to the report on screen and to its CSV export.
  - It matches on the district assigned to the case, not on district text typed into case data. The same court is often written several different ways by hand, which cannot be filtered on reliably.
  - A case with no assigned district is not returned by a district filter, even if a district name appears elsewhere on it.

Some filters also change what a column shows — see [Columns](./columns.md) for the Court notice type and Case number columns.

### Date filters

When you filter a report by a date — cases filed in a range, court notices received in a range — the days you pick are treated as whole calendar days in your firm's time zone.

- Picking a single day returns everything that happened on that day, from midnight to midnight in your firm's time zone. An end date includes the whole of that day rather than stopping at the start of it.
- Because the boundaries follow your firm's time zone, a report run in the afternoon returns the same rows as the same report run that evening. Previously the day boundaries were fixed to UTC, so firms outside UTC could see records from the edge of a neighboring day included or dropped.
- If your firm has no time zone configured in settings, day boundaries fall back to UTC. Set your firm's time zone if your date-filtered reports look shifted by a few hours. See [Settings](../../settings.md).
- A date that is not a real calendar date (for example, February 31) is rejected with an error rather than being silently rolled forward to the next valid day.

### Searching within a filtered report

The search box narrows whatever the filters have already returned — it never widens it.

- A search term can only reduce the rows a filter returned. It cannot surface a case the filters exclude, and it cannot hide a case the filters include.
- Previously a search term could silently cancel out some filters, so the same report with and without a search term disagreed about which cases belonged in it. A report filtered to cases filed this month, for example, could return unrelated cases from other months as soon as anyone typed in the search box. If your team stopped trusting search on a filtered report, try it again.

## Configuration

- **Custom report filters**: Custom reports filter by workflow type (matching all versions of the selected template), completion event (including "retainer signed" and "retainer not signed"), pending client tasks, and court district. Workflow type selections are not subject to the 500-entry cap that applies to the intake status report's filters, so a firm with a large number of template versions can still select every type it needs.
- **Custom report workflow type filter**: Options are derived automatically from your firm's active case types and the case types you have cases under. There is no setting that controls which types are listed.
- **Custom report date filters**: Day boundaries follow your firm's configured time zone. There is no per-report time zone setting. A firm with no time zone configured falls back to UTC.

## Edge Cases & Limitations

- A custom report's **Workflow type** filter does not list case types that have neither an active template nor any cases. A brand-new case type is not selectable until it is enabled or has its first case.
- The **Court district** filter only returns cases with a district assigned to them. Cases that record a district as free text but have none assigned are excluded from a filtered report.
- Custom report date filters interpret the days you pick in your firm's time zone. Reports run before this was corrected may have included or omitted records at the edges of the range — re-run any date-filtered report whose totals looked slightly off.

## Related Features

- [Custom Reports](./README.md)
- [Columns](./columns.md)
- [Exporting](./exports.md)
- [Intake Status Report](../intake-status-report.md) — its own workflow/service/retainer type filters
- [Settings](../../settings.md) — firm timezone
