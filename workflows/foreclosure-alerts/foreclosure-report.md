# The Foreclosure Report

## Overview

The foreclosure report is the case list view your team works through after each monthly report is activated: one row per case, with the foreclosure columns showing the match score, where the flag came from, the address and names on the report, and the review. This page covers filtering cases by designation, sorting by any foreclosure column, the report's filters, and exports and saved reports.

## Key Behaviors

### Finding flagged cases

On the workflows list and on custom reports, filter with **Foreclosure**: **All**, **Designated**, or **Not designated**. The filter carries through to the cases CSV export.

### Sorting

Every foreclosure column can be sorted, so a long monthly report can be worked in whatever order suits the reviewer instead of paged through by hand.

- **Match score** ranks a case by its highest current match — the first number shown in its Match score cell. Matches that were removed by your team, never applied, or deleted are not counted.
- **Foreclosure source** sorts **Glade match** first, then cases flagged both ways, then **Manually tagged**.
- **Review status** sorts by its label (**Affirmed**, **Dismissed**, **Unreviewed**).
- **Foreclosure address**, **Foreclosure client**, **Review note**, **Foreclosure attorney**, and **Foreclosure attorney email** sort alphabetically, ignoring capitalization. Where a cell holds more than one value, the case sorts by the first one shown in the cell.
- A blank cell, or a case with no current match, sits at the bottom whichever direction you sort.
- Paging through the report and the CSV export both keep the sorted order.

### Filters

Alongside the existing tag and label filters, the report can be narrowed by:

| Filter | What it keeps |
|--------|---------------|
| **Match score** | Matches within a score range. Either end can be left open, and both ends are inclusive. |
| **Review status** | **Affirmed**, **Dismissed**, or **Unreviewed** — see [Flags and Review](./flags-and-review.md#review-status). |
| **Foreclosure source** | **Glade match**, **Manually tagged**, or both. |
| **Report month** | Matches from the chosen month's report. The choices are every month your firm has a successfully imported report for, newest first. |

- **Filters combine, and they all apply to the same match.** "Unreviewed and above 80%" keeps a case only when one of its matches is both unreviewed and above 80% — not a case with one unreviewed match and a different high-scoring one.
- The filters combine with each other and with the tag and label filters.
- A hand-applied flag has no report month, so it never matches a report-month filter.
- The filters and the sort carry through to the CSV export and to saved reports, including saved reports run through the Glade MCP assistant.

The foreclosure columns on the workflows list and on custom reports are **Foreclosure address**, **Foreclosure client**, **Match score**, **Review status**, **Review note**, **Foreclosure attorney**, **Foreclosure attorney email**, and **Foreclosure source**.

The uploaded file is a different screen. Open **Foreclosure detection**, then **View data**. The **Foreclosure data** table shows **Source row**, **Property address**, **Owner**, **Mortgagor**, **City**, **County**, **ZIP code**, **Foreclosure reference**, **Parcel**, and **Data quality**.

## Edge Cases & Limitations

- A filter value that is not valid is refused with an error, rather than being ignored and returning — or exporting — the firm's whole caseload.
- Sorting puts blank cells last but does not hide them. Use the filters to leave cases out.
- A report whose import failed, or whose report date could not be read, does not appear as a report-month choice.

## Related Features

- [Foreclosure Alerts](./README.md)
- [Reports and Matching](./reports-and-matching.md)
- [Flags and Review](./flags-and-review.md)
- [Workflow List](../status-tracking/workflow-list.md)
