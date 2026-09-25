# Client Booking Flow

## Overview

Clients book appointments by choosing a product or service, picking an open date and time from the firm's availability, and confirming. This doc covers the steps a client goes through, how the booking calendar behaves while it loads, and booking from a firm member's profile **Meetings** tab.

## Key Behaviors

### Client booking flow

1. The client views the firm's product or service listing. For free sessions, the booking button reads **Book a call**; for paid sessions it shows the session price.
2. The client selects a product and initiates scheduling.
3. A calendar displays available dates and time slots.
4. Times are shown in the client's own timezone, with a timezone picker above the slot list if they want to view them in a different one. See [Timezones](./timezones.md).
5. The client selects a date and time.
6. The booking is confirmed and created.
7. If the product has video conferencing enabled, a meeting link is generated automatically.
8. The client receives a confirmation with booking details.

### While the booking calendar is loading

A consultation calendar has to fetch a month's availability before it can show which days are open. Until that finishes, the calendar makes it clear it is still loading rather than showing an answer it does not have yet.

- **A day with no availability data yet is not shown as booked.** The whole grid is covered by a loading indicator until the month's availability arrives, and days grey out as unavailable only once Glade actually knows they are.
- Previously a month that had not loaded looked exactly like a month with nothing free. Receptionists reading a grey calendar told callers there were no consultation slots when there were — the calendar was simply still fetching. If your team has been turning bookings away on a full-looking calendar, this is the likely cause.
- Once the month has loaded, days that are genuinely booked or unavailable grey out as they always did.
- **Months load in well under a second in typical cases.** A month's availability is fetched in one go rather than day by day, so the wait that made the loading state noticeable in the first place is largely gone.
- If adding a session to the cart does not complete within about ten seconds, the attempt stops and reports the failure instead of leaving the button spinning indefinitely. Try again, or reload the calendar.

### User Profile Meetings

Each firm member's profile includes a **Meetings** tab that clients can visit to view upcoming appointments and book new consultation types.

- The Meetings tab shows the firm member's upcoming scheduled appointments, including any that started within the past hour.
- **Book a meeting** cards appear for consultation products that have the Meetings tab option enabled. Each card shows the appointment type name, session duration, and the firm member's name and photo.
- Clicking a Book a meeting card takes the client into the scheduling flow for that consultation type.
- Each consultation product has a toggle that controls whether it appears as a booking option on the profile's Meetings tab. Products with the toggle disabled are not shown as booking cards.

## Configuration

| Setting | Description |
|---------|-------------|
| Show in Meetings tab | Whether this consultation product appears as a Book a meeting card on a firm member's profile Meetings tab. |

## Edge Cases & Limitations

- A calendar still showing its loading indicator has no availability to report yet. Wait for it to finish before concluding a month is full — a month that loads and then shows every day greyed out is genuinely unavailable.

## Related Features

- [Scheduling](./README.md)
- [Timezones](./timezones.md)
- [Client County and Address](./client-location.md)
- [Conflicts and Concurrent Bookings](./conflicts-and-concurrent-bookings.md) — what happens when a slot fills before the client confirms
- [Video Consultations](../video-consultations.md)
