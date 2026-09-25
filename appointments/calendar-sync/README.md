# Calendar Sync

## Overview

Calendar sync connects Glade with external calendar providers — Google Calendar and Microsoft Outlook — to keep appointments synchronized and prevent double-booking. When connected, external calendar events automatically block availability in Glade's scheduling system, and Glade bookings appear on the firm's external calendar. Sync happens in real time through push notifications from each provider.

In addition to bookings, Glade can place court hearings (such as 341 Meetings of Creditors) detected from court notices onto the assigned team member's connected calendar. This is off by default and turned on per firm by Glade.

## Topics

- [Connecting Calendars](./connecting-calendars.md) — supported providers, connecting an account, choosing calendars and a primary calendar, and per-team-member setup.
- [How Sync Works](./sync-behavior.md) — what syncs in each direction, real-time notifications and the hourly catch-up job, and how booking events follow reassignment.
- [Availability Blocking](./availability-blocking.md) — which events block time, concurrent bookings, enforcement at save time, all-day events, and who can read a synced event's title.
- [Court Hearing Sync](./court-hearing-sync.md) — placing hearings detected from court notices on the assigned team member's calendar, including notices with more than one hearing.

## Configuration

| Setting | Description |
|---------|-------------|
| Connected accounts | Google and/or Outlook accounts linked via OAuth. |
| Enabled calendars | Which specific calendars from each account are actively synced. |
| Primary calendar | The calendar where Glade creates booking events. |
| Per-team-member setup | Each team member connects and manages their own calendars independently. |
| Court hearing sync | Whether detected court hearings are added to assigned team members' calendars. Off by default; enabled per firm by Glade. |

## Related Features

- [Scheduling](../scheduling/README.md)
- [Reminders](../reminders.md)
- [Video Consultations](../video-consultations.md)
- [PACER](../../integrations/pacer/README.md) — court hearing notices that feed calendar sync originate from court systems.
