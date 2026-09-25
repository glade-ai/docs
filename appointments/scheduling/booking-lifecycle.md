# Booking Lifecycle

## Overview

Each booking moves through a series of statuses over its lifetime, from unscheduled through completed or canceled. Clients and firm staff can reschedule and cancel bookings; only the firm can unschedule or delete one. This doc covers the statuses and each of those actions.

## Key Behaviors

### Booking statuses

Each booking moves through a series of statuses over its lifetime:

| Status | Meaning |
|--------|---------|
| Unscheduled | Booking created but no time selected yet. Has an expiration date. |
| Scheduled | Time is set and the appointment is upcoming. |
| In Progress | Appointment is currently happening (between start and end time). |
| Completed | Appointment end time has passed. |
| Canceled | Firm or client canceled the appointment. |
| Skipped | Appointment was missed but not formally canceled. |

### Rescheduling

- Both clients and firm staff can reschedule appointments.
- Rescheduling checks availability to prevent conflicts with existing bookings.
- When rescheduling, available time slots are filtered to the team member originally assigned to the booking. This ensures the rescheduled appointment stays with the same team member.
- By default, clients cannot reschedule within 48 hours of the appointment start time. This protects firms from last-minute schedule changes.
- Firms can override this restriction and allow client rescheduling within 48 hours on a per-product basis.
- Firm staff can always reschedule regardless of the 48-hour window.
- When a firm blocks calendar time to pause new bookings, firm staff can still move an existing appointment into that blocked time by confirming **Schedule Anyway** when they select the blocked slot. Clients cannot reschedule into blocked time this way. See [Conflicts and Concurrent Bookings](./conflicts-and-concurrent-bookings.md).
- Team members can also reschedule bookings that are in canceled or completed status by assigning a new time, returning them to scheduled status and recreating associated calendar events, reminders, and email notifications.
- Clients and their workflow collaborators (for example, a spouse on a joint case) can reschedule a booking from its attachment card in the workflow Discussion view even after the appointment time has passed. Past bookings on the path render with a completion check and a "Completed on …" subtitle, but the card stays clickable so the client can pick a new time.
- A **canceled** booking on a workflow step stays actionable: its attachment card reads **"Canceled, select a new time"** and the **View** button opens the scheduler so the client or attorney can choose a new slot. Picking a time revives the same booking — it returns to scheduled status rather than requiring a brand-new booking. (If the canceled booking still has its original time, the scheduler opens on a review screen showing that time; tap **Reschedule** to reach slot selection.) Cards for **skipped** bookings remain disabled.
- When an appointment is rescheduled, all associated reminders and calendar events are updated automatically.

### Unscheduling

- Team members can unschedule a booking — removing the scheduled time and returning it to an unscheduled state so the client can select a new appointment time.
- Unscheduling clears the meeting link and removes the associated event from any connected external calendar.
- Scheduled reminders are deleted when a booking is unscheduled.
- The client receives an email notification referencing the original appointment date.
- A system message is posted in the client's Glade conversation when a booking is unscheduled.
- Only team members can unschedule a booking; clients do not have this option.

### Cancellation

- Both clients and firm staff can cancel appointments.
- Cancellation records when it happened but does not delete the booking. The record is preserved for history.
- Associated reminders are removed when a booking is canceled.
- Calendar events on connected external calendars are updated to reflect the cancellation.

### Deleting a booking

Cancelling keeps the appointment on the books — the row stays in every list marked **Canceled** and the client is emailed. **Delete** is for a booking that should never have existed at all: a test row, a duplicate, or one taken against the wrong client. It is offered on the booking's detail panel.

- **A deleted booking leaves every view at once** — the bookings list, the calendar, the team views, and the reports. It is not shown as canceled; it is simply gone.
- **The client is not told.** No cancellation email goes out, because the firm is retracting its own record rather than calling off an appointment the client is expecting. Cancel instead if the client needs to know the appointment is off.
- **The team member's calendar is cleaned up.** The event Glade created on a connected external calendar is released, so deleting never leaves an orphaned block on someone's calendar.
- **Pending reminders, completion, and follow-up messages are cancelled**, so nothing is sent about a booking that no longer exists.
- **It is recorded.** Glade keeps an audit entry naming who deleted the booking and when, even though the booking itself no longer appears.
- **Only the firm can delete.** A client can cancel their own booking but cannot delete it — erasing the firm's record of an appointment is not something the client can do.

> TODO: Confirm whether a deleted booking can be restored, and by whom.

## Configuration

| Setting | Description |
|---------|-------------|
| 48-hour reschedule rule | Whether clients can reschedule within 48 hours of the appointment. |

## Edge Cases & Limitations

- Unscheduled bookings expire if no time is selected before the expiration date.
- The 48-hour rescheduling restriction applies to clients only. Firm staff can always reschedule.

## Related Features

- [Scheduling](./README.md)
- [Appointment Outcomes](./appointment-outcomes.md) — recording what happened, separately from status
- [Conflicts and Concurrent Bookings](./conflicts-and-concurrent-bookings.md)
- [Workflow Bookings](./workflow-bookings.md)
- [Reminders](../reminders.md)
- [Calendar Sync](../calendar-sync/README.md)
