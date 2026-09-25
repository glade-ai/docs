# Minimum Booking Notice

## Overview

Each appointment type carries a **minimum booking notice** — how much warning your firm needs before an appointment starts. Clients cannot book a time that falls inside the notice window; firm team members can.

## Key Behaviors

- The notice is set per appointment type under **Availability → Booking settings**, and the choices are same day, 8 hours, 24 hours, 48 hours, 72 hours, 5 days, or 7 days.
- Time slots that fall inside the notice window are not offered to clients. A firm needing a day's warning shows tomorrow's slots but not this afternoon's.
- **The window is enforced when the booking is saved, not just hidden on the calendar.** Previously it only controlled which slots were displayed, so a client working from a stale slot list, an old link, or a page left open could still book a time the calendar had deliberately hidden. That booking is now refused.
- **Firm team members are not held to the window.** Staff booking a client in, or moving an existing appointment, can still use a time inside the notice period — useful for taking a same-day appointment over the phone on a service that otherwise requires notice.
- An appointment type with no notice set allows same-day booking. Choosing **same day** explicitly has the same effect and is worth setting deliberately on services where same-day consultations are part of how your firm works.
- This is a per-appointment-type setting, so a firm can require a week's notice for a signing while leaving consultations open same day.

## Configuration

| Setting | Description |
|---------|-------------|
| Minimum booking notice | How far ahead of the appointment a client must book: same day, 8, 24, 48, or 72 hours, or 5 or 7 days. Set per appointment type under Availability → Booking settings. Appointment types with nothing set allow same-day booking. |

## Edge Cases & Limitations

- The minimum booking notice applies to clients only. It does not stop a team member booking or moving an appointment inside the window, so it is not a way to protect a team member's time from their own colleagues — use a **Blocked** availability window for that (see [Availability](./availability.md)).
- Changing the minimum booking notice does not affect appointments already booked. A client who booked before the change keeps their time.

## Related Features

- [Scheduling](./README.md)
- [Availability](./availability.md)
- [Booking Lifecycle](./booking-lifecycle.md)
