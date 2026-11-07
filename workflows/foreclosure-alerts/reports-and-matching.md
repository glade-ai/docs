# Foreclosure Reports and Matching

## Overview

Your firm uploads the monthly foreclosure report it receives, and Glade compares each listing against the addresses and debtor names on your open bankruptcy cases. Each candidate gets a match percentage, and a match at or above your firm's threshold flags the case. This page covers uploading and activating reports, how matching works, and when cases are re-checked.

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
- **An exact address on a recorded property scores 100%.** When the report's address has the same house number, street, and ZIP as a real-estate asset recorded on the case, the match is scored at 100% from the address alone. The debtor's name cannot pull that score down, so a misspelled or since-changed name on the case does not hide a match on the client's own scheduled property. A different house number on the same street, and matches that come from the residential or contact address, are still scored with the name as supporting evidence, as before.
- **Debtor AKAs count as debtor names.** The other names recorded for either debtor on the case — the "also known as" names on the schedules or from the credit report, including business names — are compared against the owner and mortgagor on the report alongside the debtors' legal names. A listing filed under a maiden name, a former married name, or a business name is found and scored the same way as one under the legal name. Where an AKA records only a surname, it is compared together with that debtor's first name.
  - When the report names a debtor only by an AKA, the match evidence says the alias (AKA) matched the report's owner or mortgagor name.
  - An exact address on a recorded property with an AKA on the report's ownership line scores 100%, as it would with the legal name.
  - Previously AKAs were not used at all, so a listing under an AKA was treated as a stranger's name: it could be missed entirely, or be flagged with a low percentage even at the client's exact address.
  - Cases with no AKAs are matched exactly as before.
- **Evidence is split into what matched and what did not.** The match card separates the signals that raised the percentage (ZIP match, name match, close address) from the ones that held it below 100% (no ZIP available, a one-sided street qualifier, a name that is similar but not identical). This is what tells a paralegal where the percentage came from.
- **Cases are re-checked when the underlying data changes.** Editing a property address, the client's residential address, the client's contact record, or a debtor's name re-runs the check for that case. Unrelated edits — the case number, attorney fields, a phone number — do not.

For what happens when a match reaches the threshold, see [Flags and Review](./flags-and-review.md).

## Configuration

- **Match threshold.** Your firm sets the percentage at which a match is treated as actionable. It defaults to **82%** and is entered as a whole number. Raise it for fewer, safer matches; lower it to catch more. The page records who last changed it and when.
- **Threshold changes apply to future checks only.** Matches already recorded are not re-scored, so changing the threshold does not retroactively flag or unflag existing cases.

> TODO: Confirm where reports are uploaded and activated in the dashboard, where the match threshold is set, and where a case's foreclosure evidence is viewed.

## Edge Cases & Limitations

- **Only open filing cases are checked.** Intake and ancillary workflows, and cases that have been closed, dismissed, discharged, archived, cancelled, or completed, are left out.
- **A contact record only matches within the firm that holds it.** Another firm's record for the same person is never used.
- **A name alone never produces a match.** Names raise or lower the confidence of an address match; they cannot create one. An address that is too incomplete to identify a property is skipped even when the name matches exactly.
- **The match card lists the debtors' legal names only.** An AKA that produced a match is named in the evidence, not in the card's list of debtor names.
- **A residence or contact-address match can still show a low percentage.** The exact-address 100% rule applies only to a recorded real-estate asset. A match on the client's residential or contact address is still scored with the name as evidence.
- **Reports uploaded before residence matching shipped are not re-checked on their own.** Glade re-runs matching against your firm's active report; you do not need to upload the file again. Individual cases also pick it up whenever their address or debtor name is next edited.
- **Existing match scores are not recalculated on their own.** A match recorded before exact-address scoring or AKA matching changed keeps its stored percentage until the case is checked again — for example, when the active report is re-run or the case's address or debtor name is next edited.
- **Report history is read-only.** There is no way to merge a corrected file into an earlier report — upload the corrected file and activate it.

> TODO: Confirm whether Glade re-runs firms' active reports so that listings filed under an AKA are picked up, or whether firms should ask support to re-run their report.

## Related Features

- [Foreclosure Alerts](./README.md)
- [Flags and Review](./flags-and-review.md)
- [The Foreclosure Report](./foreclosure-report.md)
