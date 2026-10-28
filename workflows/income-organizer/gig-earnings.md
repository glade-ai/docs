# Gig Earnings Statements

## Overview

Clients who drive or deliver for apps such as Uber, Lyft, DoorDash, Grubhub and Instacart often upload their app earnings statements to the Income Organizer. Glade reads these statements automatically and turns each one into monthly income rows, the same way it reads paystubs. Staff no longer have to type gig income in by hand.

## Key Behaviors

### Which documents are recognized

- Glade recognizes these gig earnings documents:
  - weekly and monthly earnings statements;
  - multi-month "proof of income" summaries;
  - the platforms' own monthly tax summaries;
  - screenshots taken in the app.
- **A gig statement is read as a gig statement, not as a paystub or a profit & loss statement.** Before this change, most of these files weren't read at all. The rest were misread as paystubs or as business profit & loss statements. When a file looks like both, Glade reads it as gig earnings, so its income is never counted twice.
- Regular paystubs from an employer are still read as paystubs.

### How income is recorded

- **One income row per calendar month.** A weekly or monthly statement becomes one row, like a paystub. A file covering several months, such as a 6-month proof of income, is split into one row for each month.
- If a statement doesn't print a year, Glade uses the year the file was uploaded.
- **Only the driver's share counts as income.** Tips and incentives are included. What riders or customers paid and the platform's fee are not.
- Mileage, payouts and platform fees appear in the extracted data for your team to review. They don't change any totals.
- **The upload slot decides the income type.** A gig statement uploaded into an employment slot counts as wages. There is no separate gig income type.

### Working with split files

- Deleting, restoring, including or excluding a file that was split by month applies to every monthly row it produced.
- Re-running extraction keeps the earlier result if the new read finds nothing.
- If a re-run reads a split file as a paystub or a profit & loss statement instead, its monthly rows are removed so the file isn't counted twice.

## Configuration

No setup is needed. Gig statements are read automatically for new uploads and for files your team re-runs.

## Edge Cases & Limitations

- **Overlapping files are not deduplicated.** If a client uploads a monthly summary and the weekly statements for the same month, both are counted. Exclude one of them with the record's include/exclude switch (see [Including and Excluding Income Records](./including-excluding-records.md)).
- **A single PDF that combines a real paystub with a gig statement is read as gig earnings only.** The paystub income in that file isn't counted. Upload the paystub on its own.
- **A list of 12 or more months with no years printed** can place its oldest month in the current month. Check the months on long statements that don't print years.
- **Organizers on Glade's older income calculation don't count files that were split by month.** Those organizers can only place a file on one pay date.
- **Files read before this change keep their old rows.** For example, a DoorDash statement may have been read as a paystub, or an Uber summary as a profit & loss statement. Re-running the file puts the new values into review. An old profit & loss record and any business source it created are not removed and need to be cleaned up by hand.

> TODO: Confirm the exact list of gig platforms supported beyond Uber, Lyft, DoorDash, Grubhub and Instacart.

## Related Features

- [Income Organizer](./README.md)
- [Paystub Extraction](./paystub-extraction.md)
- [Upload Processing Status](./processing-status.md)
- [Including and Excluding Income Records](./including-excluding-records.md)
- [Profit & Loss Statements](./business-and-rental-income/profit-and-loss-statements.md)
- [Income Documents](../document-collection/income-documents.md)
