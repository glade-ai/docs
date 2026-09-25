# Court Calendar

## Overview

The Court Calendar displays court hearing events populated from PACER docket data, grouped by date, so a firm can see upcoming hearings across its cases in one place and export them.

## Key Behaviors

- Displays court hearing events grouped by date, populated from PACER docket data.
- Each event includes hearing type, event time, client, attorney, judge, trustee, case number, court code, courtroom location, and Zoom meeting details.
- Only timed hearings appear on the calendar. All-day events are excluded.
- You can filter by hearing type, attorney, judge, trustee, client, and case number. Filter options are dynamically populated from existing calendar data.
- CSV export formats dates and times in your firm's configured timezone.

## Configuration

- **Date range**: The report requires or accepts a start date and end date.
- **Firm timezone**: The court calendar CSV export uses your firm's timezone setting for date/time formatting. If no timezone is configured, it defaults to UTC.

## Edge Cases & Limitations

- Court calendar entries only appear for timed hearings. If all hearings on a docket entry are all-day events, nothing appears on the calendar.

## Related Features

- [Reporting](./README.md)
- [Court Notices Report](./court-notices-report.md)
- [Settings](../settings.md) — firm timezone affects CSV formatting.
