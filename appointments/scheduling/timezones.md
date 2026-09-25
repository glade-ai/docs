# Timezones

## Overview

Firms define availability in their own local timezone, while clients see every appointment time in their own timezone. Firm-side views stay in the firm's timezone.

## Key Behaviors

- Firms define availability in their local timezone.
- Clients booking an appointment see every time in **their own** timezone, not the firm's. This applies to the slot list, the review screen before confirming, the booking confirmation, the cart, the Meetings tab on a firm member's profile, and the next-consultation widget on the client's home page.
- Every client-facing reference to an appointment shows the time in the recipient's own timezone — the booking confirmation, email and text reminders, client-portal messages, and the calendar invite. A client in Eastern time who books a "2:30 PM" slot with a firm that operates in Pacific time sees 2:30 PM Eastern everywhere, and the calendar invite lands at the correct local time. Previously these could show the firm's time instead, so an appointment could appear at the wrong hour on the client's calendar and invites.
- A timezone picker sits above the slot list so a client can view times in a different timezone — useful when they are travelling or booking on behalf of someone else. Changing it re-sorts the slots into that timezone's days, and the choice is saved to the client's profile so later bookings open in the same timezone.
- The picker starts on the client's saved profile timezone if they have one, otherwise the timezone their device reports.
- Whichever timezone is on screen, the client books the exact moment they clicked. A client in Eastern time booking a "2:30 PM" slot from a Pacific-time firm gets 2:30 PM Eastern, and the firm sees the matching time on their own calendar.
- Firm-side views — the Bookings section, the firm dashboard, and internal staff notifications — continue to show times in the firm's timezone.
- The system validates timezone inputs and defaults to US/Eastern if a timezone cannot be determined.

## Edge Cases & Limitations

- Timezone mismatches can occur if the firm's timezone setting is incorrect.

## Related Features

- [Scheduling](./README.md)
- [Availability](./availability.md)
- [Client Booking Flow](./client-booking-flow.md)
- [Reminders](../reminders.md)
