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
- Each appointment type can be given a calendar color, used to tint its bookings on the firm's booking calendar. See [Color-coding appointment types on the calendar](#color-coding-appointment-types-on-the-calendar).

### Routing bookings to a calendar by county

An appointment type can send its bookings to a particular calendar based on **the county the client is in**. A firm that covers several counties from different offices, or that has a different attorney responsible for each, can have a booking land on the right calendar when it is made rather than being moved by hand afterwards.

- Rules are set per appointment type, one county to one calendar. A county with no rule on that appointment type is not routed.
- **Routing only applies when it has an answer for every part of it.** The booking falls back to your firm's usual calendar selection — exactly as it worked before — when the appointment type has no county rules, when no county is recorded for the client, when the recorded county is not one Glade recognizes, or when no rule covers the client's county. A booking is never left without a calendar because routing did not resolve.
- **An appointment type with no county rules is unchanged.** Nothing about your existing booking behavior changes until your firm sets a rule up.

> TODO: Confirm where county routing rules are configured on an appointment type, and which county the rules match on — the one a client supplies at booking time or the one on their address in Glade.

### Defining availability

- Firms set up recurring availability patterns by specifying days of the week and start/end times.
- Availability is defined in the firm's local timezone.
- The system generates concrete bookable time slots from these patterns.
- Individual team members can have their own separate availability schedules.
- External calendar events from connected calendars (Google Calendar or Outlook) automatically block availability to prevent double-booking.
- Only events marked as "busy" block availability. Events marked as "free" or "transparent" do not.
- A synced calendar event counts against the product's concurrent booking limit rather than blocking the slot outright. On a product that allows one booking per slot, an event on the assigned team member's calendar closes that slot. On a product that allows several, the event takes one place and the remaining places stay bookable. The Glade booking and the calendar event Glade created for it count as one, not two.
- A synced calendar event does more than hide the slot — it is also enforced when a booking is saved. Creating, rescheduling, or reassigning a booking on top of a hearing or meeting already on the assigned team member's synced calendar is rejected. Previously only Glade's own Blocked windows were enforced at save time, so a slot list that was out of date — or a booking written by a staff member covering for someone else — could still land a client on top of a court hearing. Firm team members can override deliberately with **Schedule Anyway**.
- In addition to recurring availability, you can add **availability blocks** for specific date ranges. Each block has a type that determines its effect on bookable time:
  - **Blocked** — removes the covered times from bookable availability. Clients cannot schedule into these windows. Use this for vacations, court dates, off-site days, or any other time you should not be booked.
  - Other block types (for example, blocks used purely for visual annotation on the calendar) do not remove availability — only blocks marked as Blocked actually prevent new bookings.
- Blocked times are **hard blocks**. They always remove the covered slots from the booking calendar regardless of the product's concurrent booking limit — even a product that allows multiple overlapping bookings does not offer slots inside a blocked window. Firm team members can still book into one deliberately with **Schedule Anyway**, described below.
- A Blocked entry that is not assigned to a specific team member applies to **every team member**. Use this when you need to take the firm off the calendar for everyone at once (for example, an office closure) without creating one entry per team member.
- Firm team members can deliberately book or reschedule into a blocked window using **Schedule Anyway**. When a team member picks a blocked (or otherwise conflicting) slot, Glade asks them to confirm; confirming overrides the block and saves the booking. This lets a firm keep its calendar blocked to pause new bookings while still moving an existing appointment into that time — no need to temporarily reopen the calendar first.
- Clients and other non-team members cannot book into blocked time even if they reach a blocked slot. For them, attempting to create or reschedule into a blocked window — for example from a stale link or an out-of-date slot list — is rejected with an error rather than silently saved.

### Availability management view

The **Availability** tab in the Bookings section gives you a centralized place to review and manage availability across all services and team members.

The tab has two sub-views:

- **Team Members**: Shows availability settings organized by team member.
- **Services**: Lists all schedulable services. For each service, a summary shows which team members have availability configured. Clicking a service name opens the availability editor for that service inline. A **View in services** link navigates to the full service settings page.

Clicking a service in either view opens the availability editor directly — you can update availability without leaving the Bookings section.

### How far ahead a client must book

Each appointment type carries a **minimum booking notice** — how much warning your firm needs before an appointment starts. It is set per appointment type under **Availability → Booking settings**, and the choices are same day, 8 hours, 24 hours, 48 hours, 72 hours, 5 days, or 7 days.

- Time slots that fall inside the notice window are not offered to clients. A firm needing a day's warning shows tomorrow's slots but not this afternoon's.
- **The window is enforced when the booking is saved, not just hidden on the calendar.** Previously it only controlled which slots were displayed, so a client working from a stale slot list, an old link, or a page left open could still book a time the calendar had deliberately hidden. That booking is now refused.
- **Firm team members are not held to the window.** Staff booking a client in, or moving an existing appointment, can still use a time inside the notice period — useful for taking a same-day appointment over the phone on a service that otherwise requires notice.
- An appointment type with no notice set allows same-day booking. Choosing **same day** explicitly has the same effect and is worth setting deliberately on services where same-day consultations are part of how your firm works.
- This is a per-appointment-type setting, so a firm can require a week's notice for a signing while leaving consultations open same day.

### Recording what happened at an appointment

Your firm can keep its own list of appointment outcomes — **No show**, **Claimed**, or whatever labels match how your team works — and attach one to a booking after the fact. This is how the calendar and daily reports come to record what actually happened, rather than only whether the appointment was scheduled.

- **Your firm defines the list.** Nothing is provided as a starting point, so every firm begins with an empty list and no outcome on any booking until someone creates them. Outcomes can be reordered so the ones your team uses most sit at the top.
- **An outcome is separate from the booking's status.** Attaching one does not move the booking through its lifecycle — a completed appointment marked **No show** is still recorded as completed. The statuses in [Booking lifecycle](#booking-lifecycle) are unchanged.
- **It is also separate from workflow custom statuses.** The two lists are kept apart deliberately: an appointment outcome carries none of the case-tracking behavior a workflow status does, and choosing one triggers nothing.
- Only firm team members can set or clear a booking's outcome. Clients cannot.
- An outcome has to belong to your firm and be currently in use — an archived or deleted outcome cannot be attached to a booking.
- **Retiring an outcome does not rewrite history.** Archiving one keeps it on the bookings that already carry it while removing it from the list of choices, so past appointments stay readable.
- The outcome appears on the booking and as an **Outcome** column in the bookings report and its spreadsheet export.

> TODO: Confirm where the outcome list is managed in firm settings and where the outcome is chosen on an individual booking.

### Client booking flow

1. The client views the firm's product or service listing. For free sessions, the booking button reads **Book a call**; for paid sessions it shows the session price.
2. The client selects a product and initiates scheduling.
3. A calendar displays available dates and time slots.
4. Times are shown in the client's own timezone, with a timezone picker above the slot list if they want to view them in a different one.
5. The client selects a date and time.
6. The booking is confirmed and created.
7. If the product has video conferencing enabled, a meeting link is generated automatically.
8. The client receives a confirmation with booking details.

### Asking a booking client for their county

An appointment type can require the client to give their **county** when they book. This is for firms whose work depends on where the client lives — which office covers them, which court their case would be filed in, and whether the firm practices in their county at all.

- **The requirement is set per appointment type**, and it is off until your firm turns it on. A service with no use for a county asks for nothing, so nothing changes for a firm that does not enable it.
- **The client picks their county from a list rather than typing it.** The list is searchable by county name and can be narrowed to a state, so a client finds their county without needing to spell it the way the courts do. Picking from the list is what makes the answer usable downstream — a typed county has to be matched before it can be relied on, and misspellings are the usual reason that fails.
- **Requiring the county is separate from requiring the client's address.** The two settings are independent: an appointment type can ask for one, both, or neither.
- **Existing appointment types are unchanged.** Turning the requirement on affects bookings made afterwards. It does not go back and ask for a county on appointments already booked, and it does not block a client from managing a booking they made before the setting changed.

### Counties your firm serves

Separately from what a booking asks the client, your firm can record **the counties it serves** — the list of counties your practice covers.

- The list is set once for the firm, not per appointment type or per team member.
- Counties are chosen from the same searchable catalog the booking form uses, so the names your firm records and the ones clients pick from are the same names.
- A firm that records nothing is treated as having no restriction recorded, which is how every firm starts.

> TODO: Confirm where the served-counties list is edited in the dashboard, and what Glade does with it once recorded — whether it filters which appointment types a client in an unserved county is offered, drives office routing, or is reporting only. The setting is stored and editable; how it is acted on is not established from the source change.

### While the booking calendar is loading

A consultation calendar has to fetch a month's availability before it can show which days are open. Until that finishes, the calendar makes it clear it is still loading rather than showing an answer it does not have yet.

- **A day with no availability data yet is not shown as booked.** The whole grid is covered by a loading indicator until the month's availability arrives, and days grey out as unavailable only once Glade actually knows they are.
- Previously a month that had not loaded looked exactly like a month with nothing free. Receptionists reading a grey calendar told callers there were no consultation slots when there were — the calendar was simply still fetching. If your team has been turning bookings away on a full-looking calendar, this is the likely cause.
- Once the month has loaded, days that are genuinely booked or unavailable grey out as they always did.
- **Months load in well under a second in typical cases.** A month's availability is fetched in one go rather than day by day, so the wait that made the loading state noticeable in the first place is largely gone.
- If adding a session to the cart does not complete within about ten seconds, the attempt stops and reports the failure instead of leaving the button spinning indefinitely. Try again, or reload the calendar.

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

### Color-coding appointment types on the calendar

Each appointment type can be given a color. Bookings of that type are tinted with it on the firm's booking calendar, so the calendar shows at a glance which kind of appointment each block is — a consultation, a signing, a status check-in.

- The color is set on the appointment type itself, alongside its other settings, and applies to every booking of that type.
- Your firm picks the colors. No color carries a fixed meaning and there is no preset mapping, so choose whatever scheme matches how your team reads the calendar.
- **The color follows the appointment type, not the team member.** Two appointment types assigned to the same person show as two colors; one appointment type spread across several team members shows as one.
- Appointment types have no color until you set one, so a firm that has not chosen colors sees the calendar exactly as before. Clearing a color returns that type's bookings to the standard appearance.
- This is a display setting. It does not affect availability, booking rules, assignment, or reminders.

> TODO: Confirm where the color is chosen in the dashboard, whether a palette is offered or any color can be picked, and whether the color appears anywhere other than the booking calendar.

### Rescheduling

- Both clients and firm staff can reschedule appointments.
- Rescheduling checks availability to prevent conflicts with existing bookings.
- When rescheduling, available time slots are filtered to the team member originally assigned to the booking. This ensures the rescheduled appointment stays with the same team member.
- By default, clients cannot reschedule within 48 hours of the appointment start time. This protects firms from last-minute schedule changes.
- Firms can override this restriction and allow client rescheduling within 48 hours on a per-product basis.
- Firm staff can always reschedule regardless of the 48-hour window.
- When a firm blocks calendar time to pause new bookings, firm staff can still move an existing appointment into that blocked time by confirming **Schedule Anyway** when they select the blocked slot. Clients cannot reschedule into blocked time this way.
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
- Every client-facing reference to an appointment shows the time in the recipient's own timezone — the booking confirmation, email and text reminders, client-portal messages, and the calendar invite. A client in Eastern time who books a "2:30 PM" slot with a firm that operates in Pacific time sees 2:30 PM Eastern everywhere, and the calendar invite lands at the correct local time. Previously these could show the firm's time instead, so an appointment could appear at the wrong hour on the client's calendar and invites.
- A timezone picker sits above the slot list so a client can view times in a different timezone — useful when they are travelling or booking on behalf of someone else. Changing it re-sorts the slots into that timezone's days, and the choice is saved to the client's profile so later bookings open in the same timezone.
- The picker starts on the client's saved profile timezone if they have one, otherwise the timezone their device reports.
- Whichever timezone is on screen, the client books the exact moment they clicked. A client in Eastern time booking a "2:30 PM" slot from a Pacific-time firm gets 2:30 PM Eastern, and the firm sees the matching time on their own calendar.
- Firm-side views — the Bookings section, the firm dashboard, and internal staff notifications — continue to show times in the firm's timezone.
- The system validates timezone inputs and defaults to US/Eastern if a timezone cannot be determined.

### Booking into a conflicting time

- When a selected slot conflicts with an existing booking, the scheduler flags the conflict and offers **Schedule Anyway** so a team member can double-book deliberately.
- **Schedule Anyway** works both when creating a booking and when rescheduling one. Previously it was only honored on the reschedule path — on a new booking the click appeared to do nothing and the appointment was never created. If your team hit that and worked around it by booking a non-conflicting time and then rescheduling into the conflict, that workaround is no longer necessary.
- **Schedule Anyway** also covers a **Blocked** availability window. A firm team member who selects a blocked slot is asked to confirm, and confirming saves the booking into that window — so a firm can keep its calendar blocked to pause new bookings while still moving an appointment into that time. Clients and other non-team members cannot book into blocked time this way; for them a blocked window remains a hard block. See [Defining availability](#defining-availability).
- **Events on a synced calendar are treated the same way.** An appointment that would overlap a hearing, meeting, or other busy event on the assigned team member's connected calendar is refused unless a team member confirms **Schedule Anyway**. This applies when creating a booking, when rescheduling one, and when reassigning a scheduled booking to a different team member — so covering for a colleague no longer risks booking a client over that colleague's court hearing.
- Moving a booking is not blocked by the calendar event Glade created for the booking itself, so rescheduling an appointment to a new time works normally.
- Only calendars that are switched on for syncing are checked. An event on a calendar the team member has disabled does not block the booking, matching what the slot list shows.

### Booking a slot that is already full

A slot is full when the number of things already occupying it — existing Glade bookings for that team member, plus any synced calendar events that are not those bookings' own events — has reached the product's concurrent booking limit. Booking into a full slot is refused, and the refusal is now visible at the moment of booking.

- The booking fails with an error instead of showing a confirmation. Previously the confirmation screen appeared even when the booking had not been saved, so a client or staff member could be told an appointment existed when it did not — no calendar event was created, no reminders were sent, and any workflow the appointment was meant to start never ran. If your team has seen "confirmed" consultations that never appeared on anyone's calendar, this is the cause.
- Because the check now counts occupancy against the concurrent booking limit rather than treating any overlap as a conflict, products configured for several concurrent bookings behave as configured. A single overlapping calendar event no longer prevents booking on a product that allows five.
- **Blocked** availability windows are unaffected. They remain a hard block regardless of the concurrent booking limit, and firm team members override them with **Schedule Anyway** as described above.

A slot that fills between the moment the client loads the time list and the moment they confirm is the common way to hit this. Reloading the booking calendar shows the slot as taken.

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

#### Email when a team member is assigned a Schedule Appointment task

When a team member is newly assigned to a **Schedule Appointment** task on a case, they receive an email telling them so, with a link to the case. Reassigning the task now reaches the new assignee — previously nothing was sent, and a task could sit with someone who had no idea it was theirs.

- **Only the people newly added get the email.** Bookings re-check their assignees whenever they are created, rescheduled, skipped, canceled, or unscheduled, and when collaborators change. Someone who was already on the task is not emailed again each time one of those happens.
- **You are not emailed about your own action.** Assigning the task to yourself sends nothing.
- **This covers the Schedule Appointment task only.** Other task types — responding to a discussion, reviewing a document request, and the rest — do not send an assignment email. A task asking a client to pick from your availability is also excluded, because the case owners already receive their own notification for it.
- No setting is involved: the email is on for every firm.

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
| Calendar color | Color used to tint this appointment type's bookings on the firm's booking calendar. Optional — appointment types have no color until one is set. |
| Client county required | Whether a client booking this appointment type must give their county. Off until your firm turns it on. Independent of whether the client's address is required. |
| Counties served | The counties your firm's practice covers, recorded once for the firm. Empty until your firm records them. |
| Minimum booking notice | How far ahead of the appointment a client must book: same day, 8, 24, 48, or 72 hours, or 5 or 7 days. Set per appointment type under Availability → Booking settings. Appointment types with nothing set allow same-day booking. |
| Appointment outcomes | The firm's own list of labels recording what happened at an appointment (for example No show). Firm-defined and empty until you create them; can be reordered and archived. |

## Edge Cases & Limitations

- Unscheduled bookings expire if no time is selected before the expiration date.
- The 48-hour rescheduling restriction applies to clients only. Firm staff can always reschedule.
- Concurrent booking limits are per time slot, not per day.
- The full-slot check applies to bookings that have an assigned team member. A booking with nobody assigned has no calendar to check against, so the limit is not enforced for it.
- If no team member availability is configured for a product, the product may show no available time slots.
- External calendar events marked as "free" do not block availability. Only "busy" events create blocks.
- Enforcement against synced events depends on the event having reached Glade. A commitment a team member blocked out directly in Outlook that has not yet synced is not known to Glade and does not prevent a booking.
- A booking with no assigned team member is not checked against any synced calendar, since there is no team member whose calendar to compare it with.
- Timezone mismatches can occur if the firm's timezone setting is incorrect.
- A calendar still showing its loading indicator has no availability to report yet. Wait for it to finish before concluding a month is full — a month that loads and then shows every day greyed out is genuinely unavailable.
- Booking a time slot does not guarantee a specific team member unless one is pre-assigned to the product.
- Calendar colors are read from the appointment type each time the calendar is drawn, so changing a color re-tints that type's existing bookings as well as new ones. There is no way to color one booking differently from others of the same type.
- Requiring the county on an appointment type applies to bookings made afterwards. Appointments already on the calendar have no county recorded against them, and there is no way to ask for one retroactively.
- The county requirement and the counties your firm serves are two separate settings. Recording the counties your firm serves does not by itself require a client to give theirs, and requiring a client's county does not check it against your firm's list.
- A county your firm needs that is not in the searchable catalog cannot be selected. Contact support with the county and state to have it added.
- The minimum booking notice applies to clients only. It does not stop a team member booking or moving an appointment inside the window, so it is not a way to protect a team member's time from their own colleagues — use a **Blocked** availability window for that.
- Changing the minimum booking notice does not affect appointments already booked. A client who booked before the change keeps their time.
- A booking carries at most one outcome. Recording two things about the same appointment means choosing which one the label should capture, or noting the rest on the case.
- Appointment outcomes are per firm. They are not shared between firms and nothing is set up in advance, so a new firm sees no outcome option on its bookings until the list is created.

## Related Features

- [Calendar Sync](./calendar-sync.md)
- [Reminders](./reminders.md)
- [Video Consultations](./video-consultations.md)

