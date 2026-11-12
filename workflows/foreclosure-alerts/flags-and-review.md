# Foreclosure Flags and Review

## Overview

A case that matches the foreclosure report, or that staff flag by hand, carries a **Foreclosure** designation. Staff then review each flag: they **affirm** it when the foreclosure is real, or **dismiss** it when it is not. This page covers what a flag does on the case, flagging by hand, affirming and dismissing, and the review status shown on the match card.

## Key Behaviors

### What a flag does

- **A match at or above your firm's threshold applies the Foreclosure designation** and creates an urgent task for the paralegal assigned to the case, due the next calendar day in your firm's timezone. If no one holds the paralegal role on the case, the task goes to the team queue unassigned rather than not being created at all. For how matches are scored, see [Reports and Matching](./reports-and-matching.md).
- **Staff can flag a case by hand.** A case can be tagged as foreclosure directly, with a note explaining why; the note is required. This writes the same designation the report does, so the case appears in the same filters and reports. A hand-applied flag posts a note on the case, does not create the urgent paralegal task (whoever applied it already knows about the case), and survives the next report activation. A case can carry one hand-applied flag at a time, and a case that is already designated cannot be flagged again.

### Affirming a flag

Staff can **affirm** a flag to record that the foreclosure is real, not only dismiss the ones that are wrong.

- Affirming takes an optional note.
- Only a flag that is currently on can be affirmed. Hand-applied flags can be affirmed as well as report matches.
- Affirming covers every current flag on the case for the same property, the same way removing a flag does.
- Affirming posts a note on the case reading **Foreclosure flag affirmed.**, followed by the affirmation note when one was given.
- Affirming again replaces the earlier affirmation and its note.
- The affirmation does not carry into later reports. When a later month's report matches the same property again, that new match starts unreviewed.
- Affirming does not change the designation, filters, or the paralegal task — the case stays flagged.

### Dismissing (removing) a flag

- **Removing a flag records who removed it and why**, and stops that same property from being flagged again on that case. Removing a flag does not complete the paralegal task — close that separately.
- **Removing a flag posts a note to the case's internal notes.** The note reads *Foreclosure flag removed.*, followed by the reason when one was given, and is posted as the person who removed it — the same way a note added while the flag is on already appears. One note is posted per removal, even when the removal clears the same property from more than one match. If the note cannot be posted, the flag is not removed, so a removal never happens without its record in the notes. Previously the reason was saved on the match but nothing appeared in the case's notes.
- A flag that was affirmed and later removed reads as dismissed.

### Review status

Every flag has a review status:

| Status | Meaning |
|--------|---------|
| **Unreviewed** | The flag is on and nobody has affirmed or removed it. |
| **Affirmed** | A team member confirmed the flag and it is still on. |
| **Dismissed** | A team member removed the flag. |

- **The match card on the case shows the latest review**: whether the flag was affirmed or dismissed, the note, who did it, and when. Previously the reason a flag was dismissed showed only on the report, so someone working inside the case could not see why.
- A flag Glade clears on its own is not a review and does not read as dismissed.
- The foreclosure report has a **Review status** column and filter — see [The Foreclosure Report](./foreclosure-report.md). An affirmed flag no longer counts as unreviewed there.

## Configuration

- **Paralegal role.** The urgent task goes to whoever holds the paralegal role on the case, so that role needs to be assigned for the task to reach a person rather than the team queue.

> TODO: Confirm the labels of the Affirm and remove-flag actions on the match card.

## Edge Cases & Limitations

- **Flags are affirmed and dismissed from the case, not from the report.** The foreclosure report rows have no Affirm or remove-flag action.
- **A dismissed match stays dismissed.** Once a flag is removed for a property, later checks skip that property on that case even if a new address source later points at the same house.
- **Removals made before removal notes were added have no note.** Their reasons are not posted retroactively; they remain visible in the report's review note column.
- **Each month's match is reviewed on its own.** An affirmation on one month's match does not mark a later month's match for the same property as affirmed.
- Flags reviewed before affirming was available read as **Unreviewed** or **Dismissed**.

## Related Features

- [Foreclosure Alerts](./README.md)
- [Reports and Matching](./reports-and-matching.md)
- [The Foreclosure Report](./foreclosure-report.md)
- [Task Templates](../task-templates.md)
