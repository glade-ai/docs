# Booking a Client from a Case

## Overview

Firm staff can book a case's client into any of the firm's consultation services directly from the case, using the **Book client** action on the case summary. This is for appointments that happen between workflow steps. For example, a paralegal can book "doc prep" appointments to chase missing documents before filing. The appointment is attached to the case you are looking at, but it is not part of any workflow step.

> TODO: The case summary's **Book client** action ships in a separate app release. Confirm the exact labels once it is live.

## Key Behaviors

- **Book at any point in the case, as many times as needed.** Each booking made this way is a new appointment. It never reschedules an existing booking of the same service. The global booking wizard does reschedule: it moves the client's existing booking of that service instead of adding one.
- **The booking stays on this case.** It is attached to the case it was made from. It never starts a new case and never moves to another of the client's cases.
- **It doesn't affect workflow steps.** The booking belongs to no step, so holding it or skipping it never completes a step or moves the case forward. A step's own booking still works as usual.
- **Firm-wide booking automations still run.** Automations your firm has set up for every new booking still fire.
- **Choose a service, time and team member.** Any consultation or session service your firm schedules can be booked. You can assign the appointment to a team member at your firm. If you are allowed to book over conflicts, you can book a time that conflicts with existing appointments (see [Conflicts and Concurrent Bookings](./conflicts-and-concurrent-bookings.md)).
- **Add an internal note.** The note is saved to the case's notes and linked to the booking. It appears a moment after the booking is created.
- **Tell several bookings apart.** The case summary's Bookings group lists each booking on the case with its service name and status, next to any booking the workflow created.

## Configuration

| Setting | Effect |
|---------|--------|
| Consultation and session services | Every consultation or session service your firm schedules is offered, including paid ones. A service is offered only if it has an active price with a session length. |
| Team member | Optional. The team member must belong to your firm. |
| Internal note | Optional. Saved to the case's notes. |

## Edge Cases & Limitations

- **Paid consultations are not charged.** A paid consultation booked from a case charges the client nothing, the same as a booking created by a workflow step.
- **Address and county are not asked for.** The wizard skips the client details step, so it doesn't ask for the client's address or county, even for a service that normally requires them. See [Client County and Address](./client-location.md).
- **If the note can't be saved, the booking stays.** When saving the internal note to the case fails, the booking is still created, and the note text stays on the appointment's calendar card.
- Only members of the firm that owns the case can book from it.
- A service whose price is inactive or archived, or that has no session length, can't be booked this way.

## Related Features

- [Scheduling](./README.md)
- [Workflow Bookings and Access](./workflow-bookings.md)
- [Team Member Assignment](./team-assignment.md)
- [Booking Lifecycle](./booking-lifecycle.md)
- [Client Booking Flow](./client-booking-flow.md)
