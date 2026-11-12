# Firm Default Homepage

## Overview

A firm can pick one of its named dashboards as its **default homepage**. Home shows each person's own widgets only. The default dashboard is a separate dashboard: open it from **Dashboards** at the top of Home, where it is listed by name. Team managers set and clear which dashboard is the default. While it is the default, only Admins and the firm owner can edit it, and everyone else sees it read-only. Nothing is copied onto anyone's personal dashboard.

## Key Behaviors

- **One default per firm.** A firm has at most one default homepage at a time. Choosing a different named dashboard moves the default to it, and the previous dashboard stays as an ordinary named dashboard. The default can also be cleared, which leaves the firm with none.
- **Opened from the dashboard switcher.** Home does not show the default dashboard. Choose it from **Dashboards** at the top of Home. Edits an Admin makes to it — adding, changing, reordering, or removing widgets — are what everyone sees when they open it.
- **Personal widgets are untouched.** Setting, changing, or clearing the default does not add, remove, or change anyone's widgets on Home.
- **Only team managers set or clear the default.** On the named dashboard, **Make firm default homepage** sets it and **Stop using as firm default** clears it. The dashboard is tagged **Firm default**. Setting it confirms with **Everyone's homepage now shows this dashboard**. Clearing it confirms with **This dashboard is no longer on everyone's homepage**. Anyone else sees **Only team managers can change the firm default homepage.** While a dashboard is the default, only Admins and the firm owner can rename or delete it or change its widgets. If a Case Worker or Finance team member tries to edit it, the change is refused. Every other named dashboard stays editable by any member.
- **Only a named dashboard qualifies.** A personal homepage dashboard cannot be made the firm default.
- **Simultaneous changes don't overwrite each other.** If someone else changed the default after you loaded it, your change is refused rather than silently replacing theirs. Reload and try again.

### Team dashboard

Glade can set up a named dashboard called **Team dashboard** for a firm and make it the firm default. It contains five widgets:

- **Retain to File**: median days from retainer to filing, by month, over cases filed this year.
- **Cases**: the firm's cases shown as cards.
- A leads → retained → filed funnel of three counts for the current month, each a third of the row wide: **consultations booked**, **retainers signed**, and **cases filed**.

Every date range on it is relative (this year, this month), so the dashboard stays current without anyone editing it. Months are counted in the firm's time zone.

- Home does not show the team dashboard. Open **Team dashboard** from **Dashboards** at the top of Home. It does not include the three starting widgets on Home — to do list, appointments, and cases — which stay on each person's Home.
- The widgets are backed by saved reports. If the firm already has a report with the same name, in any capitalization, that filters the same way, that report is reused. If a report with that name exists but filters differently, Glade creates its own report with " (team dashboard)" added to the name and leaves the firm's report as it was.
- A firm that already has a default homepage does not get a team dashboard.
- The team dashboard is being rolled out by Glade. Contact Glade support if you don't see a firm default homepage.

## Configuration

- **Firm default homepage**: On a named dashboard, a team manager chooses **Make firm default homepage** or **Stop using as firm default**.

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
