# Appointment Types

## Overview

Appointments in Glade are configured as products. Each appointment type defines what kind of session it is, how long it runs, how its slots are spaced, what it costs, and how its bookings look on the firm's booking calendar.

## Key Behaviors

### Appointment types

- Appointments are configured as products. Each product has a type: Online Session (video call), In-Person Session, Consultation, or Chat Session.
- Each product can be free or paid, with one or more pricing tiers.
- Products define session duration, scheduling interval (the gap between available time slots), and buffer time (preparation time before and after appointments).
- Products can enable or disable automatic video conference link generation.
- Products can set a concurrent booking limit, which controls how many overlapping bookings are allowed in the same time slot. The default is 1. See [Conflicts and Concurrent Bookings](./conflicts-and-concurrent-bookings.md).
- A custom confirmation message can be configured per product and is shown to clients after booking.
- Each appointment type can be given a calendar color, used to tint its bookings on the firm's booking calendar. See [Color-coding appointment types on the calendar](#color-coding-appointment-types-on-the-calendar).

### Color-coding appointment types on the calendar

Each appointment type can be given a color. Bookings of that type are tinted with it on the firm's booking calendar, so the calendar shows at a glance which kind of appointment each block is — a consultation, a signing, a status check-in.

- The color is set on the appointment type itself, alongside its other settings, and applies to every booking of that type.
- Your firm picks the colors. No color carries a fixed meaning and there is no preset mapping, so choose whatever scheme matches how your team reads the calendar.
- **The color follows the appointment type, not the team member.** Two appointment types assigned to the same person show as two colors; one appointment type spread across several team members shows as one.
- Appointment types have no color until you set one, so a firm that has not chosen colors sees the calendar exactly as before. Clearing a color returns that type's bookings to the standard appearance.
- This is a display setting. It does not affect availability, booking rules, assignment, or reminders.

> TODO: Confirm where the color is chosen in the dashboard, whether a palette is offered or any color can be picked, and whether the color appears anywhere other than the booking calendar.

## Configuration

| Setting | Description |
|---------|-------------|
| Product type | Online Session, In-Person Session, Consultation, or Chat Session. |
| Session duration | Length of each appointment. |
| Scheduling interval | Minimum gap between available time slots. |
| Buffer time | Preparation time added before and after appointments. |
| Concurrent bookings | Maximum number of overlapping Glade bookings allowed per time slot. Default is 1. Busy time on a synced external calendar blocks the slot regardless of this setting. |
| Video conference link | Whether to auto-generate a video meeting link for the appointment. |
| Custom confirmation message | Message shown to the client after booking is confirmed. |
| Calendar color | Color used to tint this appointment type's bookings on the firm's booking calendar. Optional — appointment types have no color until one is set. |

## Edge Cases & Limitations

- Calendar colors are read from the appointment type each time the calendar is drawn, so changing a color re-tints that type's existing bookings as well as new ones. There is no way to color one booking differently from others of the same type.

## Related Features

- [Scheduling](./README.md)
- [Availability](./availability.md)
- [Conflicts and Concurrent Bookings](./conflicts-and-concurrent-bookings.md)
- [Booking Lifecycle](./booking-lifecycle.md) — the per-product 48-hour reschedule rule
- [Video Consultations](../video-consultations.md)
