# Outlook Calendar Integration

## Overview

Glade integrates with Microsoft Outlook to sync a firm's calendar availability into the Glade booking system. Both work or school accounts (Microsoft 365) and personal Microsoft accounts (such as `@outlook.com`) can be connected. Firm members connect their Microsoft account, and Glade pulls busy events from their selected calendars to block off unavailable time slots. When a client books an appointment through Glade, the booking is pushed back to the firm member's Outlook calendar.

## Key Behaviors

### Connecting Outlook

- Firm members connect from the Calendar settings page by clicking "Connect Outlook."
- Both work or school accounts (Microsoft 365) and personal Microsoft accounts (such as `@outlook.com`) can be connected.
- The Microsoft sign-in flow prompts the user to grant calendar read/write and offline access. The consent screen appears **every time** you connect or reconnect, so any permissions Glade has added since your last connection are always presented for approval. If you reconnect after a Glade update, expect to see the consent screen again even if you previously authorized Outlook.
- After authorization, Glade discovers all calendars in the account (including shared calendars) and creates entries for each one.
- Calendars start disabled — the user explicitly enables which calendars should sync.
- **If the connection can't be completed** (for example, Microsoft declines access to the mailbox during the initial calendar load), Glade does not leave the account in a broken "connected, no calendars" state. Instead it returns you to the app with a notice that the Outlook connection failed, and the account is not marked as connected. You can simply try connecting again, which re-runs the calendar load.
- The primary calendar is auto-detected based on Outlook's default.
- **Connecting on behalf of another team member**: A firm administrator can run the connect flow for a specific team member (for example, when setting up a calendar for an attorney during onboarding). The resulting calendar account is attached to that team member rather than to the admin, so it appears under the target person's calendar list and their availability — not the admin's. Admins can only connect on behalf of someone who is already a team member of the firm.

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
- If the delta link expires or becomes stale (for example, after a long sync gap or a mailbox migration), Microsoft Graph signals this condition and Glade automatically resets the link and performs a full sync to recover. This recovery happens within the current sync run — there is no need to wait for the next scheduled sync cycle.

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
- Personal Microsoft accounts (such as `@outlook.com`) can connect and sync their own calendars, but cannot sync **shared** calendars. Shared-calendar sync is available only on work or school (Microsoft 365) accounts.
- All-day events are supported and block the entire day. Glade converts all-day event times to the user's timezone.
- The sync window covers the next 3 months — events further out are not synced.
- Unlike Google Calendar, Outlook does not support push notification webhooks in Glade's current implementation. Sync relies on the manual trigger and the 24-hour background job. Stale or expired delta links are recovered automatically during the next sync run (manual or scheduled).
- If the Microsoft OAuth token is permanently revoked — for example, because you changed your Microsoft password, revoked the app permission in your Microsoft account settings, or the refresh token has permanently expired — Glade automatically disconnects the calendar account and notifies your firm so your team knows to reconnect. Sync stops immediately rather than continuing to fail silently. Reconnect from Calendar settings to restore availability blocking and booking sync.
- Disconnecting an account soft-deletes all synced events from Glade but does not modify the Outlook calendar.
- Rate limiting from Microsoft Graph API is handled with retry logic and exponential backoff.

## Related Features

- [Calendar Sync](../appointments/calendar-sync.md)
- [Scheduling](../appointments/scheduling.md)
- [Google Calendar Integration](./google-calendar.md)
