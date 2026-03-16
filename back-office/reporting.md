# Reporting

## Overview

Reporting provides creators with operational and financial visibility into their practice. The system includes workflow-level reports (intake status, paralegal workload, documents team activity, court calendar), financial reports (sales overview, conversion metrics), and task efficiency analytics. Reports are scoped to a single creator and support date-range filtering, team member filtering, and CSV export.

## Key Behaviors

### Intake Status Report

- Lists all main user workflows for a creator within a date range, showing client info, workflow name, status, consultation date, intake lead, assigned paralegal, recommended case type, and last activity.
- Filters by workflow status, intake lead (`initiatedByPersonId`), and paralegal (via `UserWorkflowOwner` join).
- Resolves associated workflows to display the initial workflow and any recommended case types.
- Consultation dates are pulled from the `Booking` associated with the initial workflow.
- Paginated for dashboard display; supports `perPage = 0` for full CSV export.

### Paralegal Report

- Shows per-paralegal workload metrics: cases in preparation, cases filed, filing rate, dropped cases, paused cases, and archived cases.
- Breaks down active (non-paused, non-archived) cases by custom status, showing counts per status per paralegal.
- Filing rate is calculated as `casesFiled / (casesInPreparation + casesFiled) * 100`.
- Cases are classified as dropped if `canceledAt` or `endedAt` is set, filed if `filedAt` is set, or in preparation otherwise.
- CSV export includes a TOTAL row with summed columns and averaged filing rate.

### Documents Report

- Tracks documents team and paralegal activity: document checklists reviewed, new workflows assigned, clients served percentage, and key metrics (total cases assigned, incoming cases).
- Filters team members by "Paralegal" and "Documents Team" workflow roles.
- Document checklists reviewed counts completed tasks with `action = 'review-document-request'` assigned to the team member within the date range.
- Clients served is expressed as a percentage of total main workflows.

### Court Calendar

- Displays court hearing events grouped by date, populated from PACER docket data.
- Each event includes hearing type, event time, client, attorney, judge, trustee, case number, court code, courtroom location, and Zoom meeting details.
- Events are parsed from docket annotations where `all_day === false`. All-day annotations are excluded.
- Filters by hearing type, attorney, judge, trustee, client, and case number. Filter options are dynamically aggregated from existing calendar data.
- Docket data is persisted in a `Dockets` table for reference, and calendar entries are created in `CourtCalendar`.
- CSV export formats dates and times in the creator's configured timezone.

### Sales Overview

- Provides payment volume, transaction count, and average transaction amount for a configurable lookback period (default 30 days), with percentage change compared to the previous equivalent period.
- Payment volume data is grouped by day (<=30 days), week (<=90 days), month (<=3 years), or year (>3 years).
- Shows payment source breakdown: payment plans, on-behalf-of payments, client payments, and outside-of-platform payments.
- Lists top 10 clients by total payment amount and 10 most recent payments.

### Current Sales Overview

- Shows month-to-date and year-to-date summaries: payment volume, transaction count, and average transaction amount.

### Conversion Metrics (Firm Overview)

- Tracks client acquisition and retention over time with yearly and monthly granularity.
- Metrics include total new clients, total retained clients (those who agreed to terms), same-day closed count and percentage, average revenue per retained client, and total revenue collected.
- Monthly metrics include percentage change vs. last month and vs. same month last year.
- Monthly data includes a 12-month conversion waterfall showing when clients converted relative to their workflow creation month.

### Task Efficiency

- Tracks time-to-completion for tasks identified by `referenceType` and `referenceId`.
- Records task start, completion (with immutable `firstCompletedAt` and mutable `lastCompletedAt`), and reopens (incrementing `reopenCount`).
- Aggregate metrics are grouped by `(templateId, templateName, referenceType)` and include: total started, total completed, completion rate, avg/median/p90 time-to-complete, reopen rate, and avg reopen count.
- Supports AI-generated narrative reports via `TaskEfficiencyReportService`, which passes efficiency data to an AI bot and stores the generated content.

### Leaderboard

- Tracks attorney filing data from PACER, aggregated by state and district.

## Configuration

- **Date range**: All workflow reports require or accept `startDate` and `endDate` parameters.
- **Team member filter**: Documents report accepts an optional list of team member person IDs.
- **Workflow status filter**: Intake status report accepts an optional list of workflow status slugs.
- **Lookback period**: Sales overview accepts a `days` parameter (default 30).
- **Creator timezone**: Court calendar CSV export uses the creator's `timezone` setting for date/time formatting; falls back to UTC if not set or invalid.

## Edge Cases & Limitations

- The sales overview rounds monetary values to 2 decimal places. Percentage change returns 0 when the previous period had no records, rather than infinity or N/A.
- The conversion metrics firm overview aggregates across all time since creator creation. For creators with long histories, this query may be slow.
- Court calendar entries are only created from docket annotations where `all_day === false`. If all annotations on a docket entry are all-day, the entry is silently skipped.
- Task efficiency uses atomic SQL operations (COALESCE for firstCompletedAt, increment for reopenCount) to prevent race conditions on concurrent updates.
- Batch task efficiency lookups are limited to 100 items per request.

## Related Features

- [Case Management](./case-management.md) — reports operate on `UserWorkflow` data and case statuses.
- [Staff Management](./staff-management.md) — paralegal and documents reports segment by workflow role.
- [Settings](./settings.md) — custom statuses affect status-based report columns; creator timezone affects CSV formatting.
