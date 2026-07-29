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
- In addition to recurring availability, you can add **availability blocks** for specific date ranges. Each block has a type that determines its effect on bookable time:
  - **Blocked** — removes the covered times from bookable availability. Clients cannot schedule into these windows. Use this for vacations, court dates, off-site days, or any other time you should not be booked.
  - Other block types (for example, blocks used purely for visual annotation on the calendar) do not remove availability — only blocks marked as Blocked actually prevent new bookings.
- Blocked times are **hard blocks**. They always remove the covered slots from the booking calendar regardless of the product's concurrent booking limit — even a product that allows multiple overlapping bookings cannot be booked inside a blocked window.
- A Blocked entry that is not assigned to a specific team member applies to **every team member**. Use this when you need to take the firm off the calendar for everyone at once (for example, an office closure) without creating one entry per team member.
- Bookings cannot be created or rescheduled into a blocked window. Attempting to do so from a stale link or an out-of-date slot list is rejected with an error rather than silently saved.

### Availability management view

The **Availability** tab in the Bookings section gives you a centralized place to review and manage availability across all services and team members.

The tab has two sub-views:

- **Team Members**: Shows availability settings organized by team member.
- **Services**: Lists all schedulable services. For each service, a summary shows which team members have availability configured. Clicking a service name opens the availability editor for that service inline. A **View in services** link navigates to the full service settings page.

Clicking a service in either view opens the availability editor directly — you can update availability without leaving the Bookings section.

### Client booking flow

1. The client views the firm's product or service listing. For free sessions, the booking button reads **Book a call**; for paid sessions it shows the session price.
2. The client selects a product and initiates scheduling.
3. A calendar displays available dates and time slots.
4. Times are shown in the client's own timezone, with a timezone picker above the slot list if they want to view them in a different one.
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
- A booking created without a specific team member is treated as belonging to the calendar owner and is shown under the owner's name. When you filter the bookings list (or the **Your appointments** widget) by the calendar owner, these unassigned bookings appear alongside the ones explicitly assigned to the owner. Filtering by any other team member shows only the bookings explicitly assigned to that person.
- When connected to a workflow, team assignment follows workflow rules.
- Each team member's individual availability is checked when assigning.
- When a workflow has an assigned attorney, the scheduling modal automatically opens to that attorney's availability. This applies in the client portal (Home Page booking tasks) and on the firm-side Bookings tab. If the assigned attorney has no availability, a message indicates this and you can select another team member from the available chips. Selecting a different team member chip always shows their calendar, even if they have no availability.

### Which team member the Bookings section is showing

The Bookings section has List, Calendar, and Team views, and the team member you are looking at carries across them. Whoever you have selected stays selected as you move between views, so you no longer have to re-pick them each time.

- Opening a booking in List view and switching to Calendar shows **that booking's team member's** calendar. Previously the calendar reset to the appointment type's default assignee, so opening one team member's booking could land you on someone else's calendar.
- **Block this Time** applies to the team member currently selected, rather than always to the appointment type's default assignee. Check who is selected before blocking time.
- The Team view's team member filter lists every member of the firm, including people with no appointments booked. Previously anyone without a booking dropped out of the filter entirely, so they could not be selected.
- Once you have picked a team member by hand, that choice stays put — a change to the appointment type's default assignee, or bookings reloading in the background, does not switch the view away from the person you chose.

### Rescheduling

- Both clients and firm staff can reschedule appointments.
- Rescheduling checks availability to prevent conflicts with existing bookings.
- When rescheduling, available time slots are filtered to the team member originally assigned to the booking. This ensures the rescheduled appointment stays with the same team member.
- By default, clients cannot reschedule within 48 hours of the appointment start time. This protects firms from last-minute schedule changes.
- Firms can override this restriction and allow client rescheduling within 48 hours on a per-product basis.
- Firm staff can always reschedule regardless of the 48-hour window.
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

### Timezone handling

- Firms define availability in their local timezone.
- Clients booking an appointment see every time in **their own** timezone, not the firm's. This applies to the slot list, the review screen before confirming, the booking confirmation, the cart, the Meetings tab on a firm member's profile, and the next-consultation widget on the client's home page.
- A timezone picker sits above the slot list so a client can view times in a different timezone — useful when they are travelling or booking on behalf of someone else. Changing it re-sorts the slots into that timezone's days, and the choice is saved to the client's profile so later bookings open in the same timezone.
- The picker starts on the client's saved profile timezone if they have one, otherwise the timezone their device reports.
- Whichever timezone is on screen, the client books the exact moment they clicked. A client in Eastern time booking a "2:30 PM" slot from a Pacific-time firm gets 2:30 PM Eastern, and the firm sees the matching time on their own calendar.
- Firm-side views — the Bookings section and the firm dashboard — continue to show times in the firm's timezone.
- The system validates timezone inputs and defaults to US/Eastern if not specified.

### Booking into a conflicting time

- When a selected slot conflicts with an existing booking, the scheduler flags the conflict and offers **Schedule Anyway** so a team member can double-book deliberately.
- **Schedule Anyway** works both when creating a booking and when rescheduling one. Previously it was only honored on the reschedule path — on a new booking the click appeared to do nothing and the appointment was never created. If your team hit that and worked around it by booking a non-conflicting time and then rescheduling into the conflict, that workaround is no longer necessary.
- **Schedule Anyway** does not override a Blocked availability entry. Blocked windows remain hard blocks and cannot be booked into.

### User Profile Meetings

Each firm member's profile includes a **Meetings** tab that clients can visit to view upcoming appointments and book new consultation types.

- The Meetings tab shows the firm member's upcoming scheduled appointments, including any that started within the past hour.
- **Book a meeting** cards appear for consultation products that have the Meetings tab option enabled. Each card shows the appointment type name, session duration, and the firm member's name and photo.
- Clicking a Book a meeting card takes the client into the scheduling flow for that consultation type.
- Each consultation product has a toggle that controls whether it appears as a booking option on the profile's Meetings tab. Products with the toggle disabled are not shown as booking cards.

### Workflow integration

- Appointments can be created automatically as steps within a workflow.
- Workflow-generated bookings can be assigned to specific team members based on workflow rules.
- Access permissions are automatically granted to workflow participants.
- Booking events (created, rescheduled, canceled) can trigger subsequent workflow steps.
- When a workflow creates a booking task for a client, the task title includes the appointment type name — for example, "Schedule Appointment: Initial Consultation". This helps clients identify which service they are being asked to schedule when multiple appointment types exist.

### Permissions and access

- Firm users always have full access to manage bookings.
- Clients can view and manage their own bookings.
- Additional collaborators can be granted access to specific bookings.
- Workflow participants automatically receive appropriate access.
- **Workflow bookings require explicit assignment**: When a booking is created as a step in a workflow, only people who are explicitly assigned to that booking (or who are members of the firm) can view, reschedule, or cancel it. A client being the subject of the booking is not enough on its own — for example, a signing or notarization booking that is only assigned to firm staff is hidden from the client's upcoming bookings list and the client cannot reschedule it. Add the client as an assignee on the booking if they should be able to manage it themselves.

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
| Show in Meetings tab | Whether this consultation product appears as a Book a meeting card on a firm member's profile Meetings tab. |

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

