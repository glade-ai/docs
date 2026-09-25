# Case Numbers

## Overview

When a filing succeeds, Glade records the court-assigned PACER case number on the workflow. This page covers where the case number is shown, how to record a case your firm filed outside Glade, and how case numbers behave when a matter carries more than one workflow.

## Key Behaviors

### Viewing the case number

- The assigned PACER case number is shown in the workflow header. Clicking the case number copies it to your clipboard, making it easy to paste into other tools or communications.
- For a case your firm filed outside Glade and then recorded in Glade, the **Filed at** date on the PACER case number panel is the court's actual filing date, which is usually earlier than the day someone entered the case. Your own team can now read that date back after entering it — it stays visible on the panel when you reload the case or come back to it another day. Previously only Glade staff could read the value, so the panel showed the date as unset to the firm even though it had been saved, and an attorney could re-enter the same date repeatedly without it ever appearing. Each firm sees only its own cases.

### Recording a case filed outside Glade

When a case is filed directly in PACER instead of through Glade, your team can register it against the workflow from the dashboard's case-status widget, so Glade tracks it alongside cases it filed itself.

- Enter the court-assigned case number to register the case. The registration is attributed to your firm, so the case appears in your firm's case-status views and reports next to cases filed through Glade. Previously a manually registered case was not attributed to the firm and could be missing from those reports.
- **Filed at date** — an optional date field records the date the court actually accepted the filing, which is often earlier than the day someone entered the case into Glade. After you save it, the date is shown read-only next to the case number.

### Case numbers when a case has more than one workflow

A single matter often carries several workflows — a retainer alongside a filing workflow, or a new workflow created when a case converts from one chapter to another. The court case number is recorded on the workflow the case was actually filed under, not on all of them.

- Every workflow in the group now **displays** the case number, taking it from whichever sibling holds one. Opening the retainer on a filed case shows the docket number instead of a blank field. Where more than one sibling carries a number, the most recently created one is shown.
- The case number is displayed, not copied. It still belongs to the workflow the case was filed under, which is what keeps incoming court notices attached to the right workflow.
- **Reports and filters that match on case number are unchanged.** They match the workflow that actually carries the number, so a report segmenting cases by whether a case number is present continues to count each matter once rather than once per workflow in the group.

## Related Features

- [PACER Integration](./README.md)
- [Case number matching](./court-notices/case-number-matching.md) — how court notices are linked to a case by its number.
- [Filing progress](../efiling/filing-progress.md)
- [Amending a filing](./amending-a-filing.md)
