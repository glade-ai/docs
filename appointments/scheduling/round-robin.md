# Round-Robin Consultation Booking

## Overview

Round robin lets a firm share a consultation service across several team members. Clients don't pick a staff member. They see one calendar of times when anyone on the service is free, and each booking goes to the team member who has gone longest without one. Firms that spread new consultations evenly across attorneys or intake staff use it.

## Key Behaviors

### What clients see

- **One shared calendar.** A time is offered when at least one team member can take it. That person must have hours set for that service at that time, must not be busy in Glade or on their connected calendar, must be under the service's booking limit, and must have a working calendar connection.
- **No staff picker.** On a round-robin service, the public booking page and the client portal don't show a list of team members. The portal also no longer shows the "The attorney assigned to this case has no availability" message on these services.
- **A booking that has no team member yet shows every open time.** One example is a booking link the firm sent. When the client picks a time, Glade assigns the booking to whoever is next.
- **A booking that already has a team member shows only that person's times.** This applies when a client reschedules from the portal.

### Who gets each booking

- The team member who has gone longest without a booking gets the next one, among those free at the chosen time.
- **Paid consultations:** before the client is charged, Glade checks that someone is free at that time.
- **Booking links:** the team member is assigned when the client picks a time, not when the link is sent.
- **Staff rescheduling:** a reschedule keeps the current team member if they are free at the new time. If they are not, Glade picks again.
- **A booking staff made for a named team member stays with that person.**
- Each assignment is recorded along with the reason each other team member was passed over, so support can explain why a booking went to a particular person.

### Staff

- Staff booking from the dashboard still choose the team member, as on any other service.

## Configuration

| Setting | Description |
|---------|-------------|
| Round robin | A per-service switch. Only consultation services can turn it on. Off by default. |

Before turning round robin on, set weekly hours on the service for each team member who should take bookings, and have each of them connect their calendar.

> TODO: Confirm where the round-robin switch appears in the firm app and what it is labelled. Round robin is not yet available to every firm.

## Edge Cases & Limitations

- A team member whose calendar connection needs reconnecting is left out of the rotation until they reconnect.
- When a client reschedules from the portal, a round-robin booking stays with its current team member, even if someone else is free at the new time. The portal offers only that person's times.
- Clients can't choose a specific person on a round-robin service.
- Priority tiers and daily caps per team member are not supported.

## Related Features

- [Scheduling](./README.md)
- [Team Member Assignment](./team-assignment.md)
- [Availability](./availability.md)
- [Conflicts and Concurrent Bookings](./conflicts-and-concurrent-bookings.md)
- [Client Booking Flow](./client-booking-flow.md)
- [Calendar Sync](../calendar-sync/README.md)
