# Availability

## Overview

Firms define when they can be booked. Recurring weekly availability patterns, set per team member, are turned into concrete bookable time slots; connected calendars and availability blocks then remove time that should not be offered. The Availability tab in the Bookings section is the central place to review and edit these settings.

## Key Behaviors

### Defining availability

- Firms set up recurring availability patterns by specifying days of the week and start/end times.
- Availability is defined in the firm's local timezone.
- The system generates concrete bookable time slots from these patterns.
- Individual team members can have their own separate availability schedules.
- External calendar events from connected calendars (Google Calendar or Outlook) automatically block availability to prevent double-booking.
- Only events marked as "busy" block availability. Events marked as "free" or "transparent" do not.
- A busy event on the assigned team member's synced calendar **closes the slot outright**, whatever the product's concurrent booking limit. A hearing, focus time, or a block carried over from other practice software means that person is unavailable, not that one place in the slot is taken. Previously such an event counted as a single occupant, so a product allowing several concurrent bookings kept offering the remaining places and clients could book over protected time.
- The concurrent booking limit governs **Glade bookings only**: two clients can still share a genuinely free slot on a product that allows it. The Glade booking and the calendar event Glade created for it count as one, not two, so booking #1's own event never blocks booking #2.
- A synced calendar event does more than hide the slot — it is also enforced when a booking is saved. Creating, rescheduling, or reassigning a booking on top of a hearing or meeting already on the assigned team member's synced calendar is rejected. Previously only Glade's own Blocked windows were enforced at save time, so a slot list that was out of date — or a booking written by a staff member covering for someone else — could still land a client on top of a court hearing. Firm team members can override deliberately with **Schedule Anyway**.
- In addition to recurring availability, you can add **availability blocks** for specific date ranges. Each block has a type that determines its effect on bookable time:
  - **Blocked** — removes the covered times from bookable availability. Clients cannot schedule into these windows. Use this for vacations, court dates, off-site days, or any other time you should not be booked.
  - Other block types (for example, blocks used purely for visual annotation on the calendar) do not remove availability — only blocks marked as Blocked actually prevent new bookings.
- Blocked times are **hard blocks**. They always remove the covered slots from the booking calendar regardless of the product's concurrent booking limit — even a product that allows multiple overlapping bookings does not offer slots inside a blocked window. Firm team members can still book into one deliberately with **Schedule Anyway**, described below.
- A Blocked entry that is not assigned to a specific team member applies to **every team member**. Use this when you need to take the firm off the calendar for everyone at once (for example, an office closure) without creating one entry per team member.
- Firm team members can deliberately book or reschedule into a blocked window using **Schedule Anyway**. When a team member picks a blocked (or otherwise conflicting) slot, Glade asks them to confirm; confirming overrides the block and saves the booking. This lets a firm keep its calendar blocked to pause new bookings while still moving an existing appointment into that time — no need to temporarily reopen the calendar first. See [Conflicts and Concurrent Bookings](./conflicts-and-concurrent-bookings.md).
- Clients and other non-team members cannot book into blocked time even if they reach a blocked slot. For them, attempting to create or reschedule into a blocked window — for example from a stale link or an out-of-date slot list — is rejected with an error rather than silently saved.

### Restricting which minutes a slot can start at

Ordinarily the bookable times inside an availability window are worked out by stepping through it at the appointment type's scheduling interval. A window can instead name the exact minutes past the hour at which an appointment may start, so a firm whose consultations always begin at ten to the hour offers only those times.

- **The allowed start minutes are set on the availability window itself**, so they can differ from one weekday to the next — Monday to Friday 9–5 starting only at :50, Saturday 9–1 starting at :00 and :40. Because windows are defined per team member, two people working the same day can offer different start times.
- **A window with no start minutes set behaves exactly as before**, stepping through the window at the scheduling interval.
- **Everything else that closes a slot still applies.** An allowed start time is only offered if the slot is free — blocked windows, conflicts on a synced Google or Outlook calendar, the concurrent booking limit, and the minimum booking notice all still remove it.
- **An appointment type that already had start times restricted for the whole service keeps working.** Those times continue to apply until the weekly schedule for the service is saved again, at which point the per-day windows take over. Re-save the schedule when you want a service to move onto per-day start times.

> TODO: Confirm where the allowed start minutes are entered in the Availability editor and how the control is labeled — the source change does not establish the settings screen.

### Availability management view

The **Availability** tab in the Bookings section gives you a centralized place to review and manage availability across all services and team members.

The tab has two sub-views:

- **Team Members**: Shows availability settings organized by team member.
- **Services**: Lists all schedulable services. For each service, a summary shows which team members have availability configured. Clicking a service name opens the availability editor for that service inline. A **View in services** link navigates to the full service settings page.

Clicking a service in either view opens the availability editor directly — you can update availability without leaving the Bookings section.

## Configuration

| Setting | Description |
|---------|-------------|
| Availability patterns | Days of the week and start/end times, configured per team member. |
| Allowed start times | The exact minutes past the hour at which an appointment may start, set on an individual availability window. Empty until set, in which case slots follow the scheduling interval. |

## Edge Cases & Limitations

- If no team member availability is configured for a product, the product may show no available time slots.
- External calendar events marked as "free" do not block availability. Only "busy" events create blocks.
- Allowed start times narrow a window rather than extend it — they select from the times the window would otherwise offer. A window whose listed start times do not fall inside its own hours offers nothing at all.
- A service that previously had its start times restricted for the whole service keeps those times on every day until its weekly schedule is saved again. Until then the per-day windows have no effect.

## Related Features

- [Scheduling](./README.md)
- [Minimum Booking Notice](./minimum-booking-notice.md)
- [Conflicts and Concurrent Bookings](./conflicts-and-concurrent-bookings.md)
- [Timezones](./timezones.md)
- [Calendar Sync](../calendar-sync/README.md)
