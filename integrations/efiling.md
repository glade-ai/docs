# Electronic Court Filing (eFiling)

## Overview

Glade integrates with electronic court filing systems to let you submit cases directly from the platform. Your team submits filings through the case's eFiling modal, and Glade tracks the submission's progress in real time, sends inbox notifications when status changes occur, and links those notifications back to the relevant case view.

## Key Behaviors

- Initiating a filing submission from a case opens the eFiling submission modal, where you confirm and submit the filing.
- If the case's Schedule I (monthly income) exceeds Schedule J (monthly expenses), a **surplus warning** appears in the eFiling modal before you submit. This signals that the debtor's income exceeds their reported expenses, which may be relevant to the case outcome. You can review and address the discrepancy or proceed with the filing.
- Filing progress steps appear in the case immediately after submission — you do not need to refresh the page or wait for a background sync. Steps update as each stage of the filing lifecycle completes.
- If a filing fails partway through, the progress panel shows which step failed and the case returns to a retryable state. Retrying the filing starts a new submission attempt and replaces the previous attempt's progress.
- When a filing fails with an error that cannot be retried, a **Contact Support** button appears alongside the error message. Clicking it sends a pre-filled message to your Glade support conversation describing the district, error, and filing attempt. The support chat opens automatically so you can follow up with the Glade team immediately. The button changes to a "Support has been notified" state after the message is sent, and resets if you start a new filing attempt.
- Historical filing events are replayed when you navigate to a case, so the progress panel always reflects the full sequence of events even if you weren't viewing the case when they occurred.
- **Inbox notifications**: When a filing event occurs (such as a status update from the court), you receive a notification in the Glade inbox. Clicking the notification takes you directly to the Case Status tab for that case so you can review the current filing status without navigating manually.
- Direct links to a case opened via an inbox notification automatically open the Case Status tab.

### PDF flattening in filing packets

Court electronic filing systems (CM/ECF) reject PDFs that contain editable layers such as fillable form fields, annotations, or sticky notes. Client-uploaded documents — cover sheets, local forms, photo IDs, mortgage statements — frequently arrive as non-flat PDFs and would otherwise cause the court to reject the packet.

- When Glade compiles an eFiling packet, every PDF source in the packet is automatically **flattened** before the documents are merged. Form fields, comments, and annotations are baked into the page so the final packet meets CM/ECF requirements without manual intervention.
- Flattening is transparent — your team does not need to enable a setting or pre-process files. Uploads continue to behave the same way as before; the filing packet that goes to the court is what changes.
- If flattening fails on a particular file for any reason, Glade falls back to including the original file in the packet rather than blocking the filing. The filing proceeds and the failure is reported internally for follow-up.
- Glade-generated petition PDFs can also be flattened on output when the workflow that produced them requests it, so signature blocks and form fields render as a static page rather than as fillable form widgets.

### Required documents in the filing packet

Some documents are required by a district's rules and must not be dropped from the petition before filing. When you prepare a petition, any document the district marks as required is pre-checked and **locked** in the document list — it shows a **Required for filing** note and cannot be unchecked or removed, and range-selection skips over it. This prevents a required document from being left out by accident. For example, Florida Middle District Chapter 7 petitions require the Creditor Matrix and the Verification of Creditor Matrix, so both are locked into the packet. Other pre-checked documents that the district does not mark as required stay freely toggleable, so you can include or exclude them as needed.

### Image uploads in filing packets

Client-uploaded documents sometimes arrive as photos — for example, a phone picture of a signed Certificate of Credit Counseling saved as a JPEG or PNG. Court filing systems reject these when they reach the court as image data under a PDF name.

- When Glade compiles a filing packet, image files (JPEG and PNG) are automatically converted to a single-page PDF before the packet goes to the court, so a photographed document files successfully without your team re-scanning or re-saving it.
- Conversion is transparent — there is no setting to enable, and uploads continue to behave the same way. Only JPEG and PNG images are converted; other file types pass through unchanged.
- If conversion fails for a particular image, Glade falls back to including the original file rather than blocking the filing, and reports the failure internally for follow-up.

## Configuration

> TODO: Document any per-workflow or per-firm eFiling configuration options, such as enabling PACER submissions on a workflow template.

## Edge Cases & Limitations

- If you navigate away from a case mid-filing, the filing continues in the background. When you return, historical events are replayed so the progress panel is up to date.
- Cancelling a filing dismisses the progress panel and shows the filing in a cancelled state. The case can be re-filed if needed.
- The Contact Support button is only available for non-retryable errors. Errors that can be retried show the normal retry option instead. If a support conversation is not available for your account, the button does not appear and the error message is displayed as static text.

## Related Features

- [Workflows](../workflows/automation-rules.md) — workflows can include eFiling steps as part of an automated case sequence.
- [Status Tracking](../workflows/status-tracking.md) — the Case Status tab where eFiling notifications deep-link.

