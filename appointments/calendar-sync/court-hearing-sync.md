# Court Hearing Sync

## Overview

When enabled for a firm, court hearings that Glade detects from court notices (such as 341 Meetings of Creditors) are automatically added to the assigned team member's primary connected calendar (Google or Outlook). This is separate from booking sync — it puts hearings the firm is already tracking onto the calendars team members actually use. This feature is off by default and is turned on per firm by Glade.

## Key Behaviors

### Hearing events

- The hearing lands on the **primary calendar of the case's assigned team member** (the workflow owner). Both Google and Outlook are supported.
- The event is informational only: no guests are invited and **no invitation or notification emails are sent** to anyone, and no video link is added.
- The event title combines the hearing type, client name, and case number. The description includes details such as the case number, trustee, judge, courtroom, location, and any dial-in information for virtual hearings, along with a note that Glade added it from a court notice. The default duration is one hour, since notices carry a start time but no end time. The location is the courtroom, or "Zoom" for a virtual hearing.
- A synced hearing also **blocks bookable availability**, so clients can't book the team member during the hearing.
- For 341 Meetings, a continued or amended notice for the same case replaces the earlier calendar event rather than creating a duplicate.
- Court hearings Glade places on a team member's calendar are synced events like any other, so the hearing's title reads as **Busy** to everyone except that team member. See [Who can read a synced event's title](./availability-blocking.md#who-can-read-a-synced-events-title).

### Notices that schedule more than one hearing

A single court notice often sets more than one hearing — a confirmation hearing and a 341 meeting of creditors in the same entry is a common pattern in some districts. Glade reads **every** hearing date on the notice and creates a separate calendar entry for each one, matching each date to the hearing type named next to it.

- Previously only one hearing per notice was recorded, and it could be labeled with the wrong hearing type — a notice setting a confirmation hearing for one date and a 341 meeting for another could produce a single entry carrying one date with the other's label. A team relying on the calendar would have missed the second hearing entirely.
- When a notice is processed again — for example after a rescheduling notice arrives — Glade reconciles what it already has: it adds hearings that are missing and removes entries that no longer match the notice, so a previously mislabeled entry is corrected rather than left alongside the right one.
- Each hearing on the notice produces its own calendar event on the assigned team member's calendar, and each blocks availability for its own time.

Hearings recorded before this correction are not revisited automatically. If your firm works in a district that issues combined notices, ask Glade to reprocess your court notices for the affected period so the missing and mislabeled hearings are corrected.

## Configuration

| Setting | Description |
|---------|-------------|
| Court hearing sync | Whether detected court hearings are added to assigned team members' calendars. Off by default; enabled per firm by Glade. |

## Edge Cases & Limitations

- Court hearing sync only adds **future** hearings, and only when the case is linked to a team member who has a connected calendar. Unresolved cases are skipped.
- A hearing that is vacated or cancelled with no replacement time is not yet removed from the calendar. De-duplication of repeat notices currently applies only to 341 Meetings.
- Reading multiple hearings from one notice depends on each date being named alongside a recognizable hearing type in the notice text. A date the notice does not label is paired with the nearest hearing type it can find.
- Unlike inbound booking sync (which reads only event times), court hearing events Glade creates carry full hearing details.

## Related Features

- [Calendar Sync](./README.md)
- [Availability Blocking](./availability-blocking.md)
- [Connecting Calendars](./connecting-calendars.md)
- [PACER](../../integrations/pacer/README.md) — court hearing notices that feed calendar sync originate from court systems.
- [Court Notice Automations](../../workflows/court-notice-automations/README.md)
