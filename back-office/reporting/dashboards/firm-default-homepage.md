# Firm Default Homepage

## Overview

A firm can pick one of its named dashboards as its **default homepage**. Every member's homepage then shows that dashboard live, above their own personal widgets, so the team shares the same views without each person building them. It reaches new hires and existing staff alike, and a change an Admin makes to it shows up for everyone. Nothing is copied into anyone's personal dashboard.

## Key Behaviors

- **One default per firm.** A firm has at most one default homepage at a time. Choosing a different named dashboard moves the default to it, and the previous dashboard stays as an ordinary named dashboard. The default can also be cleared, which leaves the firm with none.
- **Shown live on every homepage.** Each member's homepage shows the default dashboard's widgets above their own personal widgets. Nothing is copied, so edits to the default (adding, changing, reordering, or removing widgets) appear on everyone's homepage, and a team member who joins later sees the same thing.
- **Personal widgets are untouched.** The default sits above each person's own homepage widgets. Setting, changing, or clearing it does not add, remove, or change anyone's personal widgets.
- **Only Admins and the firm owner manage it.** Choosing or clearing the default is limited to Admins and the firm owner. While a dashboard is the default, the same restriction applies to renaming or deleting it and to adding, editing, reordering, or removing its widgets, because a change there is a change for the whole firm. If a Case Worker or Finance team member tries, the change is refused. Every other named dashboard stays editable by any member.
- **Only a named dashboard qualifies.** A personal homepage dashboard cannot be made the firm default.
- **Simultaneous changes don't overwrite each other.** If someone else changed the default after you loaded it, your change is refused rather than silently replacing theirs. Reload and try again.

### Team dashboard

Glade can set up a named dashboard called **Team dashboard** for a firm and make it the firm default. It contains five widgets:

- **Retain to File**: median days from retainer to filing, by month, over cases filed this year.
- **Cases**: the firm's cases shown as cards.
- A leads → retained → filed funnel of three counts for the current month, each a third of the row wide: **consultations booked**, **retainers signed**, and **cases filed**.

Every date range on it is relative (this year, this month), so the dashboard stays current without anyone editing it. Months are counted in the firm's time zone.

- The team dashboard leaves out the three standard homepage widgets, because each person's homepage already shows them directly below the firm default.
- The widgets are backed by saved reports. If the firm already has a report with the same name, in any capitalization, that filters the same way, that report is reused. If a report with that name exists but filters differently, Glade creates its own report with " (team dashboard)" added to the name and leaves the firm's report as it was.
- A firm that already has a default homepage does not get a team dashboard.

> TODO: Confirm whether the team dashboard has been rolled out to all firms, and whether a firm can ask for it.

## Configuration

- **Firm default homepage**: An Admin or the firm owner picks it from the firm's named dashboards, or clears it so there is none.

> TODO: Confirm where in the interface the default homepage is chosen and cleared.

## Edge Cases & Limitations

- Once a named dashboard becomes the default, team members without Admin rights can no longer edit it. To let them edit it again, an Admin clears the default or picks another dashboard.
- If the dashboard you pick was deleted in the meantime, the change fails and the previous default stays in place.
- Only Admins and the firm owner can delete the default dashboard. Once it is deleted, the firm has no default homepage until someone picks another one.
- Only one dashboard can be the default. A firm that wants different views for different roles has to keep them on ordinary named dashboards.

## Related Features

- [Dashboards](./README.md)
- [Named Dashboards](./named-dashboards.md)
- [Default Homepage Widgets](./default-homepage-widgets.md)
- [Time from Retainer to Filing](../custom-reports/retainer-to-filing.md)
- [Staff Management](../../staff-management.md): Admin, Case Worker, and Finance roles
