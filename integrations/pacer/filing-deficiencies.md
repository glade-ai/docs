# Filing Deficiencies

## Overview

Sometimes a case is accepted by the court but one or more required documents are rejected and must be re-filed by hand in PACER — a "filed with deficiency" outcome. Glade surfaces this state persistently across the case so it is not missed after the live filing view is closed.

## Key Behaviors

- An **action-required banner** appears on the case listing the specific forms that still need to be filed manually in PACER. The banner stays visible until the deficiency is addressed, rather than appearing only while the submission is running.
- On the Case Status tab, the filing card shows a **Filed with deficiency** heading and a **View Submission** button that opens the submission details, so you can see exactly which documents were rejected.
- The status updates live — if a filing's status changes while you are viewing the case, the banner and the status card refresh without a manual reload.
- **One task per rejected document.** Glade creates a separate cure task for each document the court rejected, each titled after its own document, rather than a single task covering all of them. Your team can divide the work and see at a glance how many documents are still outstanding. See [Status Tracking](../../workflows/status-tracking/README.md) for how these tasks are assigned.
- **Completing a task clears that document.** After you file a rejected document by hand in PACER, mark its task complete and that document is cleared from the case's deficiency. The action-required banner narrows to the documents that remain and disappears once the last one is cleared. Previously the banner stayed up even after every document had been re-filed, and clearing it required contacting Glade.

> TODO: Confirm in production that completing a cure task clears the document from the banner. The court-integration side of this behavior was still pending when the change shipped, and a failure there is reported internally rather than shown to the user — so a banner that still lists an already-filed document should be raised with Glade.

## Related Features

- [PACER Integration](./README.md)
- [Filing progress](../efiling/filing-progress.md)
- [Status Tracking](../../workflows/status-tracking/README.md)
