# Conflicts and Concurrent Bookings

## Overview

When a requested time overlaps an existing booking, a busy event on a synced calendar, or a Blocked availability window — or when a slot has already reached its product's concurrent booking limit — Glade refuses the booking or asks a team member to confirm it deliberately with **Schedule Anyway**. This doc covers how conflicts are detected, how capacity is counted, and when the override applies.

## Key Behaviors

### Booking into a conflicting time

- When a selected slot conflicts with an existing booking, the scheduler flags the conflict and offers **Schedule Anyway** so a team member can double-book deliberately.
- **Schedule Anyway** works both when creating a booking and when rescheduling one. Previously it was only honored on the reschedule path — on a new booking the click appeared to do nothing and the appointment was never created. If your team hit that and worked around it by booking a non-conflicting time and then rescheduling into the conflict, that workaround is no longer necessary.
- **Schedule Anyway** also covers a **Blocked** availability window. A firm team member who selects a blocked slot is asked to confirm, and confirming saves the booking into that window — so a firm can keep its calendar blocked to pause new bookings while still moving an appointment into that time. Clients and other non-team members cannot book into blocked time this way; for them a blocked window remains a hard block. See [Defining availability](./availability.md#defining-availability).
- **Events on a synced calendar are treated the same way.** An appointment that would overlap a hearing, meeting, or other busy event on the assigned team member's connected calendar is refused unless a team member confirms **Schedule Anyway**. This applies when creating a booking, when rescheduling one, and when reassigning a scheduled booking to a different team member — so covering for a colleague no longer risks booking a client over that colleague's court hearing.
- Moving a booking is not blocked by the calendar event Glade created for the booking itself, so rescheduling an appointment to a new time works normally.
- Only calendars that are switched on for syncing are checked. An event on a calendar the team member has disabled does not block the booking, matching what the slot list shows.

### Booking a slot that is already full

A slot is full when the number of **Glade bookings** already held for that team member has reached the product's concurrent booking limit. Booking into a full slot is refused, and the refusal is visible at the moment of booking.

- The booking fails with an error instead of showing a confirmation. Previously the confirmation screen appeared even when the booking had not been saved, so a client or staff member could be told an appointment existed when it did not — no calendar event was created, no reminders were sent, and any workflow the appointment was meant to start never ran. If your team has seen "confirmed" consultations that never appeared on anyone's calendar, this is the cause.
- Products configured for several concurrent bookings behave as configured: booking #1's own calendar event does not count a second time and does not prevent booking #2.
- **Busy events on a synced calendar are not counted — they block.** An external hearing or focus-time block takes the team member off the calendar for that window entirely, so a product allowing five concurrent bookings offers none inside it. Previously the event counted as one occupant and the remaining places stayed bookable, which let clients book over protected time.
- A booking with nobody assigned is checked against the firm calendar owner's calendar, so a busy event there blocks it too.
- **Blocked** availability windows are unaffected. They remain a hard block regardless of the concurrent booking limit, and firm team members override them with **Schedule Anyway** as described above.

A slot that fills between the moment the client loads the time list and the moment they confirm is the common way to hit this. Reloading the booking calendar shows the slot as taken.

### Counting concurrent bookings per appointment type

By default a slot's occupancy is counted across the team member's whole calendar: a booking of any appointment type at 2pm counts toward the concurrent booking limit of every other appointment type at 2pm. A firm running several consultation types alongside each other — an intake consultation and a sign-and-pay appointment, say — can have each type counted on its own instead, so that booking one does not take capacity away from the other.

- With the option on, only bookings of the **same** appointment type count toward that type's concurrent booking limit. Each type offers its own slots up to its own limit, so two services can each run at 2pm.
- **Busy time still blocks every type.** An event on the assigned team member's synced calendar, and a **Blocked** availability window, remove the slot from every appointment type regardless of this setting.
- The calendar event Glade creates for a booking is not counted against other types — another service's booking does not block a slot through its own calendar event.
- The option is **off for every firm** until it is turned on, so a firm relying on one shared limit across its calendar is unaffected. Turning it on changes which slots clients are offered, so review each appointment type's concurrent booking limit before enabling it.

> TODO: Confirm where the setting appears in the appointment type's Product details and what it is labelled there.

## Configuration

| Setting | Description |
|---------|-------------|
| Concurrent bookings | Maximum number of overlapping Glade bookings allowed per time slot. Default is 1. Busy time on a synced external calendar blocks the slot regardless of this setting. |
| Count concurrent bookings per appointment type | Whether each appointment type's concurrent booking limit is counted against bookings of that type only, rather than against every booking on the team member's calendar. Set for the firm, and off until your firm turns it on. |

## Edge Cases & Limitations

- Counting concurrent bookings per appointment type is a firm-wide choice, not a per-appointment-type one. It applies to every appointment type at once.
- Concurrent booking limits are per time slot, not per day.
- A booking with nobody assigned is measured against the firm calendar owner's bookings and calendar rather than being left unchecked.
- Enforcement against synced events depends on the event having reached Glade. A commitment a team member blocked out directly in Outlook that has not yet synced is not known to Glade and does not prevent a booking.
- Products that allow several concurrent bookings offer fewer slots than before wherever a team member's synced calendar carries busy time. This is deliberate — those slots were never genuinely free — but a firm relying on concurrent stacking will see its availability tighten.

## Related Features

- [Scheduling](./README.md)
- [Availability](./availability.md)
- [Appointment Types](./appointment-types.md)
- [Booking Lifecycle](./booking-lifecycle.md)
- [Calendar Sync](../calendar-sync/README.md)
