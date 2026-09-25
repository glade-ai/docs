# Bookings Report

## Overview

The bookings list answers *"what is on the calendar"*. The bookings report answers a different question — *"which of our cases have appointments, and whose cases are they?"* — with **one row per booking** rather than one row per case.

## Key Behaviors

- Each row carries the client, the service booked, the appointment time, and the **assignees on the case the booking belongs to**. A firm can therefore see a paralegal's appointments without cross-referencing the case list by hand.
- **Filter by case assignee**, including an option for bookings whose case has nobody assigned. This is separate from the existing filter on whose calendar a booking sits, and the two combine. Firms that book everything onto one shared calendar could not narrow to a person's own cases before — every booking carried the same calendar, so the calendar filter returned either nothing or everyone.
- **The date range is optional.** Leaving it off returns every booking rather than none. It also brings in bookings that have no time on them at all — a service bought but never scheduled — which no date range can match. For firms that sell sessions ahead of scheduling them, these can be a large share of the total and were previously unreachable.
- Paging through a long report is stable: bookings that share a time, and bookings with no time at all, keep a consistent order instead of some rows repeating on one page and going missing from another. Never-scheduled bookings sort to the end in both directions.
- **CSV export reads the same data as the report on screen**, so a filtered export and the report it came from always agree about which bookings match.

### Lead source, case labels, and when the booking was taken

Three more pieces of information are available on each row, so the report can answer where an appointment came from and what kind of case it belongs to without cross-referencing the case list:

- **Lead source** — the lead source recorded on the client when they were captured. It can also be filtered on. The filter matches the lead source's name as it was recorded at the time, so renaming a lead source in your settings does not drop the clients captured under the old name out of the report.
- **The case's labels and tag** — a booking carries none of its own, so these are read from the case the booking is linked to. They are ordered and filtered exactly as they are on the cases list, including the rule that keeps an archived label visible on a case that already carries it.
- **Booked on** — when the booking was taken, which is a separate axis from when the appointment is scheduled. Filtering on a booked-on range alongside the existing appointment-date range answers questions like "booked in March, scheduled any time." A date-only end of the range includes the whole of the day it names.

### Filters that match the columns

**Status**, **Custom status**, and **Linked** were columns with no filter, so narrowing a long report meant reading down it. All three can now be filtered, and the filter narrows the whole report rather than the page you are looking at — so the count at the top always describes the same set of bookings as the rows beneath it.

- **Filtering on a case label only returns bookings that are attached to a case**, because a booking with no case has no case to carry a label. This is what the filter means rather than an oversight — but it makes an empty label column ambiguous on its own. Read it alongside the **Linked** column: a booking linked to a case with an empty label column is a case with no labels, and an unlinked booking has no case at all. Reporting both as "untagged" would misstate a large share of some firms' bookings.
- **A status you did not pick from the list is rejected rather than returning nothing.** A typo would otherwise match no rows and read as "this firm has no completed appointments," which is indistinguishable from a real answer.

### Address and county on the appointments report

> TODO: Confirm that the "appointments report" referred to here is the same report as the bookings report.

The appointments report can include the booking client's **address** and **county** as columns, and both are carried into its CSV export.

- **Address is one column**, written as a single line — street, city, state, and ZIP. A client with no address on file exports an empty cell rather than stray punctuation.
- **County is its own column** rather than being folded into the address, because the county is what a firm routes and reports on. A client whose county has not been recorded shows an empty cell.
- Both read the client's current details, so a client who moves shows their new address against appointments booked before the move.
- Select the columns on the report and they appear in the export. An export that includes them matches what the report shows on screen.

> TODO: Confirm where the bookings report is opened from in the dashboard and which columns can be added or removed.

## Configuration

- **Bookings report filters**: A date range (optional — leaving it off returns every booking), the calendar the booking sits on, and the assignees on the booking's case, with an option for cases that have nobody assigned. The calendar and case-assignee filters combine rather than replacing each other. There is no setting that enables these.
- **Appointments report address and county columns**: Selected on the report like any other column. There is no setting that enables them.

## Edge Cases & Limitations

- **Canceled bookings are left out of the bookings report entirely**, and there is no filter that brings them back. A report of canceled appointments is not currently possible.
- A booking that is not attached to a case has no assignees, so it is returned only by the unassigned selection on the case-assignee filter.
- The appointments report's address and county columns read the client's current record, not what was true when the appointment was booked. An old appointment is not a record of where the client lived at the time.
- A client's county has to have been recorded before it can appear in the report. An address on file does not by itself produce a county.

## Related Features

- [Reporting](./README.md)
- [Intake Status Report](./intake-status-report.md)
- [Scheduling](../../appointments/scheduling/README.md) — bookings, appointment outcomes, and client address/county collection
- [Case Management](../case-management.md)
