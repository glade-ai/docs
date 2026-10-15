# Hearings and 341 Meetings

## Overview

Glade reads the hearings scheduled in incoming court notices — including 341 meetings (meetings of creditors) — and records each one on the case, along with the trustee who will conduct a 341 meeting. It also works out which trustee is shown on the case.

## Key Behaviors

### 341 meeting notices

Glade processes incoming court notices about 341 meetings (meetings of creditors) and displays the name of the trustee who will conduct the meeting.

- When a 341 meeting notice identifies the conducting trustee by name — for example, via a video or phone conference format — Glade shows that person as the trustee for the meeting.
- The conducting trustee may differ from the case trustee listed elsewhere in the notice. Glade prioritizes the person actually conducting the meeting, not other named parties such as case-party trustees.

### The trustee shown on the case

The trustee shown on a case is worked out from the court emails Glade has received for that case.

- **The newest creditors-meeting email decides the trustee.** That includes the notice that schedules the meeting of creditors and the trustee's "341 Meeting Held" or "Continued" reports. Because the newest one wins, a case converted from Chapter 13 to Chapter 7 shows the Chapter 7 trustee once the Chapter 7 notice arrives. Previously an earlier Chapter 13 "341 Meeting Held" report outranked everything after it, so a converted case kept showing the old trustee.
- An email counts as a creditors-meeting email by its subject line as well as by how Glade classified it, so an unclassified notice or a certificate of mailing of the meeting of creditors is still used. A case number that happens to contain "341" does not count.
- **Without a creditors-meeting email, only a recognized trustee name is used.** Glade takes the newest court email that names a trustee on the U.S. Trustee Program's list, ignoring differences in periods and commas ("Robin R Weiner" matches "Robin R. Weiner"). Previously the newest email of any kind was used, which could put a course provider, a creditor, or a phrase such as "Bankruptcy Case Closed" in the trustee field.
- **If neither exists, no trustee is shown.** A blank is shown rather than a wrong name.
- The trustee is worked out each time the case is opened, so every case shows the corrected trustee on its next load with nothing to reprocess.

### Notices scheduling several hearings at once

Some courts set more than one hearing in a single notice — a confirmation hearing on one date and a 341 meeting on another, in the same docket entry. Glade records **each** hearing separately, matching every date to the hearing type named beside it.

- Previously only one hearing per notice was captured, and the date and the hearing type could come from different hearings — so a notice could produce a single entry showing a 341 meeting label against the confirmation hearing's date, with the other hearing missing altogether.
- When a notice is processed again — after a rescheduling notice, for example — Glade reconciles the hearings it already recorded against the notice: missing hearings are added and entries that no longer match are removed, so an earlier mismatched entry is corrected rather than duplicated.
- Each recorded hearing flows through to the rest of Glade independently: it appears on the case, and (where court hearing sync is enabled) creates its own calendar event. See [Calendar Sync](../../../appointments/calendar-sync/README.md).

## Edge Cases & Limitations

- A case with no court emails attached — most often because no case number has been entered in Glade — has no source for its trustee and shows none.
- A real trustee who is missing from the U.S. Trustee Program list, on a case with no creditors-meeting email, shows blank rather than by name.
- Notices processed before this correction are not revisited automatically. If your firm files in a district that routinely issues combined notices, ask Glade to reprocess your court notices for the affected date range.

## Related Features

- [Court Notices](./README.md)
- [Case number matching](./case-number-matching.md)
- [Calendar Sync](../../../appointments/calendar-sync/README.md)
