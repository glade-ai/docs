# Calendar Sync

## Overview

Calendar sync connects Glade with external calendar providers — Google Calendar and Microsoft Outlook — to keep appointments synchronized and prevent double-booking. When connected, external calendar events automatically block availability in Glade's scheduling system, and Glade bookings appear on the firm's external calendar. Sync happens in real time through push notifications from each provider.

## Key Behaviors

### Supported providers

- Google Calendar (connected via Google OAuth 2.0).
- Microsoft Outlook / Exchange Online (connected via Azure OAuth 2.0).

### Two-way sync

- **Inbound (external to Glade):** Events from connected calendars are pulled into Glade. These events block scheduling availability, preventing clients from booking during times when the firm member has existing commitments.
- **Outbound (Glade to external):** When a booking is created, rescheduled, or canceled in Glade, a corresponding event is automatically created, updated, or removed in the connected external calendar.

### What syncs

| Direction | What syncs | What does not sync |
|-----------|------------|-------------------|
| External to Glade | Event start and end times (for availability blocking) | Event titles, descriptions, attendees, or other details |
| Glade to external | Booking details: time, duration, client name, meeting link | Changes made to the external event after initial sync |

### Availability blocking

- All synced external events marked as "busy" create blocks in Glade's scheduling calendar.
- Events marked as "free" or "transparent" in the external calendar do not block availability.
- When a client views available time slots, any time covered by an external "busy" event is hidden.
- This prevents double-booking across Glade and external calendars.

### Real-time sync

- Google Calendar uses Google's push notification (webhook) system. Glade is notified instantly when a Google Calendar event changes.
- Outlook uses Microsoft Graph subscriptions. Glade receives real-time notifications when Outlook events change.
- No manual sync is needed. Changes are picked up automatically.
- Google webhook subscriptions auto-renew before expiration (approximately 30 days).

### Connecting a calendar account

1. The user clicks "Connect Google Calendar" or "Connect Outlook" from the availability settings.
2. The user is redirected to the provider's consent screen to grant Glade access.
3. After authorization, Glade discovers all calendars on the account.
4. The user selects which specific calendars to sync. Individual calendars can be enabled or disabled.
5. An initial sync pulls in upcoming events from the next three months.
6. A real-time webhook subscription is established for ongoing updates.

### Managing connected calendars

- Users can view all connected accounts and their calendars.
- Individual calendars can be toggled on or off for syncing.
- One calendar can be designated as the "primary" calendar. This is where Glade creates booking events.
- Accounts can be disconnected entirely, which removes all synced events from Glade.
- If authorization expires or is revoked, the user can reconnect from the same settings page.

### Multi-calendar support

- Users can connect multiple calendar accounts (e.g., both Google and Outlook).
- Each account may contain multiple calendars (e.g., "Work", "Personal", "Team").
- Users choose which calendars to sync. Not all calendars need to be active.
- Events from all enabled calendars contribute to availability blocking.

### Per-team-member calendars

- Each team member connects and manages their own calendar accounts.
- Availability blocking applies per team member. A member's external events only affect their own availability.
- When a client books with a specific team member, only that member's calendar conflicts are checked.

## Configuration

| Setting | Description |
|---------|-------------|
| Connected accounts | Google and/or Outlook accounts linked via OAuth. |
| Enabled calendars | Which specific calendars from each account are actively synced. |
| Primary calendar | The calendar where Glade creates booking events. |
| Per-team-member setup | Each team member connects and manages their own calendars independently. |

## Edge Cases & Limitations

- Only event times are synced inbound. Glade does not see or store external event titles, descriptions, or attendee lists (for privacy).
- Events marked as "free" or "transparent" in external calendars do not block availability. This is by design but can cause confusion if users expect all events to block.
- The sync window covers the next three months. Events further in the future are not synced until they fall within that window.
- If a Google or Outlook OAuth token expires and cannot be auto-refreshed, the user must manually reconnect.
- Changes made directly to a synced event in the external calendar (after Glade created it) are not synced back to Glade.
- There is no manual "sync now" button. Sync happens automatically via webhooks.
- Disconnecting a calendar account removes all synced event data from Glade but does not delete events from the external calendar.
- All-day events are handled based on the firm's configured timezone.

## Related Features

- [Scheduling](./scheduling.md)
- [Reminders](./reminders.md)
- [Video Consultations](./video-consultations.md)
