# Appointment Outcomes

## Overview

Your firm can keep its own list of appointment outcomes — **No show**, **Claimed**, or whatever labels match how your team works — and attach one to a booking after the fact. This is how the calendar and daily reports come to record what actually happened, rather than only whether the appointment was scheduled.

## Key Behaviors

- **Your firm defines the list.** Nothing is provided as a starting point, so every firm begins with an empty list and no outcome on any booking until someone creates them. Outcomes can be reordered so the ones your team uses most sit at the top.
- **An outcome is separate from the booking's status.** Attaching one does not move the booking through its lifecycle — a completed appointment marked **No show** is still recorded as completed. The statuses in [Booking Lifecycle](./booking-lifecycle.md) are unchanged.
- **It is also separate from workflow custom statuses.** The two lists are kept apart deliberately: an appointment outcome carries none of the case-tracking behavior a workflow status does, and choosing one triggers nothing.
- Only firm team members can set or clear a booking's outcome. Clients cannot.
- An outcome has to belong to your firm and be currently in use — an archived or deleted outcome cannot be attached to a booking.
- **Retiring an outcome does not rewrite history.** Archiving one keeps it on the bookings that already carry it while removing it from the list of choices, so past appointments stay readable.
- The outcome appears on the booking and as an **Outcome** column in the bookings report and its spreadsheet export.

> TODO: Confirm where the outcome list is managed in firm settings and where the outcome is chosen on an individual booking.

## Configuration

| Setting | Description |
|---------|-------------|
| Appointment outcomes | The firm's own list of labels recording what happened at an appointment (for example No show). Firm-defined and empty until you create them; can be reordered and archived. |

## Edge Cases & Limitations

- A booking carries at most one outcome. Recording two things about the same appointment means choosing which one the label should capture, or noting the rest on the case.
- Appointment outcomes are per firm. They are not shared between firms and nothing is set up in advance, so a new firm sees no outcome option on its bookings until the list is created.

## Related Features

- [Scheduling](./README.md)
- [Booking Lifecycle](./booking-lifecycle.md)
- [Reporting](../../back-office/reporting/README.md) — the bookings report's Outcome column
