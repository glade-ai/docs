# Reporting

## Overview

Reporting provides your firm with operational and financial visibility into your practice. The system includes workflow-level reports (intake status, paralegal workload, documents team activity, court calendar), financial reports (sales overview, conversion metrics), and task efficiency analytics. Reports support date-range filtering, team member filtering, and CSV export.

## Key Behaviors

### Intake Status Report

- Lists all primary cases for your firm within a date range, showing client info, workflow name, status, consultation date, intake lead, assigned paralegal, recommended case type, and last activity.
- You can filter by workflow status, intake lead, and paralegal.
- Shows associated workflows alongside the initial workflow, including any recommended case types.
- Consultation dates come from the booking associated with the initial workflow.
- Paginated for dashboard display; supports full CSV export.

### Paralegal Report

- Shows per-paralegal workload metrics: cases in preparation, cases filed, filing rate, dropped cases, paused cases, and archived cases.
- Breaks down active (non-paused, non-archived) cases by custom status, showing counts per status per paralegal.
- Filing rate is the percentage of cases filed out of the total cases in preparation plus cases filed.
- Cases are classified as dropped if they were canceled or ended, filed if a filing date is recorded, or in preparation otherwise.
- CSV export includes a total row with summed columns and averaged filing rate.

### Documents Report

- Tracks documents team and paralegal activity: document checklists reviewed, new workflows assigned, percentage of clients served, and key metrics (total cases assigned, incoming cases).
- Only shows team members with a "Paralegal" or "Documents Team" role.
- Document checklists reviewed counts completed document review tasks assigned to the team member within the date range.
- Clients served is expressed as a percentage of total primary cases.

### Court Calendar

- Displays court hearing events grouped by date, populated from PACER docket data.
- Each event includes hearing type, event time, client, attorney, judge, trustee, case number, court code, courtroom location, and Zoom meeting details.
- Only timed hearings appear on the calendar. All-day events are excluded.
- You can filter by hearing type, attorney, judge, trustee, client, and case number. Filter options are dynamically populated from existing calendar data.
- CSV export formats dates and times in your firm's configured timezone.

### Sales Overview

- Shows payment volume, transaction count, and average transaction amount for a configurable lookback period (default 30 days), with percentage change compared to the previous equivalent period.
- Payment data is grouped by day (up to 30 days), week (up to 90 days), month (up to 3 years), or year (over 3 years).
- Shows payment source breakdown: payment plans, on-behalf-of payments, client payments, and outside-of-platform payments.
- Lists the top 10 clients by total payment amount and the 10 most recent payments.

### Current Sales Overview

- Shows month-to-date and year-to-date summaries: payment volume, transaction count, and average transaction amount.

### Conversion Metrics (Firm Overview)

- Tracks client acquisition and retention over time with yearly and monthly granularity.
- Metrics include total new clients, total retained clients (those who agreed to terms), same-day closed count and percentage, average revenue per retained client, and total revenue collected.
- Monthly metrics include percentage change vs. last month and vs. the same month last year.
- Monthly data includes a 12-month conversion waterfall showing when clients converted relative to the month their case was created.

### Task Efficiency

- Tracks time-to-completion for tasks across your firm.
- Records when tasks are started, completed, and reopened.
- Aggregate metrics include: total started, total completed, completion rate, average/median/90th-percentile time-to-complete, reopen rate, and average reopen count.
- Supports AI-generated narrative summaries that interpret the efficiency data.

### Leaderboard

- Tracks attorney filing data from PACER, aggregated by state and district.

## Configuration

- **Date range**: All workflow reports require or accept a start date and end date.
- **Team member filter**: The documents report accepts an optional list of team members to include.
- **Workflow status filter**: The intake status report accepts an optional list of statuses to filter by.
- **Lookback period**: The sales overview accepts a number of days to look back (default 30).
- **Firm timezone**: The court calendar CSV export uses your firm's timezone setting for date/time formatting. If no timezone is configured, it defaults to UTC.

## Edge Cases & Limitations

- The sales overview rounds monetary values to 2 decimal places. Percentage change shows 0% when the previous period had no records, rather than showing "N/A".
- The conversion metrics report aggregates across all time since your firm was created. For firms with long histories, this report may be slow to load.
- Court calendar entries only appear for timed hearings. If all hearings on a docket entry are all-day events, nothing appears on the calendar.
- Task efficiency lookups are limited to 100 items per request.

## Related Features

- [Case Management](./case-management.md) — reports operate on case data and case statuses.
- [Staff Management](./staff-management.md) — paralegal and documents reports segment by workflow role.
- [Settings](./settings.md) — custom statuses affect status-based report columns; firm timezone affects CSV formatting.
