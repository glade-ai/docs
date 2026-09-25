# Team Member Assignment

## Overview

Bookings can be assigned to specific team members within the firm, either by default per product, by workflow rules, or by hand. The Bookings section's List, Calendar, and Team views follow whichever team member you have selected.

## Key Behaviors

### Assigning bookings to team members

- Bookings can be assigned to specific team members within the firm.
- A default team member can be set per product, so new bookings are pre-assigned.
- Team members can be reassigned after booking.
- A booking created without a specific team member is treated as belonging to the calendar owner and is shown under the owner's name. When you filter the bookings list (or the **Your appointments** widget) by the calendar owner, these unassigned bookings appear alongside the ones explicitly assigned to the owner. Filtering by any other team member shows only the bookings explicitly assigned to that person.
- When connected to a workflow, team assignment follows workflow rules.
- Each team member's individual availability is checked when assigning.
- When a workflow has an assigned attorney, the scheduling modal automatically opens to that attorney's availability. This applies in the client portal (Home Page booking tasks) and on the firm-side Bookings tab. If the assigned attorney has no availability, a message indicates this and you can select another team member from the available chips. Selecting a different team member chip always shows their calendar, even if they have no availability.

### Which team member the Bookings section is showing

The Bookings section has List, Calendar, and Team views, and the team member you are looking at carries across them. Whoever you have selected stays selected as you move between views, so you no longer have to re-pick them each time.

- Opening a booking in List view and switching to Calendar shows **that booking's team member's** calendar. Previously the calendar reset to the appointment type's default assignee, so opening one team member's booking could land you on someone else's calendar.
- **Block this Time** applies to the team member currently selected, rather than always to the appointment type's default assignee. Check who is selected before blocking time.
- The Team view's team member filter lists every member of the firm, including people with no appointments booked. Previously anyone without a booking dropped out of the filter entirely, so they could not be selected.
- Once you have picked a team member by hand, that choice stays put — a change to the appointment type's default assignee, or bookings reloading in the background, does not switch the view away from the person you chose.

## Configuration

| Setting | Description |
|---------|-------------|
| Default team member | Pre-assigned team member for new bookings on this product. |

## Edge Cases & Limitations

- Booking a time slot does not guarantee a specific team member unless one is pre-assigned to the product.

## Related Features

- [Scheduling](./README.md)
- [Availability](./availability.md)
- [Conflicts and Concurrent Bookings](./conflicts-and-concurrent-bookings.md) — conflict checks when reassigning a booking
- [Workflow Bookings](./workflow-bookings.md)
