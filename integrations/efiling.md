# Electronic Court Filing (eFiling)

## Overview

Glade integrates with electronic court filing systems to let you submit cases directly from the platform. Your team submits filings through the case's eFiling modal, and Glade tracks the submission's progress in real time, sends inbox notifications when status changes occur, and links those notifications back to the relevant case view.

## Key Behaviors

- Initiating a filing submission from a case opens the eFiling submission modal, where you confirm and submit the filing.
- Filing progress steps appear in the case immediately after submission — you do not need to refresh the page or wait for a background sync. Steps update as each stage of the filing lifecycle completes.
- If a filing fails partway through, the progress panel shows which step failed and the case returns to a retryable state. Retrying the filing starts a new submission attempt and replaces the previous attempt's progress.
- When a filing fails with an error that cannot be retried, a **Contact Support** button appears alongside the error message. Clicking it sends a pre-filled message to your Glade support conversation describing the district, error, and filing attempt. The support chat opens automatically so you can follow up with the Glade team immediately. The button changes to a "Support has been notified" state after the message is sent, and resets if you start a new filing attempt.
- Historical filing events are replayed when you navigate to a case, so the progress panel always reflects the full sequence of events even if you weren't viewing the case when they occurred.
- **Inbox notifications**: When a filing event occurs (such as a status update from the court), you receive a notification in the Glade inbox. Clicking the notification takes you directly to the Case Status tab for that case so you can review the current filing status without navigating manually.
- Direct links to a case opened via an inbox notification automatically open the Case Status tab.

## Configuration

> TODO: Document any per-workflow or per-firm eFiling configuration options, such as enabling PACER submissions on a workflow template.

## Edge Cases & Limitations

- If you navigate away from a case mid-filing, the filing continues in the background. When you return, historical events are replayed so the progress panel is up to date.
- Cancelling a filing dismisses the progress panel and shows the filing in a cancelled state. The case can be re-filed if needed.
- The Contact Support button is only available for non-retryable errors. Errors that can be retried show the normal retry option instead. If a support conversation is not available for your account, the button does not appear and the error message is displayed as static text.

## Related Features

- [Workflows](../workflows/automation-rules.md) — workflows can include eFiling steps as part of an automated case sequence.
- [Status Tracking](../workflows/status-tracking.md) — the Case Status tab where eFiling notifications deep-link.
