# Google Calendar Integration

## Overview

Glade integrates with Google Calendar to sync a firm's calendar availability into the Glade booking system. Firm members connect their Google account, and Glade pulls busy events from their selected calendars to block off unavailable time slots. When a client books an appointment through Glade, the booking is pushed back to the firm member's Google Calendar.

## Key Behaviors

### Connecting Google Calendar

- Firm members connect from the Calendar settings page by clicking "Connect Google."
- The standard Google OAuth flow prompts the user to grant calendar access.
- After authorization, Glade discovers all calendars in the account and creates entries for each one.
- Calendars start disabled — the user explicitly enables which calendars should sync.
- The primary calendar is auto-detected based on Google's default.

### What syncs

| Direction | Data | Details |
|-----------|------|---------|
| Google → Glade | Busy events | Events marked as "busy" (opaque) sync into Glade as blocked time. Events marked as "free" (transparent) are ignored. |
| Glade → Google | Bookings | When a client books an appointment, Glade creates a corresponding event on the firm member's Google Calendar. Rescheduled bookings update the event; cancelled bookings delete it. |

- Sync is per-calendar — each calendar in the account can be independently enabled or disabled.
- Multiple calendars from one account are supported.

### Sync modes

- **Delta sync** (default): Uses Google's sync tokens to fetch only events that changed since the last sync. Fast and efficient.
- **Full sync** (initial and fallback): Fetches all events for the next 3 months. Used on first connection and when the delta sync token is invalidated.
- If the sync token expires or is invalidated by Google, Glade automatically falls back to a full sync.

### Sync triggers

- **Manual**: The user clicks "Sync Now" from the calendar settings page. Returns a summary showing calendars synced, events created/updated/deleted, and sync mode used.
- **Automatic**: A background job syncs calendars that have not been synced in the last 24 hours.
- **Push notifications**: Google Calendar sends webhook notifications when events change, triggering an immediate sync. Watch subscriptions are refreshed before their 30-day expiry.

### Availability blocking

- Synced busy events appear as blocked time on the firm's booking calendar.
- Blocked time is combined with existing Glade bookings to calculate available slots.
- If all slots in a day are blocked, the day shows as unavailable to clients.
- Each team member's calendar blocks are tracked independently — different team members have different availability.

## Configuration

| Setting | Description |
|---------|-------------|
| Google account connection | Connect or disconnect from Calendar settings |
| Calendar selection | Enable or disable individual calendars for sync |

## Edge Cases & Limitations

- Sync is one-way for availability — Glade reads events from Google Calendar but does not modify existing Google events. Only Glade-created booking events are written back to Google.
- Events marked as "free" or "transparent" in Google Calendar are not synced.
- All-day events are supported and block the entire day.
- The sync window covers the next 3 months — events further out are not synced.
- If the Google OAuth token is revoked or expires without refresh, the user must reconnect.
- Push notification watch subscriptions expire after 30 days and are auto-renewed. If renewal fails, sync falls back to the 24-hour background job.
- Disconnecting an account soft-deletes all synced events from Glade but does not modify the Google Calendar.

## Related Features

- [Calendar Sync](../appointments/calendar-sync.md)
- [Scheduling](../appointments/scheduling.md)
- [Outlook Calendar Integration](./outlook-calendar.md)
