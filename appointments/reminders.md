# Reminders

## Overview

Glade automatically sends appointment reminders to both clients and firm members before scheduled bookings. Clients receive reminders 30 minutes before their appointment via email and SMS, while firm members receive a daily digest email the day before at 5:00 PM in their local timezone. Reminders are created automatically when a booking is scheduled and update automatically when bookings are rescheduled or canceled.

## Key Behaviors

### Reminder types and timing

| Recipient | Channel | Timing | Content |
|-----------|---------|--------|---------|
| Client | Email | 30 minutes before appointment | Booking date/time, firm name and branding, product/session name, link to client portal |
| Client | SMS | 30 minutes before appointment | Firm name, "30 minutes" notice, link to client portal |
| Firm member | Email | 5:00 PM the day before | List of all bookings for the next day, customer names, booking times, product details |

### Automatic reminder creation

- Reminders are created automatically when a booking is scheduled. No manual setup is required.
- The system calculates the exact send time based on the booking start time.
- Client reminders are set to the booking start time minus 30 minutes.
- Firm member reminders are set to 5:00 PM the day before, in the firm's local timezone.

### Reminder updates on reschedule

- When a booking is rescheduled, all associated reminders automatically update to reflect the new time.
- Client reminders recalculate to 30 minutes before the new start time.
- Firm member reminders recalculate to the day before the new date.
- If the booking is rescheduled to a different time on the same day, the firm member reminder timing stays unchanged since the day-before trigger date has not changed.

### Reminder cancellation

- When a booking is canceled, all associated reminders are automatically removed.
- No cancellation-specific notification is sent through the reminder system.

### Email reminders

- Branded with the firm's name, logo, and primary color.
- Include the appointment date and time formatted in the firm's timezone.
- Include the product or session name.
- Include a link for the client to access their portal.

### SMS reminders

- Sent only if the client has opted in to receive text messages.
- Require a valid phone number on the client's profile.
- Require the firm to have a Glade-assigned phone number for sending.
- Message includes the firm name, a "30 minutes" notice, and a link to the client portal.

### Firm member daily digest

- Firm members receive a single email listing all bookings for the following day.
- Sent at 5:00 PM in the firm's local timezone.
- Multiple bookings are batched into one email rather than sent individually.
- Each entry includes the customer name, booking time, and product details.

### Task follow-up integration

- When a client has pending tasks and an upcoming booking, the reminder system adjusts task follow-up cadence.
- This prevents over-messaging clients who already have an upcoming appointment.
- Normal task follow-up resumes after the booking completes.

## Configuration

| Setting | Description |
|---------|-------------|
| SMS opt-in | Clients must opt in to receive text message reminders. |
| Client phone number | Required for SMS delivery. If missing, only email reminders are sent. |
| Firm phone number | Firm must have a Glade-assigned phone number to send SMS reminders. |
| Firm timezone | Determines when firm member reminders are sent (5:00 PM local time). |

Reminder timing (30 minutes for clients, day-before at 5:00 PM for firms) is not configurable per firm or per product. All bookings follow the same schedule.

## Edge Cases & Limitations

- Reminder timing is fixed. Firms cannot customize when reminders are sent (for example, changing 30 minutes to 1 hour).
- SMS reminders require both client opt-in and a valid phone number. If either is missing, only email is sent.
- The firm must have a Glade-assigned phone number to send any SMS. Without one, SMS reminders are not delivered.
- Firm member reminders are email-only. There is no SMS option for firm members.
- There is no read receipt or delivery confirmation. The system does not track whether a recipient opened or read the reminder.
- Clients cannot reschedule or cancel directly from a reminder email or text. They must log into the platform.
- If the firm's timezone is set incorrectly, firm member reminders may arrive at the wrong time.
- There is no push notification channel. Reminders are limited to email and SMS.
- If a booking is created less than 30 minutes before the start time, the client reminder may not have time to send.

## Related Features

- [Scheduling](./scheduling.md)
- [Calendar Sync](./calendar-sync.md)
- [Video Consultations](./video-consultations.md)
