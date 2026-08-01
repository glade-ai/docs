# Reporting

## Overview

Reporting provides your firm with operational and financial visibility into your practice. The system includes workflow-level reports (intake status, paralegal workload, documents team activity, court calendar), financial reports (sales overview, conversion metrics), and task efficiency analytics. Reports support date-range filtering, team member filtering, and CSV export.

## Key Behaviors

### Intake Status Report

- Lists all primary cases for your firm within a date range, showing client info, workflow name, status, consultation date, intake lead, assigned paralegal, recommended case type, and last activity.
- You can filter by workflow status, intake lead, and paralegal. You can also narrow the report by **workflow type**, **service type**, and **retainer type** to focus on a specific kind of case, the service the client signed up for, or the type of retainer agreement in place. These selectors can be combined with each other and with the existing filters, and each accepts up to 500 selections at a time.
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

### Case Data custom reports

Custom reports let your firm build its own view over case data, choosing the columns and filters it needs rather than working from a fixed report layout.

> TODO: This section documents only the filter and column behavior confirmed by recent changes. Building, saving, and sharing a custom report is not yet described — fill in from the custom report builder.

#### Who created a report

Every saved report shows the team member who created it, with their name and profile photo on the report card, so a firm with dozens of saved reports can tell at a glance whose view each one is.

- The person shown is the report's original creator. It does not change when someone else edits the report.
- A **Created by me** filter narrows the report list to the reports you created. Combine it with the search box to find your own saved view quickly.
- If the person who created a report has since been removed from the firm, the report still lists and remains usable — it simply shows no creator.

#### Filtering a report

- **Attorney**: An **Unassigned** option returns only cases with no attorney assigned, so you can find cases that still need an attorney on them. It is an exclusive choice — selecting **Unassigned** returns unassigned cases only, rather than combining with specific attorneys you have also picked.
- The **Workflow type** filter lists only case types your firm can actually be working: a type appears if it has an active attorney-case template, or if at least one case has ever been opened under it.
  - This is a deliberate narrowing. The filter previously listed every workflow template that had ever existed on the firm, which included abandoned "New Workflow" drafts and per-service utility templates that were never used for client matters — one firm saw 52 options where roughly 30 were meaningful. If your list of workflow types is much shorter than it used to be, nothing has been deleted; the unusable entries are simply no longer offered.
  - **Archived case types that have real cases behind them remain selectable.** An archived "… with Filing" type that your firm filed cases under still appears, so historical reporting on it is unaffected.
  - Selecting a workflow type returns cases built on *every* version of that template, not just the version your firm is using today. Firms that edit a template regularly accumulate many versions, and cases started on an earlier version used to be left out — so a count of filed cases could come back far lower than the true figure.
- **Completion event**: A **Retainer not signed** option returns cases that have an active retainer still awaiting signature. It is the mirror of **Retainer signed** — a case with no retainer at all matches neither option.
- **Pending client tasks**: Segments cases by whether the client still has an incomplete task assigned to them. Both the "has pending" and "no pending" selections now return accurate results; previously selecting either could produce results that did not match the filter.
- The **Court notice type** column reflects the filter you have applied. When you filter the report to specific court notice types, the column shows only those types for each case — previously it listed every notice type on the case regardless of the filter, so a filtered report showed rows whose column contradicted the filter above it.
- Each type in the **Court notice type** column is clickable and opens the matching notice in a panel. Where a case has more than one notice of the same type, the link opens the most recent one.
- **Court district**: The report can be narrowed to one or more court districts, so you can answer "which cases are filed in these districts?" rather than only seeing the district on each row. The filter applies to the report on screen and to its CSV export.
  - It matches on the district assigned to the case, not on district text typed into case data. The same court is often written several different ways by hand, which cannot be filtered on reliably.
  - A case with no assigned district is not returned by a district filter, even if a district name appears elsewhere on it.
- The **Client address** column reads the client's address from case data — the same address shown on the case's own case-data panel, written there by questionnaire sync, credit report pulls, and document extraction. The column was previously blank for most cases because it read an older location that almost nothing writes to any more; more than 10,000 cases across 51 firms had an address on file and an empty cell.
  - Each part of the address resolves on its own, so a case with a street but no ZIP still shows the street.
  - An address that exists only on the client record in the Clients panel, and was never written to case data, shows as blank. If a case shows an address on screen but not in the report, that is the reason — contact Glade support if you need those addresses brought across.
  - The column is for display. Sorting or filtering the report by client address is not available.
- **CSV export** of a custom report was failing to complete and now exports normally. If your team gave up on exporting a custom report, try it again.
- **An export now matches the report it came from.** The file is built from the report itself rather than assembled out of the pages on screen, so every column you selected is in it — including columns your firm defined for its own workflow roles, which used to be dropped from the file without warning — and the report's filters and sort order are carried through. Rows beyond the page you are looking at are included. Exports work the same way on case, court notice, and payments reports. If your firm compared an export against the report on screen and found columns or rows missing, re-run it.
- **Duplicating a report.** A **Duplicate** action on a saved report creates a copy carrying the same description, filters, sorting, and columns, so building a near-identical variant is a copy plus one edit rather than a rebuild from a blank report.
  - The copy is named after the original with a copy number — `Weekly filings Copy 1`, then `Copy 2`, and so on. Duplicating a copy continues that sequence instead of stacking markers, so duplicating `Weekly filings Copy 1` gives you `Weekly filings Copy 2`.
  - Numbering carries on past the highest number already in use rather than filling gaps, so renaming or deleting a copy in the middle of the sequence does not cause the next duplicate to reuse its number. Once every copy is gone, numbering restarts at 1.
  - The copy is recorded as authored by whoever duplicated it, not by whoever created the original.
  - A very long report name is shortened to make room for the copy number.
- **Reaffirmation agreement**: A column and a matching filter report whether a case intends to reaffirm any debt. A case counts as reaffirming when at least one creditor on the bankruptcy schedules questionnaire's creditor list answers the statement-of-intention question — "What do you intend to do with the property that secures the debt?" — with **Retain the property and enter into a Reaffirmation Agreement**. One qualifying creditor is enough for the whole case.
  - Only creditors listed on **Schedule D** are considered. The same intention question is asked on every creditor row, and rows on Schedules E/F/G carry a default answer that does not indicate an intention about secured property, so counting them would report cases as answered when nothing was decided.
  - Creditor rows excluded from the petition are ignored.
  - The filter offers reaffirming and non-reaffirming selections plus a **not answered** selection. A case whose bankruptcy schedules questionnaire has not been filled in — a consultation or a turned-down matter, for example — has no answer to give and falls under **not answered** rather than under "no".
  - The lease-assumption question on the same form ("Will the lease be assumed?") is **not** available as a column or filter.

### Dashboards

Alongside the personal dashboard each person sees on their own homepage, a firm can build **named dashboards** that everyone at the firm shares.

- A named dashboard belongs to the firm, not to the person who created it. Every member sees the same dashboard and the same widgets on it.
- Dashboard names are unique within the firm, and matching ignores capitalization — "Intake" and "intake" are treated as the same name.
- Widgets are added to a named dashboard, reordered, and removed the same way they are on the personal homepage dashboard. Each widget keeps its own filters, sorting, and choice of columns.
- Personal homepage dashboards are unaffected. Each person still has exactly one, and it stays private to them.

> TODO: Confirm where named dashboards are created and managed in the interface, and whether any firm-level permission controls who can create or edit them.

#### Date filters

When you filter a report by a date — cases filed in a range, court notices received in a range — the days you pick are treated as whole calendar days in your firm's time zone.

- Picking a single day returns everything that happened on that day, from midnight to midnight in your firm's time zone. An end date includes the whole of that day rather than stopping at the start of it.
- Because the boundaries follow your firm's time zone, a report run in the afternoon returns the same rows as the same report run that evening. Previously the day boundaries were fixed to UTC, so firms outside UTC could see records from the edge of a neighboring day included or dropped.
- If your firm has no time zone configured in settings, day boundaries fall back to UTC. Set your firm's time zone if your date-filtered reports look shifted by a few hours. See [Settings](./settings.md).
- A date that is not a real calendar date (for example, February 31) is rejected with an error rather than being silently rolled forward to the next valid day.

#### Searching within a filtered report

The search box narrows whatever the filters have already returned — it never widens it.

- A search term can only reduce the rows a filter returned. It cannot surface a case the filters exclude, and it cannot hide a case the filters include.
- Previously a search term could silently cancel out some filters, so the same report with and without a search term disagreed about which cases belonged in it. A report filtered to cases filed this month, for example, could return unrelated cases from other months as soon as anyone typed in the search box. If your team stopped trusting search on a filtered report, try it again.

#### Payments reports

Payments are available as a custom report subject, so your firm can build a saved view over its payment records the same way it does over cases — for example, *payments that failed in the last 7 days on a case with a payment plan*.

Payment reports can be filtered and sorted by:

- **Payment status** — one or several statuses at a time (for example, failed and pending together). This replaces having to pick a single status.
- **On a payment plan** — restrict to payments that are part of a payment plan, or to payments that are not.
- **Invoice** — restrict to the payments made against one invoice.
- **Payment method** — search by payment method to narrow to a particular card or bank account.
- **Date order** — sort oldest-first or newest-first. Paging through a large payment report is stable: payments that share the same timestamp (every charge in one payment-plan run, for example) keep a consistent order instead of some rows repeating on one page and going missing from another.

Choosing several statuses and the older single-status filter at the same time is not allowed — the report asks you to use one or the other. **Refunded** is not a payment status; a refund is recorded as an amount returned on a payment, so it is only available through the single-status filter.
### Court Notices

The Court Notices report lists the court notices Glade has received from PACER for your firm, and can be filtered by notice type.

- **Unassigned** is available as a notice-type option alongside the named types. Selecting it returns the notices Glade could not classify — precisely the ones that need someone to look at them. Previously an unclassified notice could only be reached by scrolling past everything that had been classified.
- **Unassigned** combines with the named types rather than replacing them, so you can review every Notice of Hearing together with everything unclassified in a single list. Selecting it on its own narrows the report to the unclassified notices; selecting nothing at all still returns everything.
- The CSV export applies the same selection, so an export filtered to **Unassigned** contains the same notices as the report on screen.

## Configuration

- **Date range**: All workflow reports require or accept a start date and end date.
- **Team member filter**: The documents report accepts an optional list of team members to include.
- **Workflow status filter**: The intake status report accepts an optional list of statuses to filter by.
- **Workflow / service / retainer type filters**: The intake status report also accepts optional lists of workflow types, service types, and retainer types. Each list is capped at 500 entries.
- **Custom report filters**: Custom reports filter by workflow type (matching all versions of the selected template), completion event (including "retainer signed" and "retainer not signed"), pending client tasks, and court district. Workflow type selections are not subject to the 500-entry cap that applies to the intake status report's filters, so a firm with a large number of template versions can still select every type it needs.
- **Court notice type filter**: The Court Notices report filters by any combination of named notice types plus **Unassigned**. Options are derived from the notice types Glade has classified for your firm; there is no setting that controls the list.
- **Lookback period**: The sales overview accepts a number of days to look back (default 30).
- **Firm timezone**: The court calendar CSV export uses your firm's timezone setting for date/time formatting. If no timezone is configured, it defaults to UTC.
- **Custom report workflow type filter**: Options are derived automatically from your firm's active case types and the case types you have cases under. There is no setting that controls which types are listed.
- **Reaffirmation agreement**: Nothing to configure. The answer is read from the bankruptcy schedules questionnaire and updates as the questionnaire is filled in.
- **Named dashboards**: Created per firm and shared by everyone in it. Names must be unique within the firm.
- **Custom report date filters**: Day boundaries follow your firm's configured time zone. There is no per-report time zone setting. A firm with no time zone configured falls back to UTC.
- **Payments report filters**: Payment status (one or more), payment-plan membership, a specific invoice, payment method search, and date sort order. There is no setting that enables these — they are available on any payments report.

## Edge Cases & Limitations

- The sales overview rounds monetary values to 2 decimal places. Percentage change shows 0% when the previous period had no records, rather than showing "N/A".
- The conversion metrics report aggregates across all time since your firm was created. For firms with long histories, this report may be slow to load.
- Court calendar entries only appear for timed hearings. If all hearings on a docket entry are all-day events, nothing appears on the calendar.
- Task efficiency lookups are limited to 100 items per request.
- A custom report's **Workflow type** filter does not list case types that have neither an active template nor any cases. A brand-new case type is not selectable until it is enabled or has its first case.
- The **Reaffirmation agreement** column reports what the schedules questionnaire says, not what was ultimately filed. A reaffirmation agreement decided outside the questionnaire, or changed after the petition went out, is not reflected until the questionnaire is updated.
- Cases with no bankruptcy schedules questionnaire are reported as **not answered** on the reaffirmation column. This is the expected result for consultations and non-bankruptcy matters, and it is distinct from a case that answered "no".
- A named dashboard cannot reuse the name of another named dashboard at the same firm, regardless of capitalization.
- The **Court district** filter only returns cases with a district assigned to them. Cases that record a district as free text but have none assigned are excluded from a filtered report.
- The **Client address** column is blank for a case whose address was never written to case data, including cases whose address is held only on the client record. It cannot be sorted or filtered on.
- A custom report export covers up to **50,000 rows**. A report with more rows than that exports the first 50,000 — narrow the filters and export in batches if your firm needs the rest.
- A very large export can run out of time before the file is produced, in which case the export fails rather than returning a partial file. Filter the report down and run it again.
- The **Created by me** filter on the report list matches the report's original creator only. There is no filter for "reports I have edited".
- A payments report cannot combine the multi-select **Payment status** filter with the older single-status filter. Use one or the other.
- **Refunded** is not selectable in the multi-select payment status filter, because a refund is an amount returned on a payment rather than a status the payment sits in.
- Custom report date filters interpret the days you pick in your firm's time zone. Reports run before this was corrected may have included or omitted records at the edges of the range — re-run any date-filtered report whose totals looked slightly off.

## Related Features

- [Case Management](./case-management.md) — reports operate on case data and case statuses.
- [Staff Management](./staff-management.md) — paralegal and documents reports segment by workflow role.
- [Settings](./settings.md) — custom statuses affect status-based report columns; firm timezone affects CSV formatting.
