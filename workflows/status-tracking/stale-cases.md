# Cases That Have Gone Quiet

## Overview

A case that has had no activity for **three months** is treated as **stale**, and Glade stops sending its automated follow-ups — both the emails and the text messages. Cases can sit untouched for months while continuing to chase a client who has stopped responding, which costs the firm messaging spend and pesters people on matters that are effectively dead.

## Key Behaviors

- **Activity means anything that happened on the case** — a message either way, a payment attempt including a failed one, a court notice arriving, a task completed, a note your team wrote. Any of these resets the three months.
- **A follow-up is not activity.** Sending a follow-up does not count as the case having moved, so a stale case cannot keep itself awake by chasing the client.
- **Nothing else about the case changes.** Stale is not a status: the case keeps whatever status it has, it is not archived, and its tasks stay open and assigned. Only the automated follow-ups stop.
- **You can override it either way.** A case can be marked stale by hand before three months have passed, or marked active so its follow-ups keep going however long it has been quiet. The override wins over the three-month measure until you clear it, at which point the case goes back to being judged on its last activity.
- **Finding them** — the cases list can be narrowed to stale cases, and the cases CSV export carries a column showing which cases are stale. This sits alongside the status filter rather than replacing it, so a stale case is still found by its own status too.

> TODO: Confirm where the stale override is set on a case, and whether an on-screen banner marks a stale case — that part of the change ships separately.

## Edge Cases & Limitations

- The three-month staleness threshold is fixed and is not configurable per firm. Where a case needs to keep chasing beyond it, mark the case active rather than looking for a setting.
- Staleness suppresses automated follow-ups only. Reminders tied to an appointment, and anything a team member sends by hand, are unaffected.

## Related Features

- [Status Tracking](./README.md)
- [Workflow List](./workflow-list.md)
- [Custom Statuses](./custom-statuses.md) — the Disable followups behavior
- [Tasks](./tasks.md) — automated reminders
