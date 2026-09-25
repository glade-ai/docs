# Exporting Custom Reports

## Overview

A custom report can be exported to CSV. The export is built from the report itself, so it carries the same columns, filters, and sort order as the report on screen. The same export behavior applies to case, court notice, and payments reports.

## Key Behaviors

- **CSV export** of a custom report was failing to complete and now exports normally. If your team gave up on exporting a custom report, try it again.
- **An export now matches the report it came from.** The file is built from the report itself rather than assembled out of the pages on screen, so every column you selected is in it — including columns your firm defined for its own workflow roles, which used to be dropped from the file without warning — and the report's filters and sort order are carried through. Rows beyond the page you are looking at are included. Exports work the same way on case, court notice, and payments reports. If your firm compared an export against the report on screen and found columns or rows missing, re-run it.

## Edge Cases & Limitations

- A custom report export covers up to **50,000 rows**. A report with more rows than that exports the first 50,000 — narrow the filters and export in batches if your firm needs the rest.
- A very large export can run out of time before the file is produced, in which case the export fails rather than returning a partial file. Filter the report down and run it again.

## Related Features

- [Custom Reports](./README.md)
- [Filters](./filters.md)
- [Payments Reports](./payments-reports.md)
- [Court Notices Report](../court-notices-report.md)
