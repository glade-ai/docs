# Connecting Calendars

## Overview

Each team member connects their own Google Calendar or Microsoft Outlook accounts to Glade from the availability settings, then chooses which calendars on those accounts to sync and which one Glade writes bookings to. This page covers supported providers, the connection flow, managing connected calendars, and multi-calendar setups.

## Key Behaviors

### Supported providers

- Google Calendar (connected via Google OAuth 2.0).
- Microsoft Outlook / Exchange Online (connected via Azure OAuth 2.0).

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

### Per-team-member setup

- Each team member connects and manages their own calendar accounts.
- Availability blocking applies per team member. A member's external events only affect their own availability.

## Configuration

| Setting | Description |
|---------|-------------|
| Connected accounts | Google and/or Outlook accounts linked via OAuth. |
| Enabled calendars | Which specific calendars from each account are actively synced. |
| Primary calendar | The calendar where Glade creates booking events. |
| Per-team-member setup | Each team member connects and manages their own calendars independently. |

## Edge Cases & Limitations

- If a Google or Outlook OAuth token expires and cannot be auto-refreshed, the user must manually reconnect.
- Disconnecting a calendar account removes all synced event data from Glade but does not delete events from the external calendar.
- The sync window covers the next three months. Events further in the future are not synced until they fall within that window.

## Related Features

- [Calendar Sync](./README.md)
- [How Sync Works](./sync-behavior.md)
- [Availability Blocking](./availability-blocking.md)
- [Google Calendar](../../integrations/google-calendar.md)
- [Outlook Calendar](../../integrations/outlook-calendar.md)
