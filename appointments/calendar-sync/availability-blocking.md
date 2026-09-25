# Availability Blocking

## Overview

Busy events on a team member's synced calendars block their bookable availability in Glade, so clients cannot book over existing commitments. This page covers which events block time, how blocks interact with concurrent bookings, how the block is enforced when a booking is saved, and who can read the title of a synced event.

## Key Behaviors

### Which events block time

- All synced external events marked as "busy" create blocks in Glade's scheduling calendar.
- Events marked as "free" or "transparent" in the external calendar do not block availability.
- When a client views available time slots, any time covered by an external "busy" event is hidden.
- This prevents double-booking across Glade and external calendars.
- Availability blocking applies per team member. A member's external events only affect their own availability.

### Busy events and concurrent bookings

- A "busy" event closes the slot outright. It means the team member is unavailable, so it blocks the time regardless of how many concurrent bookings the appointment type allows — focus time, a court hearing, or a block carried over from other practice software all take the team member off the calendar entirely. Previously a busy event took only one place in the slot, so an appointment type configured for several concurrent bookings kept offering the remaining places and clients could book over protected time.
- The concurrent booking limit governs **Glade bookings only**. Two clients can still share a genuinely free slot on an appointment type that allows it, and the event Glade itself puts on the calendar for a booking is not counted a second time on top of the booking.
- When sync has picked up the booking's own Outlook or Google event twice, the extra copy is recognized as the booking's own event and ignored. Occasionally the same calendar event reaches Glade as two copies a moment apart; previously the extra copy was treated as separate busy time — for example Focus Time — which could close a concurrent slot that still had room. A genuinely separate busy event on the same calendar still blocks the time as usual.

### Enforcement when a booking is saved

- The block is enforced when a booking is saved, not only when slots are displayed. A booking that would overlap a busy event on the assigned team member's synced calendar is refused — including when a booking is rescheduled, and when a scheduled booking is reassigned to a team member who has a conflicting event. A firm team member can still override with **Schedule Anyway**; clients cannot. Only calendars enabled for syncing are checked.
- A booking with nobody assigned is checked against the **firm calendar owner's** calendar rather than skipped. This covers the public booking page and a reschedule made before anyone is assigned, so a client cannot book over the owner's busy time simply because the booking has no assignee yet.

### Who can read a synced event's title

A busy block drawn from a connected calendar shows what the event is called only to the team member whose calendar account it came from. Everyone else at the firm sees the same block of time labeled **Busy**, with no title.

- Start and end times are unchanged for everyone, so availability and double-booking protection read exactly the same whichever team member is looking.
- This matters most where one person works for more than one firm and connects a single calendar to each of them. The same event then appears on every one of those firms' Glade calendars, and its title used to travel with it — so one firm could read another firm's client names off its own bookings calendar. Only the calendar's owner sees the words now.
- A block with no title is shown as **Busy**, the same as a genuinely untitled event. You cannot tell the two apart from the calendar.
- Blocked time Glade builds from your firm's own availability settings is not affected and keeps its label for everyone.
- Court hearings Glade places on a team member's calendar are synced events like any other, so the hearing's title reads as **Busy** to everyone except that team member. The hearing itself is still on the case and on the court calendar, where the whole team can read it.
- A booking made through Glade is unaffected: the calendar draws bookings from your firm's own booking records, so the appointment card keeps its real title for the whole team.

## Edge Cases & Limitations

- Hiding titles from other team members limits what a firm can read; it does not separate the calendars themselves. A calendar connected to more than one firm still contributes its busy time to every one of them, so those firms can see when that person is unavailable even though they cannot see why.
- Events marked as "free" or "transparent" in external calendars do not block availability. This is by design but can cause confusion if users expect all events to block.
- Only events that have reached Glade can block a booking. If a team member marks time as busy in Outlook and that change has not synced through, Glade does not know about it and will not stop a booking in that window.
- A busy event on a synced calendar blocks the time for everyone booking that team member, including on appointment types that allow several concurrent bookings. If your firm relied on concurrent slots staying open alongside external events, those slots now close.
- All-day events are handled based on the firm's configured timezone.
- **An all-day Busy event in Outlook blocks the whole day.** A single all-day event marked Busy — a day out of the office, for example — hides every bookable slot on that day, including on public booking pages. Previously some Outlook all-day events were recorded as taking up no time at all, so clients could still be offered and book slots on days that Outlook and the Glade calendar both showed as blocked. Events already synced this way block their day immediately; no resync is needed.

## Related Features

- [Calendar Sync](./README.md)
- [How Sync Works](./sync-behavior.md)
- [Court Hearing Sync](./court-hearing-sync.md)
- [Scheduling](../scheduling/README.md)
