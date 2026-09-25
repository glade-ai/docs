# Including and Excluding Income Records

## Overview

Each income record carries its own switches for whether it counts toward Schedule I and whether it counts toward the means test. Turning one off is a deliberate choice your team makes about that record, and Glade preserves it.

## Key Behaviors

- Excluding a record stays excluded when the underlying document is read again — for example after a re-upload, a re-run of the extraction, or an automatic background retry. Previously any re-read of the document silently switched the record back to counted, in both the income organizer and the means test, so a record your team had deliberately left out could reappear in the totals without anyone changing it.
- A first-time extraction still starts with the record counted, and a document Glade could not read keeps its record out of the totals until a later successful read.
- **Clearing the switches holds on the first try.** Turning **Include in Monthly Totals** or **Include in Means Test** off — for a whole income source or for one record — sticks, including on organizers with many paystubs and while AI is still reading uploaded documents in the background. Previously rows could re-check themselves moments after being cleared, so the same action had to be repeated several times before it held; that only happened on busy organizers, which is why it looked intermittent. If a change cannot be saved, the switch returns to its previous position and an error message appears, rather than appearing to save and then reverting on the next refresh.

### Income read from an upload now counts toward Schedule I

Income extracted from an uploaded document was being recorded as **excluded from Schedule I** even though nobody had excluded it. The record appeared on the case with its figures correct, the means test counted it, and Schedule I silently left it out.

- **What it looked like:** a case with six pay stubs, every figure read correctly, a means test reporting the income in full, and Schedule I showing nothing. Nothing was flagged and no error appeared, because a record excluded from Schedule I is an ordinary thing for a record to be.
- **Uploads now arrive counted**, the same as a record entered by hand, so newly read documents reach Schedule I.
- **Your own exclusions are unaffected.** A record your team deliberately left out stays out, including through a re-read of the document. The fix distinguishes the two.
- **Cases prepared while this was happening are not corrected on their own.** The problem ran from around May 2026 and affected thousands of cases — mostly wage income from pay stubs rather than business income — with some showing no Schedule I income at all and others understated. **Re-check Schedule I on any case prepared since May 2026 where income was read from uploaded documents**, and contact support to have affected cases repaired rather than re-entering the figures by hand.
- A case whose means test and Schedule I disagree about the same documents is the signature to look for.

## Configuration

| Setting | Description |
|---------|-------------|
| Count toward Schedule I | Whether an individual income record is included in the Schedule I figure. Set per record; preserved when the document is read again |
| Count toward means test | Whether an individual income record is included in the means test. Set per record; preserved when the document is read again |

## Edge Cases & Limitations

- Income records written before the Schedule I exclusion was fixed keep the exclusion they were written with. They are not corrected when a case is reopened or recalculated — the case has to be repaired, which support does.

## Related Features

- [Income Organizer](./README.md)
- [Schedule I](./schedule-i.md)
- [Means Test](./means-test.md)
- [Editing Income Records](./editing-income-records.md)
- [Upload Processing Status](./processing-status.md)
