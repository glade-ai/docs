# Workflow List

## Overview

The workflow list shows your firm's cases in a table that can be sorted, filtered, tagged, and exported. This page covers the list's columns, sorting, filters and their persistence, workflow tags, and exporting unassigned workflows.

## Key Behaviors

- **Sortable workflow list**: In the workflow list view, cases can be sorted by status change date, last assignment date, or by the **Assignees** column (alphabetically by the primary owner's name). Sorting by Assignees lets you group cases by responsible team member for review or handoff.
- **Last Payment Made column**: The workflow list table includes a **Last Payment Made** column showing the timestamp of the most recent payment received on the case. The column is blank for cases that have not received a payment yet.
- **Filter and pagination persistence**: Filter selections (status, assignees, attorney, settlement status), search term, sort order, and page number persist while you navigate within the dashboard. Returning to the workflow list keeps your previous view in place instead of resetting to defaults. Use the **Reset** link in the filters bar to clear all selections and return to page 1; the link appears whenever any filter is applied or you are past page 1.
- **Unassigned filter**: The assignment filter includes an **Unassigned** option (under an *Assignment Status* group) so you can isolate workflows with no current owner. The workflow list also accepts deep links that pre-apply filters — for example, opening the list from the dashboard's unassigned-workflows widget or from the paralegal report seeds the assignee, status, attorney, or settlement-status filters automatically.
- **Export unassigned workflows to CSV**: From the workflow list, you can export the current set of unassigned workflows to a CSV file. The export reflects the filters currently applied to the list, so narrowing by status or attorney before exporting limits the output to the matching cases. This is useful for triaging assignment backlogs offline or sharing the list with team leads outside Glade.
- **Workflow tags**: Workflows can be labeled with tags to group related cases. Each tag is a short label with an optional emoji icon. The workflow list shows a **Tags** column, and the list filters include a tag filter — pick one or more tags to narrow the list to workflows carrying any of the selected tags (selecting several tags shows cases that match any one of them). When tagging workflows, you can choose from the tags your firm already uses, so the same label and icon stay consistent across cases.
- **Workflow labels**: A firm-managed set of labels can be applied to cases, several at a time. Labels are separate from tags and do not replace them. See [Workflow Labels](./workflow-labels.md).
- The list can also be filtered and sorted by time-sensitive filing deadline (see [Time-Sensitive Filing Deadlines](./time-sensitive-filing-deadlines.md)) and narrowed to stale cases (see [Cases That Have Gone Quiet](./stale-cases.md)).

## Edge Cases & Limitations

- The unassigned-workflows CSV export includes only cases matching the filters currently applied to the list.

## Related Features

- [Status Tracking](./README.md)
- [Workflow Labels](./workflow-labels.md)
- [Time-Sensitive Filing Deadlines](./time-sensitive-filing-deadlines.md)
- [Cases That Have Gone Quiet](./stale-cases.md)
- [Reporting](../../back-office/reporting/README.md)
