# Paralegal Report

## Overview

The Paralegal Report shows per-paralegal workload metrics so a firm can see how many cases each paralegal is preparing, has filed, or has lost, and how their active cases break down by custom status.

## Key Behaviors

- Shows per-paralegal workload metrics: cases in preparation, cases filed, filing rate, dropped cases, paused cases, and archived cases.
- Breaks down active (non-paused, non-archived) cases by custom status, showing counts per status per paralegal.
- Filing rate is the percentage of cases filed out of the total cases in preparation plus cases filed.
- Cases are classified as dropped if they were canceled or ended, filed if a filing date is recorded, or in preparation otherwise.
- CSV export includes a total row with summed columns and averaged filing rate.
- **A paralegal keeps credit for a case after being removed from it.** A case counts toward every team member in a paralegal role who was assigned to it at any point from the start of the schedule builder onward, including one who was later unassigned. Firms that hand a case to a filing team and unassign the paralegal at that point no longer see the case drop out of the paralegal's row at the moment it is filed. Previously the report credited only the people currently assigned, so it undercounted cases written and, especially, cases filed for those firms. The CSV export follows the same rule.

## Configuration

- **Date range**: The report requires or accepts a start date and end date.

## Edge Cases & Limitations

- A paralegal unassigned from a case before the schedule builder was started on it gets no credit for that case.
- A case with two paralegals assigned counts once toward each of them.

## Related Features

- [Reporting](./README.md)
- [Documents Report](./documents-report.md)
- [Intake Status Report](./intake-status-report.md)
- [Staff Management](../staff-management.md) — the report segments by workflow role.
- [Settings](../settings.md) — custom statuses affect the status breakdown columns.
