# Scheduling

## Overview

Scheduling in Glade allows firms to offer bookable appointments to clients. Firms define their availability, configure appointment types with durations and pricing, and clients select from open time slots to book. Appointments can be created through direct booking, product purchases, subscriptions, or as part of automated workflows.

## Key Behaviors

### Appointment types

- Appointments are configured as products. Each product has a type: Online Session (video call), In-Person Session, Consultation, or Chat Session.
- Each product can be free or paid, with one or more pricing tiers.
- Products define session duration, scheduling interval (the gap between available time slots), and buffer time (preparation time before and after appointments).
- Products can enable or disable automatic video conference link generation.
- Products can set a concurrent booking limit, which controls how many overlapping bookings are allowed in the same time slot. The default is 1.
- A custom confirmation message can be configured per product and is shown to clients after booking.

### Defining availability

- Firms set up recurring availability patterns by specifying days of the week and start/end times.
- Availability is defined in the firm's local timezone.
- The system generates concrete bookable time slots from these patterns.
- Individual team members can have their own separate availability schedules.
- External calendar events from connected calendars (Google Calendar or Outlook) automatically block availability to prevent double-booking.
- Only events marked as "busy" block availability. Events marked as "free" or "transparent" do not.

### Client booking flow

1. The client views the firm's product or service listing.
2. The client selects a product and initiates scheduling.
3. A calendar displays available dates and time slots.
4. Times are shown in the client's local timezone, converted from the firm's timezone.
5. The client selects a date and time.
6. The booking is confirmed and created.
7. If the product has video conferencing enabled, a meeting link is generated automatically.
8. The client receives a confirmation with booking details.

### Booking lifecycle

Each booking moves through a series of statuses over its lifetime:

| Status | Meaning |
|--------|---------|
| Unscheduled | Booking created but no time selected yet. Has an expiration date. |
| Scheduled | Time is set and the appointment is upcoming. |
| In Progress | Appointment is currently happening (between start and end time). |
| Completed | Appointment end time has passed. |
| Canceled | Firm or client canceled the appointment. |
| Skipped | Appointment was missed but not formally canceled. |

### Team member assignment

- Bookings can be assigned to specific team members within the firm.
- A default team member can be set per product, so new bookings are pre-assigned.
- Team members can be reassigned after booking.
- When connected to a workflow, team assignment follows workflow rules.
- Each team member's individual availability is checked when assigning.
- When a workflow has an assigned attorney, the scheduling modal automatically opens to that attorney's availability. This applies in the client portal (Home Page booking tasks) and on the firm-side Bookings tab. If the assigned attorney has no availability, a message indicates this and you can select another team member from the available chips. Selecting a different team member chip always shows their calendar, even if they have no availability.

### Rescheduling

- Both clients and firm staff can reschedule appointments.
- Rescheduling checks availability to prevent conflicts with existing bookings.
- When rescheduling, available time slots are filtered to the team member originally assigned to the booking. This ensures the rescheduled appointment stays with the same team member.
- By default, clients cannot reschedule within 48 hours of the appointment start time. This protects firms from last-minute schedule changes.
- Firms can override this restriction and allow client rescheduling within 48 hours on a per-product basis.
- Firm staff can always reschedule regardless of the 48-hour window.
- When an appointment is rescheduled, all associated reminders and calendar events are updated automatically.

### Cancellation

- Both clients and firm staff can cancel appointments.
- Cancellation records when it happened but does not delete the booking. The record is preserved for history.
- Associated reminders are removed when a booking is canceled.
- Calendar events on connected external calendars are updated to reflect the cancellation.

### Timezone handling

- Firms define availability in their local timezone.
- Clients see available times converted to their own timezone.
- All bookings are stored in the firm's timezone internally.
- The system validates timezone inputs and defaults to US/Eastern if not specified.

### Workflow integration

- Appointments can be created automatically as steps within a workflow.
- Workflow-generated bookings can be assigned to specific team members based on workflow rules.
- Access permissions are automatically granted to workflow participants.
- Booking events (created, rescheduled, canceled) can trigger subsequent workflow steps.

### Permissions and access

- Firm users always have full access to manage bookings.
- Clients can view and manage their own bookings.
- Additional collaborators can be granted access to specific bookings.
- Workflow participants automatically receive appropriate access.

## Configuration

| Setting | Description |
|---------|-------------|
| Product type | Online Session, In-Person Session, Consultation, or Chat Session. |
| Session duration | Length of each appointment. |
| Scheduling interval | Minimum gap between available time slots. |
| Buffer time | Preparation time added before and after appointments. |
| Concurrent bookings | Maximum number of overlapping bookings allowed per time slot. Default is 1. |
| Video conference link | Whether to auto-generate a video meeting link for the appointment. |
| 48-hour reschedule rule | Whether clients can reschedule within 48 hours of the appointment. |
| Default team member | Pre-assigned team member for new bookings on this product. |
| Custom confirmation message | Message shown to the client after booking is confirmed. |
| Availability patterns | Days of the week and start/end times, configured per team member. |

## Edge Cases & Limitations

- Unscheduled bookings expire if no time is selected before the expiration date.
- The 48-hour rescheduling restriction applies to clients only. Firm staff can always reschedule.
- Concurrent booking limits are per time slot, not per day.
- If no team member availability is configured for a product, the product may show no available time slots.
- External calendar events marked as "free" do not block availability. Only "busy" events create blocks.
- Timezone mismatches can occur if the firm's timezone setting is incorrect.
- Booking a time slot does not guarantee a specific team member unless one is pre-assigned to the product.

## Related Features

- [Calendar Sync](./calendar-sync.md)
- [Reminders](./reminders.md)
- [Video Consultations](./video-consultations.md)
