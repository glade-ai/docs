# Workflow Labels

## Overview

Tags let anyone write whatever they like on a case, one per case. That makes them a good sticky note and a poor way to find anything: the same idea gets written five ways and none of them can be reported on. **Labels** are the controlled version — a list your firm agrees on once, then applies. A firm-managed set of labels can be applied to cases, several at a time. Labels are separate from tags and do not replace them.

## Key Behaviors

- **Your firm builds the list.** Each label has a title and a color. Every firm starts with an empty list and nothing is pre-filled, so labels do nothing until someone sets them up.
- **A case can carry several labels at once.** This is the main practical difference from tags, which remain one per case, freeform, and unchanged by this.
- **Some labels carry a date.** A label can be set up to ask for a date when it is applied — *Do not file before*, *Foreclosure*, and similar. The date belongs to that case's use of the label, so the same label carries a different date on every case. Labels not set up for a date do not ask for one.
- **Managing the list**: labels can be created, renamed, reordered, archived, and deleted. Archiving takes a label out of the picker without disturbing the cases already carrying it — the same way archiving a status works.
- **Titles are unique within your firm**, and creating or renaming a label to a title already in use is refused rather than producing two labels that read identically.
- **Finding cases by label**: the workflow list can be filtered by label — selecting several returns cases carrying any one of them — and sorted by label.

> TODO: Confirm where the label list is managed in Settings, where labels are applied to a case, and how labels are displayed in the workflow list alongside the existing Tags column.

## Configuration

- **Workflow labels**: Created and managed per firm. Each label has a title (unique within the firm) and a color, and can be set to ask for a date when it is applied. Labels can be reordered, archived, and deleted. No labels are created for you — every firm starts with an empty list and builds its own.

## Edge Cases & Limitations

- Labels and tags are separate. Existing tags are not converted into labels, and building a label list does not remove or change the tags already on your cases.
- A date can only be recorded against a label that was set up to accept one. Applying a date to any other label is refused, and the date has to be a real calendar date.
- A label is not a status and carries no behavior of its own — applying one does not move the case, complete tasks, or suppress follow-ups the way a custom status can.

## Related Features

- [Status Tracking](./README.md)
- [Workflow List](./workflow-list.md) — tags and the label filter
- [Custom Statuses](./custom-statuses.md)
