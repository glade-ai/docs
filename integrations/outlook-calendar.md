# Outlook Calendar Integration

## Overview

Glade integrates with Microsoft Outlook (via Microsoft 365) to sync a firm's calendar availability into the Glade booking system. Firm members connect their Microsoft account, and Glade pulls busy events from their selected calendars to block off unavailable time slots. When a client books an appointment through Glade, the booking is pushed back to the firm member's Outlook calendar.

## Key Behaviors

### Connecting Outlook

- Firm members connect from the Calendar settings page by clicking "Connect Outlook."
- The Microsoft OAuth flow prompts the user to grant calendar read/write and offline access.
- After authorization, Glade discovers all calendars in the account (including shared calendars) and creates entries for each one.
- Calendars start disabled — the user explicitly enables which calendars should sync.
- The primary calendar is auto-detected based on Outlook's default.

### What syncs

| Direction | Data | Details |
|-----------|------|---------|
| Outlook → Glade | Busy events | Events where `showAs` is not "free" sync into Glade as blocked time. Events marked as "free" are ignored. |
| Glade → Outlook | Bookings | When a client books an appointment, Glade creates a corresponding event on the firm member's Outlook calendar. Rescheduled bookings update the event; cancelled bookings delete it. |

- Sync is per-calendar — each calendar in the account can be independently enabled or disabled.
- Multiple calendars from one account are supported, including shared calendars.

### Sync modes

- **Delta sync** (default): Uses Microsoft's delta links to fetch only events that changed since the last sync. Fast and efficient.
- **Full sync** (initial and fallback): Fetches all events for the next 3 months. Used on first connection and when the delta link is invalidated.
- If the delta link expires, Glade automatically falls back to a full sync.

### Sync triggers

- **Manual**: The user clicks "Sync Now" from the calendar settings page. Returns a summary showing calendars synced, events created/updated/deleted, and sync mode used.
- **Automatic**: A background job syncs calendars that have not been synced in the last 24 hours.

### Availability blocking

- Synced busy events appear as blocked time on the firm's booking calendar.
- Blocked time is combined with existing Glade bookings to calculate available slots.
- If all slots in a day are blocked, the day shows as unavailable to clients.
- Each team member's calendar blocks are tracked independently.

## Configuration

| Setting | Description |
|---------|-------------|
| Outlook account connection | Connect or disconnect from Calendar settings |
| Calendar selection | Enable or disable individual calendars for sync |

## Edge Cases & Limitations

- Sync is one-way for availability — Glade reads events from Outlook but does not modify existing Outlook events. Only Glade-created booking events are written back to Outlook.
- Events marked as `showAs: "free"` in Outlook are not synced.
- All-day events are supported and block the entire day. Glade converts all-day event times to the user's timezone.
- The sync window covers the next 3 months — events further out are not synced.
- Unlike Google Calendar, Outlook does not support push notification webhooks in Glade's current implementation. Sync relies on the manual trigger and the 24-hour background job.
- If the Microsoft OAuth token is revoked or expires without refresh, the user must reconnect.
- Disconnecting an account soft-deletes all synced events from Glade but does not modify the Outlook calendar.
- Rate limiting from Microsoft Graph API is handled with retry logic and exponential backoff.

## Related Features

- [Calendar Sync](../appointments/calendar-sync.md)
- [Scheduling](../appointments/scheduling.md)
- [Google Calendar Integration](./google-calendar.md)
