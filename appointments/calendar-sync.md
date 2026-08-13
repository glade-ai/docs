# Calendar Sync

## Overview

Calendar sync connects Glade with external calendar providers — Google Calendar and Microsoft Outlook — to keep appointments synchronized and prevent double-booking. When connected, external calendar events automatically block availability in Glade's scheduling system, and Glade bookings appear on the firm's external calendar. Sync happens in real time through push notifications from each provider.

In addition to bookings, Glade can place court hearings (such as 341 Meetings of Creditors) detected from court notices onto the assigned team member's connected calendar. This is off by default and turned on per firm by Glade.

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
- The block is enforced when a booking is saved, not only when slots are displayed. A booking that would overlap a busy event on the assigned team member's synced calendar is refused — including when a booking is rescheduled, and when a scheduled booking is reassigned to a team member who has a conflicting event. A firm team member can still override with **Schedule Anyway**; clients cannot. Only calendars enabled for syncing are checked.

### Real-time sync

- Google Calendar uses Google's push notification (webhook) system. Glade is notified instantly when a Google Calendar event changes.
- Outlook uses Microsoft Graph subscriptions. Glade receives real-time notifications when Outlook events change.
- No manual sync is needed. Changes are picked up automatically.
- Google webhook subscriptions auto-renew before expiration (approximately 30 days).
- If Glade cannot process a change right away — for example, during a brief Google or Microsoft outage — it keeps trying until the change goes through. Previously a momentary failure dropped the update silently and the calendar stayed out of step until the next change came in.
- Changes to the same calendar are processed one at a time in the order they arrive, so a rapid burst of edits cannot overwrite one another.
- A calendar that has been deleted at the provider stops syncing instead of being retried. Disconnect and reconnect the account if you delete a synced calendar and later recreate it.

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
- When a booking is reassigned to a different team member and then rescheduled, its calendar event moves with it: Glade creates the event on the newly assigned member's connected calendar and removes it from the previous member's calendar, so the appointment always lands on the calendar of the person actually assigned. Previously the event could stay on the original member's calendar or fail to appear on the new member's.

### Court hearing sync

When enabled for a firm, court hearings that Glade detects from court notices are automatically added to the assigned team member's primary connected calendar (Google or Outlook). This is separate from booking sync — it puts hearings the firm is already tracking onto the calendars team members actually use.

- The hearing lands on the **primary calendar of the case's assigned team member** (the workflow owner). Both Google and Outlook are supported.
- The event is informational only: no guests are invited and **no invitation or notification emails are sent** to anyone, and no video link is added.
- The event title combines the hearing type, client name, and case number. The description includes details such as the case number, trustee, judge, courtroom, location, and any dial-in information for virtual hearings, along with a note that Glade added it from a court notice. The default duration is one hour, since notices carry a start time but no end time. The location is the courtroom, or "Zoom" for a virtual hearing.
- A synced hearing also **blocks bookable availability**, so clients can't book the team member during the hearing.
- For 341 Meetings, a continued or amended notice for the same case replaces the earlier calendar event rather than creating a duplicate.

This feature is off by default and is turned on per firm by Glade.

## Configuration

| Setting | Description |
|---------|-------------|
| Connected accounts | Google and/or Outlook accounts linked via OAuth. |
| Enabled calendars | Which specific calendars from each account are actively synced. |
| Primary calendar | The calendar where Glade creates booking events. |
| Per-team-member setup | Each team member connects and manages their own calendars independently. |
| Court hearing sync | Whether detected court hearings are added to assigned team members' calendars. Off by default; enabled per firm by Glade. |

## Edge Cases & Limitations

- Only event times are synced inbound. Glade does not see or store external event titles, descriptions, or attendee lists (for privacy).
- Events marked as "free" or "transparent" in external calendars do not block availability. This is by design but can cause confusion if users expect all events to block.
- The sync window covers the next three months. Events further in the future are not synced until they fall within that window.
- If a Google or Outlook OAuth token expires and cannot be auto-refreshed, the user must manually reconnect.
- Changes made directly to a synced event in the external calendar (after Glade created it) are not synced back to Glade.
- There is no manual "sync now" button. Sync happens automatically via webhooks.
- Only events that have reached Glade can block a booking. If a team member marks time as busy in Outlook and that change has not synced through, Glade does not know about it and will not stop a booking in that window.
- Disconnecting a calendar account removes all synced event data from Glade but does not delete events from the external calendar.
- All-day events are handled based on the firm's configured timezone.
- Court hearing sync only adds **future** hearings, and only when the case is linked to a team member who has a connected calendar. Unresolved cases are skipped.
- A hearing that is vacated or cancelled with no replacement time is not yet removed from the calendar. De-duplication of repeat notices currently applies only to 341 Meetings.
- Unlike inbound booking sync (which reads only event times), court hearing events Glade creates carry full hearing details.

## Related Features

- [Scheduling](./scheduling.md)
- [Reminders](./reminders.md)
- [Video Consultations](./video-consultations.md)
- [PACER](../integrations/pacer.md) — court hearing notices that feed calendar sync originate from court systems.
