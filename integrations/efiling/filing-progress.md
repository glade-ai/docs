# Filing Progress

## Overview

After a filing is submitted, Glade tracks the submission's progress in real time: progress steps appear on the case, a progress panel follows you around the app, a live preview shows the court's site while the filing runs, and a recording is available afterwards. Glade sends inbox notifications when status changes occur and links them back to the case.

## Key Behaviors

### Progress steps on the case

- Filing progress steps appear in the case immediately after submission — you do not need to refresh the page or wait for a background sync. Steps update as each stage of the filing lifecycle completes.
- If a filing fails partway through, the progress panel shows which step failed and the case returns to a retryable state. Retrying the filing starts a new submission attempt and replaces the previous attempt's progress.
- When a filing fails with an error that cannot be retried, a **Contact Support** button appears alongside the error message. Clicking it sends a pre-filled message to your Glade support conversation describing the district, error, and filing attempt. The support chat opens automatically so you can follow up with the Glade team immediately. The button changes to a "Support has been notified" state after the message is sent, and resets if you start a new filing attempt.
- Historical filing events are replayed when you navigate to a case, so the progress panel always reflects the full sequence of events even if you weren't viewing the case when they occurred.

### Filing progress panel

A filing progress panel appears in the bottom-right corner of the screen when a PACER filing is running. It persists as you navigate to other pages — you do not need to stay on the filing tab to monitor progress.

- The panel is collapsed by default. The header shows the current step label, a progress count (e.g., "Uploading documents (3/6)"), and a spinner while the filing is in progress.
- Click the header to expand the panel and see the full step list, a **View filing** link that opens the case's status tab, and a dismiss button.
- When the filing completes, the header shows a green check and "Filing completed." When it fails, a red indicator and "Filing failed" appear.
- If you cancel a filing in progress, the header shows "Cancellation pending" until the cancellation is confirmed.
- Dismissing the panel hides it from view. The case's status tab continues to show full filing history.
- **Three failure reasons that used to show no detail now explain themselves.** A filing that stopped because the PACER login did not finish loading, because a required file was missing from the packet, or because the court site landed on a page Glade did not expect used to leave the progress detail empty and show only a generic "Case sync failed" message on the dashboard. Each of these now reports its own explanation, so your team can tell a court-site problem worth retrying from a packet problem it has to fix first. Other failure reasons were already explained and are unchanged.

### Watching a filing as it runs

While a PACER filing is in progress, the submission view shows a live preview of the court's site as Glade works through it, so your team can see what is happening on the far side rather than waiting on a status line.

- **The preview stays up for the whole run.** It appears once the filing reaches the court's site and remains until the filing finishes, however long that takes.
- **A captured screenshot replaces it.** When Glade captures an image at a step in the filing, that image is shown in place of the live preview.
- **It ends when the filing does.** On completion — succeeded, failed, or canceled — the live preview closes and the run is replaced by a recording of the session (see [Replaying a filing](#replaying-a-filing)); the case's status tab carries the outcome and the step history.
- For a period, the preview disappeared roughly ten seconds into every filing and the pane read **Live preview unavailable** for the rest of the run. That was a fault in how the preview decided it was finished, not a sign of a problem with the filing itself, and it no longer happens. Filings that ran during that period were submitted normally.

### Replaying a filing

While a filing is running, the filing view shows the court's site as Glade works through it. Once the filing finishes, that view is replaced by a **recording of the session**, so your team can play back what actually happened on the court's site — which pages were reached, what was entered, and where it stopped — instead of working from a single still image of the final screen.

- The recording covers the **most recent filing attempt** on the case. The still image of the last screen reached is still shown alongside it.
- **An attempt with no recording says so immediately.** Older attempts, and any attempt made without a recording, are reported as unrecorded as soon as the view opens. Previously these sat in a loading state for about two minutes before giving up, which read as a recording still being prepared when there was nothing to prepare.

> TODO: Confirm how long a filing recording stays available for playback, and whether a recording exists for attempts made before this was introduced.

### When a filing pauses and needs a person

Some filings stop part-way through on a page Glade cannot complete on its own and wait for someone to take over. The filing panel has always said so, but only while it was open on screen — so a filing could sit paused for hours because nobody happened to be looking at it.

- **Whoever started the filing gets an inbox notification** titled *Your PACER filing needs you*, so the pause reaches them anywhere in Glade rather than only inside the filing panel.
- The notification names the page the filing is waiting on where the court's system tells Glade which one it is, and otherwise reads as a general prompt to open the filing.
- Opening the notification takes you to the case so you can pick the filing up where it stopped.
- **One notification per pause.** A filing that pauses is announced once, however many times the signal is re-sent.
- The notification goes to the person who started the filing, not to the whole firm. If that person is away, someone else on the case can still take the filing over from the case itself — but nobody else is alerted.

### Status tracking

- Submission status values: in progress, succeeded, failed, or manual (attorney filed outside Glade).
- Each step of the filing process is logged with timestamps.
- Screenshots are captured at key steps for debugging failed submissions.
- Inbox notifications link directly to the case's status tab.

### Inbox notifications

- When a filing event occurs (such as a status update from the court), you receive a notification in the Glade inbox. Clicking the notification takes you directly to the Case Status tab for that case so you can review the current filing status without navigating manually.
- Direct links to a case opened via an inbox notification automatically open the Case Status tab.
- The email and inbox notifications sent when a filing succeeds or fails are listed under [Filing workflow](../pacer/filing-workflow.md#notifications).

## Edge Cases & Limitations

- If you navigate away from a case mid-filing, the filing continues in the background. When you return, historical events are replayed so the progress panel is up to date.
- Cancelling a filing dismisses the progress panel and shows the filing in a cancelled state. The case can be re-filed if needed.
- The Contact Support button is only available for non-retryable errors. Errors that can be retried show the normal retry option instead. If a support conversation is not available for your account, the button does not appear and the error message is displayed as static text.
- The live preview is a view of a filing in progress, not a record of it. Closing the page or navigating away ends the preview but does not affect the filing, which continues to run — reopen the case's status tab to see where it got to. Nothing from the preview is retained afterwards; only the captured screenshots and the step history remain.
- The notification about a paused filing goes only to the person who started it. Where a filing was started without a recorded initiator, no notification is sent and the pause is visible only in the filing panel.
- The notification is an alert, not the place the filing is taken over — open the case to continue it.

## Related Features

- [Electronic Court Filing (eFiling)](./README.md)
- [Filing workflow](../pacer/filing-workflow.md)
- [Filing deficiencies](../pacer/filing-deficiencies.md)
- [Case numbers](../pacer/case-numbers.md)
- [Status Tracking](../../workflows/status-tracking/README.md) — the Case Status tab where eFiling notifications deep-link.
