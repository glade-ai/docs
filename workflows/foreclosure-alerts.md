# Foreclosure Alerts

## Overview

Foreclosure Alerts compares the monthly foreclosure report your firm already receives against your open bankruptcy cases and flags the cases that appear on it. A case that matches is given a **Foreclosure** designation, which your team can filter the case list by, and — where the automation is turned on — an urgent task for the paralegal on the case. Staff can also flag a case by hand when they know about a foreclosure the report missed.

## Key Behaviors

- **Your firm uploads the report.** The report is uploaded as a CSV file. Glade checks the file when it arrives and reports how many rows it could read: rows with a usable property address and owner, rows that are incomplete, and rows it had to reject. Uploading the same file twice is detected rather than duplicated.
- **One report is active at a time.** Activating a new upload replaces the previous one. Earlier reports are kept for reference but are not matched against again. Activating a report starts a check across your firm's open filing cases.
- **Matching is deterministic, not AI.** Glade compares the property address on the report against the addresses it holds for the case, and uses the debtor's name as corroborating evidence. Each candidate gets a match percentage.
- **Three kinds of case address are checked.** A match can come from:
  - a real-estate asset recorded on the case,
  - the client's **primary residential address** on the case, or
  - the client's **contact record** at your firm.

  A case that has none of these — or whose address is too incomplete to identify a property — is not matched. Where the same property appears in more than one of the three, it is treated as one property and the asset record is preferred as evidence.
- **A residence match does not assert that the client owns the property.** When a match comes from the residential or contact address rather than a recorded real-estate asset, the evidence says so explicitly, and no asset is created on the case. Treat it as a lead to check, not a finding of ownership.
- **Evidence is split into what matched and what did not.** The match card separates the signals that raised the percentage (ZIP match, name match, close address) from the ones that held it below 100% (no ZIP available, a one-sided street qualifier, a name that is similar but not identical). This is what tells a paralegal where the percentage came from.
- **A match at or above your firm's threshold applies the Foreclosure designation** and creates an urgent task for the paralegal assigned to the case, due the next calendar day in your firm's timezone. If no one holds the paralegal role on the case, the task goes to the team queue unassigned rather than not being created at all.
- **Cases are re-checked when the underlying data changes.** Editing a property address, the client's residential address, the client's contact record, or a debtor's name re-runs the check for that case. Unrelated edits — the case number, attorney fields, a phone number — do not.
- **Staff can flag a case by hand.** A case can be tagged as foreclosure directly, with a note explaining why; the note is required. This writes the same designation the report does, so the case appears in the same filters and reports. A hand-applied flag posts a note on the case, does not create the urgent paralegal task (whoever applied it already knows about the case), and survives the next report activation. A case can carry one hand-applied flag at a time, and a case that is already designated cannot be flagged again.
- **Removing a flag records who removed it and why**, and stops that same property from being flagged again on that case. Removing a flag does not complete the paralegal task — close that separately.
- **Finding flagged cases.** The case list can be filtered to cases that currently carry a Foreclosure designation, or to those that do not, and the filter carries through to the cases CSV export.

## Configuration

- **Match threshold.** Your firm sets the percentage at which a match is treated as actionable. It defaults to **82%** and is entered as a whole number. Raise it for fewer, safer matches; lower it to catch more. The page records who last changed it and when.
- **Threshold changes apply to future checks only.** Matches already recorded are not re-scored, so changing the threshold does not retroactively flag or unflag existing cases.
- **Paralegal role.** The urgent task goes to whoever holds the paralegal role on the case, so that role needs to be assigned for the task to reach a person rather than the team queue.

> TODO: Confirm where reports are uploaded and activated in the dashboard, where the match threshold is set, and where a case's foreclosure evidence is viewed.

## Edge Cases & Limitations

- **Only open filing cases are checked.** Intake and ancillary workflows, and cases that have been closed, dismissed, discharged, archived, cancelled, or completed, are left out.
- **A contact record only matches within the firm that holds it.** Another firm's record for the same person is never used.
- **A name alone never produces a match.** Names raise or lower the confidence of an address match; they cannot create one. An address that is too incomplete to identify a property is skipped even when the name matches exactly.
- **Reports uploaded before residence matching shipped are not re-checked on their own.** Glade re-runs matching against your firm's active report; you do not need to upload the file again. Individual cases also pick it up whenever their address or debtor name is next edited.
- **A dismissed match stays dismissed.** Once a flag is removed for a property, later checks skip that property on that case even if a new address source later points at the same house.
- **Report history is read-only.** There is no way to merge a corrected file into an earlier report — upload the corrected file and activate it.

> TODO: Confirm whether automatic designation and the urgent paralegal task are enabled for all firms or currently limited to pilot firms, and whether Foreclosure Alerts is available to every firm.

## Related Features

- [Status Tracking](status-tracking/README.md)
- [Task Templates](./task-templates.md)
- [Automation Rules](./automation-rules.md)
