# Court Notices Report

## Overview

Court notices are reportable in their own right, with **one row per notice received from PACER** rather than one row per case. This matters because most of the court notices a firm receives are never matched to a workflow in Glade, so they cannot be reached through any case-based report.

## Key Behaviors

- Each row carries the detail printed on the notice: the case name and case number, the notice type, the document number, the judge's initials, the trustee's name, the courtroom and its location, the video hearing (Zoom) details, and the date Glade received the notice.
- **Client column**: for a notice linked to a workflow, this is the client on that case. For an unlinked notice, it falls back to the case name written on the notice itself — which is the only client identifier an unlinked notice carries.
- **Linked / unlinked filter**: narrow the report to notices that are linked to a workflow, or to those that are not. For many firms the large majority of notices are unlinked, so this filter is usually the first thing to set — reviewing unlinked notices is how you find court activity that never reached a case.
- **Notice-type filter**: filter by any combination of named notice types, and by **Unassigned** — the notices Glade could not classify, precisely the ones that need someone to look at them (previously reachable only by scrolling past everything already classified). Unassigned combines with the named types rather than replacing them, so a named type and the unclassified bucket can be reviewed in one list; selecting it alone narrows to the unclassified notices, and selecting nothing still returns everything.
- **Search** matches the case name as well as the client's name, so a notice can be found by the name shown in its Client column. Previously the search only looked at client records, which meant the name displayed on an unlinked row could not be searched for.
- **Assignee and Attorney columns**: a notice shows who owns the case it landed on and which attorney is on that case, so a firm triaging the day's notices can see whose work each one is without cross-referencing the case list by hand. Both are read from the case the notice matched — a court notice carries no assignment of its own — so they are empty on a notice that never matched a case.
- **Assignee and Attorney filters**: narrow the report to your own cases, or to one attorney's. Each filter also offers an **Unassigned** option that returns the notices whose column is empty, for any reason — the notice never matched a case, or it matched one with nobody on it. Between them, the two selections cover every notice, so nothing falls between the filter and the blank column.
- **CSV export** returns the same columns as the on-screen report and respects the filters you have applied, so a filtered export and the report you are looking at agree. See also [Exporting Custom Reports](./custom-reports/exports.md).

## Configuration

- **Court notice type filter**: The Court Notices report filters by any combination of named notice types plus **Unassigned**. Options are derived from the notice types Glade has classified for your firm; there is no setting that controls the list.
- **Linked filter**: The court notices report accepts a linked/unlinked selection to include only notices attached to a workflow, or only those not attached to one. Leaving it unset includes both.
- **Assignee and attorney filters**: The court notices report accepts a list of assignees and a list of attorneys, each with an optional **Unassigned** selection. They can be combined with each other and with the other court notice filters, and both apply to the CSV export as well as the report on screen. Options come from your firm's team roster and attorney list; there is no setting that controls them.

## Edge Cases & Limitations

- An unlinked court notice has no client record behind it, so columns that come from the case — rather than from the notice itself — are empty on those rows. The case name on the notice is what identifies the client. This includes the Assignee and Attorney columns, which are read from the matched case.
- A court notice has no assignee or attorney of its own. Reassigning a case changes what its notices report; there is no way to assign a notice to someone independently of the case it landed on.
- Text taken from a court notice is exported to CSV as plain text even when it begins with a character a spreadsheet would otherwise read as a formula, so party and trustee names open as written.

## Related Features

- [Reporting](./README.md)
- [Court Calendar](./court-calendar.md)
- [Custom Report Columns](./custom-reports/columns.md) — the Court notice type column on case reports
- [Case Management](../case-management.md)
