# Time-Sensitive Filing Deadlines

## Overview

Some cases have to be filed with the court under time pressure — an emergency Chapter 13 filed ahead of a foreclosure sale, or a case racing a wage garnishment. Glade tracks that pressure on the case so your team can find these cases and work them in order rather than remembering them by hand. A case can be marked as urgent either by a specific calendar date it has to reach the court by, or by the *kind* of pressure it is under — a garnishment, repossession, foreclosure, or eviction — when nobody knows the date yet. This is separate from the filed date, which records when a case was actually filed.

## Key Behaviors

- **Two ways to mark a case urgent** — a case's settings let you record a **filing deadline** as a calendar date, a **type** of urgency, or both. A case is time sensitive if it carries either one.
- **The type** describes what the client is up against: **garnishment**, **repossession**, **foreclosure**, **eviction**, or **other**. It exists because clients frequently know that a garnishment or a repossession is coming without knowing the day it lands. Marking the type records the urgency straight away, and the date can be added later if it is ever pinned down.
- **Notes about the urgency** — an optional **reason** can be written alongside, explaining the situation in the client's own terms. The reason is now independent: it can be recorded on a case that is *not* time sensitive, so an intake worker who asks the question and hears "no" still has somewhere to put what the client told them. A reason on its own does not mark the case urgent.
  - Previously a date was required before a case could be marked time sensitive at all, and a reason could only be saved attached to one. Intake staff either invented a date or lost the client's answer.
- **Notes on a case that is not time sensitive** — where a staff member answers **No** to time-sensitive at case creation but writes notes anyway, those notes are posted as an internal note on the case, authored by whoever created it. They appear in the same internal notes thread the team already reads. Answering **Yes** keeps the reason on the time-sensitive fields rather than duplicating it as a note, and leaving the notes blank creates nothing.
- **Setting these at case creation** — the deadline, the type, and the reason can all be entered when a staff member initiates a case, so an urgent filing carries the marking from the moment it exists.
- **Who set it** — Glade records which team member marked the case and when. On a case created already marked, the person who created the case is recorded.
- **Clearing the marking** — clearing both the deadline and the type makes the case no longer time sensitive. The reason is left alone, because it may be the only record of what the client said; clear it separately if it no longer applies.
- **The date does not shift** — the deadline is a calendar day the court cares about, so it reads the same regardless of anyone's timezone.
- **Filtering, sorting, and reporting** — the workflow list can be filtered to time-sensitive cases only (or to cases that are not time sensitive), narrowed to deadlines falling inside a date range, and sorted by deadline. Cases marked by type with no date are included in the time-sensitive filter, and are excluded by a date-range filter, since they have no date to fall inside it. Cases with no deadline sort to the end in both directions. The cases CSV export includes both a filing-deadline column and a type column, so a case marked by type alone is not a blank row in the spreadsheet.
- **Activity history** records a marking being set — including a type-only marking — and records it being cleared when both the deadline and the type are removed.

### Deadlines across related cases

A matter can carry several cases at once — an associated filing alongside the main one, or a new case created when a chapter converts. Each case carries its own marking, because associated filings can genuinely be due on different dates.

- A case joining a matter that is already marked time sensitive **inherits the most recent marking** on that matter — its deadline, its type, its reason, and the record of who set it — provided the joining case is not marked itself.
- Inheritance follows the marking, not the date. A matter marked by type alone passes that type on, even though there is no date to pass with it.
- A case created with its own deadline or type keeps it instead of inheriting.
- A reason on its own is not inherited, because a reason on its own does not mark a case.
- Answering explicitly that a new case is **not** time sensitive suppresses inheritance — it stays unmarked.
- When you create an associated case, the wizard shows the matter's most recent marking so you can carry it over or override it deliberately.

## Edge Cases & Limitations

- The workflow list filters, the deadline sort, and the CSV export read the time-sensitive marking from the matter's main case. A marking set directly on a non-main case in the same matter is saved and shown on that case, but does not surface in those list views.
- The filing deadline is not a status. Setting one — or setting a type — does not change the case's status, and passing the deadline does not move the case or raise an alert on its own.
- The urgency type is a fixed list (garnishment, repossession, foreclosure, eviction, other). Anything else goes in the reason. Use **other** with a reason for a situation the list does not cover.
- A case marked by type with no date cannot be found by filtering on a date range, and sorts with the undated cases. Add the date once it is known if the case needs to appear in a date-bounded view.

## Related Features

- [Status Tracking](./README.md)
- [Workflow List](./workflow-list.md)
- [Case Status](./case-status.md)
- [Foreclosure Alerts](../foreclosure-alerts.md)
