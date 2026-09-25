# How Sync Works

## Overview

Calendar sync runs in both directions: events on connected calendars flow into Glade to block availability, and Glade bookings are written out to the assigned team member's calendar. Changes arrive in real time through provider push notifications, backed by an hourly catch-up job. This page covers what syncs in each direction, how real-time sync and catch-up work, and how booking events follow reassignment between team members.

## Key Behaviors

### Two-way sync

- **Inbound (external to Glade):** Events from connected calendars are pulled into Glade. These events block scheduling availability, preventing clients from booking during times when the firm member has existing commitments.
- **Outbound (Glade to external):** When a booking is created, rescheduled, or canceled in Glade, a corresponding event is automatically created, updated, or removed in the connected external calendar.

### What syncs

| Direction | What syncs | What does not sync |
|-----------|------------|-------------------|
| External to Glade | Event start and end times (for availability blocking), and the event title — visible only to the team member who owns the calendar | Event descriptions, attendees, or other details |
| Glade to external | Booking details: time, duration, client name, meeting link | Changes made to the external event after initial sync |

### Real-time sync

- Google Calendar uses Google's push notification (webhook) system. Glade is notified instantly when a Google Calendar event changes.
- Outlook uses Microsoft Graph subscriptions. Glade receives real-time notifications when Outlook events change.
- No manual sync is needed. Changes are picked up automatically.
- Google webhook subscriptions auto-renew before expiration (approximately 30 days).
- If Glade cannot process a change right away — for example, during a brief Google or Microsoft outage — it keeps trying until the change goes through. Previously a momentary failure dropped the update silently and the calendar stayed out of step until the next change came in.
- Changes to the same calendar are processed one at a time in the order they arrive, so a rapid burst of edits cannot overwrite one another.
- A calendar that has been deleted at the provider stops syncing instead of being retried. Disconnect and reconnect the account if you delete a synced calendar and later recreate it.

### When provider notifications go quiet

Real-time notifications are the normal path, but a provider subscription can lapse or fall silent. A background job runs every hour and catches those calendars up, so an event that never triggered a notification still lands in Glade.

- Any enabled calendar that has not synced in the last **two hours** is pulled in by the catch-up job. Previously the job waited until a calendar had gone a full day without syncing, so a busy-block added by hand could stay invisible to Glade — and stay bookable over — for more than 24 hours.
- A calendar that has **never** synced is picked up as well. Previously those were skipped entirely, so a newly enabled calendar whose first notification never arrived was never caught up.
- Calendars that have synced recently are left alone, and disabled calendars are never synced, however stale they are.
- The catch-up fetches only what changed since the last sync where the provider supports it, so tightening the window does not slow syncing down.
- If Glade cannot establish a real-time subscription with Outlook, it retries within the hour instead of waiting until the subscription would have expired two days later. A calendar therefore does not sit without live updates for days after a single failure.

### Booking events and reassignment

- When a client books with a specific team member, only that member's calendar conflicts are checked.
- When a booking is reassigned to a different team member, its calendar event moves with it: Glade creates the event on the newly assigned member's connected calendar and removes it from the previous member's calendar, so the appointment always lands on the calendar of the person actually assigned.
- **Changing only the assignee is enough to move the event.** Previously the move happened only when the booking was also given a new time, so handing an appointment to a colleague at the same time left the event sitting on the original member's calendar and it never appeared on the new member's at all. Reassigning on its own now moves it, for every appointment type.
- **If the new assignee has no connected calendar**, the event is removed from the previous member's calendar and no replacement is created. The booking itself is unaffected — it stays in Glade under the new assignee, and the event appears once that person connects a calendar and the booking is next updated.
- A booking that is reassigned and moved to a new time in one edit produces a single event on the new member's calendar, not two.

## Edge Cases & Limitations

- Inbound sync covers event times and the event title. Descriptions and attendee lists are not brought across, and a title is shown only to the team member who owns the calendar it came from — see [Who can read a synced event's title](./availability-blocking.md#who-can-read-a-synced-events-title).
- Changes made directly to a synced event in the external calendar (after Glade created it) are not synced back to Glade.
- There is no manual "sync now" button on this screen. Sync happens automatically through provider notifications, backed by the hourly catch-up job described above.
- The sync window covers the next three months. Events further in the future are not synced until they fall within that window.
- Reassigning a booking does not override an appointment type that routes its bookings to a particular calendar by county. Where county routing applies, the booking keeps the calendar that routing chose.

## Related Features

- [Calendar Sync](./README.md)
- [Connecting Calendars](./connecting-calendars.md)
- [Availability Blocking](./availability-blocking.md)
- [Scheduling](../scheduling/README.md)
