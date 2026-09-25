# Financial Reports

## Overview

Financial reports summarize your firm's payment volume and client conversion over time: the Sales Overview for a lookback period, the Current Sales Overview for month-to-date and year-to-date totals, and Conversion Metrics (Firm Overview) for client acquisition and retention.

## Key Behaviors

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

## Configuration

- **Lookback period**: The sales overview accepts a number of days to look back (default 30).

## Edge Cases & Limitations

- The sales overview rounds monetary values to 2 decimal places. Percentage change shows 0% when the previous period had no records, rather than showing "N/A".
- The conversion metrics report aggregates across all time since your firm was created. For firms with long histories, this report may be slow to load.

## Related Features

- [Reporting](./README.md)
- [Payments Reports](./custom-reports/payments-reports.md)
