# Hearings and 341 Meetings

## Overview

Glade reads the hearings scheduled in incoming court notices — including 341 meetings (meetings of creditors) — and records each one on the case, along with the trustee who will conduct a 341 meeting.

## Key Behaviors

### 341 meeting notices

Glade processes incoming court notices about 341 meetings (meetings of creditors) and displays the name of the trustee who will conduct the meeting.

- When a 341 meeting notice identifies the conducting trustee by name — for example, via a video or phone conference format — Glade shows that person as the trustee for the meeting.
- The conducting trustee may differ from the case trustee listed elsewhere in the notice. Glade prioritizes the person actually conducting the meeting, not other named parties such as case-party trustees.

### Notices scheduling several hearings at once

Some courts set more than one hearing in a single notice — a confirmation hearing on one date and a 341 meeting on another, in the same docket entry. Glade records **each** hearing separately, matching every date to the hearing type named beside it.

- Previously only one hearing per notice was captured, and the date and the hearing type could come from different hearings — so a notice could produce a single entry showing a 341 meeting label against the confirmation hearing's date, with the other hearing missing altogether.
- When a notice is processed again — after a rescheduling notice, for example — Glade reconciles the hearings it already recorded against the notice: missing hearings are added and entries that no longer match are removed, so an earlier mismatched entry is corrected rather than duplicated.
- Each recorded hearing flows through to the rest of Glade independently: it appears on the case, and (where court hearing sync is enabled) creates its own calendar event. See [Calendar Sync](../../../appointments/calendar-sync/README.md).

## Edge Cases & Limitations

- Notices processed before this correction are not revisited automatically. If your firm files in a district that routinely issues combined notices, ask Glade to reprocess your court notices for the affected date range.

## Related Features

- [Court Notices](./README.md)
- [Case number matching](./case-number-matching.md)
- [Calendar Sync](../../../appointments/calendar-sync/README.md)
