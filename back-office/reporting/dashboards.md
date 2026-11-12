# Dashboards

## Overview

Alongside the personal dashboard each person sees on their own homepage, a firm can build **named dashboards** that everyone at the firm shares. Both are built from widgets, and a new team member's homepage starts with a default set of widgets.

## Key Behaviors

### Named dashboards

- A named dashboard belongs to the firm, not to the person who created it. Every member sees the same dashboard and the same widgets on it.
- Dashboard names are unique within the firm, and matching ignores capitalization — "Intake" and "intake" are treated as the same name.
- Widgets are added to a named dashboard, reordered, and removed the same way they are on the personal homepage dashboard. Each widget keeps its own filters, sorting, and choice of columns.
- Personal homepage dashboards are unaffected. Each person still has exactly one, and it stays private to them.

### Default homepage widgets

A new team member's personal homepage starts with three widgets already on it, rather than an empty dashboard:

- **To do list** — two columns wide, showing 10 items, newest first.
- **Appointments** — one column wide, showing the next 5 upcoming appointments.
- **Cases** — one column wide, showing the 5 newest cases.

These are ordinary widgets: they can be moved, changed, or removed like any widget you add yourself. Existing team members whose homepage has no widgets on it can be given the same starting layout. A homepage that already has at least one widget is never changed.

> TODO: Confirm where named dashboards are created and managed in the interface, and whether any firm-level permission controls who can create or edit them.

### Workflow cards

The workflows widget and the custom-report widget can show cases as cards. Two of the figures on each card measure real case progress:

- **Documents outstanding** shows how many of the files a case's checklists require are still not complete, out of the total required — for example, 3 of 7. It counts required file slots across the case's active checklists. A file still marked incomplete or needing action counts as outstanding.
  - Skipped checklists, checklists still waiting on their workflow step, and optional file slots are not counted.
  - Checklists built from a template your firm has since archived are still counted, because they still appear in the case's checklist panel. The card and the panel therefore agree.
  - Previously this figure showed the client's pending task count.
- **Questionnaire** shows how far along the questionnaire the petition is generated from is — the bankruptcy schedules, or the emergency filing questionnaire. The percentage is required visible questions answered out of required visible questions. This is the same rule the questionnaire uses for its section progress, so the card matches what you see when you open the questionnaire.
  - A case linked to another case in the same group, such as a retainer case linked to the petition case, shows the petition case's questionnaire.
  - Skipped questionnaires are not counted.
  - Previously this figure showed overall task progress.

## Configuration

- **Named dashboards**: Created per firm and shared by everyone in it. Names must be unique within the firm.

## Edge Cases & Limitations

- A named dashboard cannot reuse the name of another named dashboard at the same firm, regardless of capitalization.
- The default homepage widgets are added only to a homepage with no widgets on it. A homepage you have already customized, even with a single widget, keeps exactly what is on it.

- The **Documents outstanding** and **Questionnaire** figures on workflow cards appear only to firm staff. If the checklist counts can't be loaded, the cards show "—" for that figure and the rest of the list still loads.
- The **Questionnaire** percentage is only available for questionnaires on Glade's current questionnaire engine. For other questionnaires, or before progress has been calculated, the card shows the questionnaire's status instead of a percentage. Progress updates shortly after answers are saved, not instantly.

> TODO: Confirm whether an emptied homepage is re-seeded with the default widgets, and when the default layout is applied to existing team members with empty homepages.

## Related Features

- [Reporting](./README.md)
- [Custom Reports](./custom-reports/README.md)
- [Time from Retainer to Filing](./custom-reports/retainer-to-filing.md) — adding the average to a dashboard
