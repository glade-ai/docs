# PACER Integration

## Overview

Glade integrates with PACER (Public Access to Court Electronic Records) to automate bankruptcy case filing in federal courts. Firms connect their PACER credentials, and Glade handles the end-to-end filing process — uploading documents, navigating court-specific forms, paying filing fees, and reporting the assigned case number back to the firm. The filing runs asynchronously and typically completes in 7–10 minutes.

## Key Behaviors

### Connecting PACER credentials

- Firms provide their PACER account email and two-factor authentication key from the PACER integration settings.
- Credentials are stored encrypted and linked to the firm's account.
- PACER session tokens are cached to avoid repeated logins across filings.

### Supported courts

Glade currently supports automated filing in the following bankruptcy courts:

- Florida Middle (FLMB)
- Florida Northern (FLNB)
- Florida Southern (FLSB)
- Idaho (IDB)
- South Carolina (SCB)
- Washington Western (WAWB)

Courts not in this list are not available for automated filing.

### Filing workflow

1. An attorney initiates a filing from the case's eFiling modal, confirming the documents and court district.
2. Glade validates the filing packet — checks that required documents (petition, creditor matrix, pay advices, counseling certificates) are present and the chapter type is compatible.
3. A submission attempt is created with status "in progress."
4. The filing runs asynchronously via browser automation:
   - Logs into PACER with the firm's credentials and 2FA.
   - Uploads core case documents (debtor info, attorney information, petition, creditor matrix, pay advices).
   - Uploads supplemental documents based on chapter type — Chapter 7: income statements, means test; Chapter 13: repayment plan, income statements.
   - Submits credit counseling certificates and compensation disclosures.
   - Extracts the assigned case number from the court's confirmation screen.
   - Pays the filing fee via the firm's credit card on file with PACER.
5. On success, Glade records the case number and notifies the attorney via email and inbox notification with a link to the case.
6. On failure, the attorney receives a failure notification with error details and can retry from the case view.

### Filing packet document types

Each document in the filing packet must be labeled with the correct ECF document type. The document type dropdown in the filing packet lists named options for all commonly filed documents. Selecting the correct type ensures courts can identify each file — courts including FLMB and FLSB reject filings that contain unrecognized filenames.

- For **Chapter 7 business-debt cases** where the debtor is claiming exemption from the means test presumption of abuse, upload the B122A-1 Supplement and select **Statement of Debtor's Temporary Exclusion from Presumption of Abuse (B122A-1Supp)** from the document type dropdown. Filing this document labeled as "Other" causes a submission failure.
- Use a named document type whenever one exists in the dropdown. The generic "Other" option is for documents that do not match any named type.

### Filing Packet AI Review

Before a filing is submitted, Glade automatically reviews each document in the filing packet and flags issues that could cause the court to reject the filing.

- Each document row in the filing packet shows a status badge indicating the AI review result. The badge combines a Glade AI icon with a status indicator.
- Available review statuses:
  - **Evaluating** — AI review is in progress.
  - **Approved** — Glade AI found no issues with the document.
  - **Needs Review** — Glade AI flagged potential issues. Click the document to see a summary and a checklist of specific concerns.
  - **Failed** — The review process encountered an error and could not complete.
  - **Approved by Reviewer** — A team member has manually approved the document after reviewing it.
- All document rows show a three-dot actions menu, including rows for documents that have not yet been uploaded. The **Remove** option is disabled on rows with no document attached.
- Clicking a document opens a **Document Review Status** panel above the document preview. Click the panel header to expand or collapse it. The panel shows the document's status, an AI-generated summary with flagged issues listed as bullet points, and a checklist of validation items.
- On documents with a **Needs Review** status, an **Approve Document** button lets a team member manually mark the document as approved after reviewing the flagged items.
- Review results update in real time — when the AI finishes reviewing a document, the badge and review panel update automatically without requiring a page refresh.
- To trigger AI review for a document that was uploaded before the review feature was active, open the document's three-dot options menu and select **Review by Glade AI**. The document transitions to **Evaluating** and then updates to its review result.

### Customizing AI Review Instructions

Law firms can customize the review instructions the AI uses when checking filing documents. From your dashboard, navigate to **Filing Packet AI Review Configs** to open the configuration page.

The page lists all supported document types. For each type you can:

- **Override** the default instructions — your text replaces the defaults entirely.
- **Append** additional instructions — your text is added after the defaults.

Rows with active customizations are tagged **Customized**. Click the clear button on a row to remove the customization and revert that document type to the default instructions.

An info banner on the configuration page explains the difference between override and append behavior.

### Filing fees

- PACER charges a filing fee per case, determined by court and chapter type.
- Glade submits payment through PACER's credit card interface during the filing process.
- Payment is retried up to 3 times if the initial attempt fails.
- The transaction number from PACER is recorded on the submission.

### Filing progress panel

A filing progress panel appears in the bottom-right corner of the screen when a PACER filing is running. It persists as you navigate to other pages — you do not need to stay on the filing tab to monitor progress.

- The panel is collapsed by default. The header shows the current step label, a progress count (e.g., "Uploading documents (3/6)"), and a spinner while the filing is in progress.
- Click the header to expand the panel and see the full step list, a **View filing** link that opens the case's status tab, and a dismiss button.
- When the filing completes, the header shows a green check and "Filing completed." When it fails, a red indicator and "Filing failed" appear.
- If you cancel a filing in progress, the header shows "Cancellation pending" until the cancellation is confirmed.
- Dismissing the panel hides it from view. The case's status tab continues to show full filing history.

### Status tracking

- Submission status values: in progress, succeeded, failed, or manual (attorney filed outside Glade).
- Each step of the filing process is logged with timestamps.
- Screenshots are captured at key steps for debugging failed submissions.
- Inbox notifications link directly to the case's status tab.
- The assigned PACER case number is shown in the workflow header. Clicking the case number copies it to your clipboard, making it easy to paste into other tools or communications.

### Case transfers

When a bankruptcy case is transferred to a different court and assigned a new case number, PACER sends electronic notices to the new case number. Glade automatically associates those incoming notices with the original workflow, so your case activity timeline stays complete without manual re-linking. The association is based on the transfer notice in the PACER email, which identifies the originating case number.

### Preventing duplicate filings

Before a filing proceeds, Glade checks whether the case already has an assigned case number or an in-progress filing. Depending on the situation, you will see one of two states in the pre-filing dialog:

- **Hard block** — If a case number already exists, or if a filing is actively in progress for the case, the dialog shows only a **Go Back** button. You cannot proceed until the existing filing resolves. A red alert banner in the eFiling modal also shows the blocking reason.
- **Soft warning** — If a recent filing attempt exists but does not meet the hard-block conditions, you can review the details and continue by checking an acknowledgment checkbox and clicking **Continue Anyway**.

At the moment you click the final submit button, Glade performs a fresh check. If the status has changed to a hard-block condition while the dialog was open, the submission is blocked and you will see a toast and an updated alert banner.

### Compiling selected documents for amendments

When filing an amendment, you can select a subset of the case's documents and download them as a single merged PDF — without downloading all documents or individual files.

1. Open the Case Documents pane (press **D** while viewing the case).
2. Check the boxes next to the documents you want to include. You can select across multiple document categories.
3. The footer button changes to **Download N selected as PDF**, where N is your selection count.
4. Click it to open the compile modal. Enter a custom filename and drag to reorder documents if needed.
5. Click **Compile and Download PDF** to download the merged file.

Deselecting all documents returns the footer to the standard download options. Your selection clears automatically when you close the documents pane.

### Notifications

| Event | Email | Inbox |
|-------|-------|-------|
| Filing succeeded | Case number and client name | Link to case status tab |
| Filing failed | Error summary | Link to case for retry |

## Configuration

| Setting | Description |
|---------|-------------|
| PACER credentials | Email and 2FA key, entered in integration settings |
| Court district | Selected per filing from the case's eFiling modal |
| Test environment | Submissions can be routed to PACER's test system for QA |

## Edge Cases & Limitations

- Only bankruptcy cases (Chapters 7 and 13) are supported. Other case types (civil, criminal, appellate) are not available.
- Filing requires a complete document packet — missing required documents cause the submission to fail.
- Courts outside the supported list cannot be filed to through Glade.
- Filing is asynchronous and takes 7–10 minutes. The attorney does not need to keep the page open.
- If the PACER session token expires mid-filing, the submission fails and can be retried.
- PACER passwords are not stored — they are passed only at filing time. The 2FA key is stored encrypted.
- If a filing partially succeeds (some documents uploaded but fee payment fails), the submission is marked as failed. The attorney may need to complete the filing manually in PACER.
- Once a case number is assigned, Glade hard-blocks any further automated filing attempts for that case. To file again (e.g., for an amended petition), contact support or file directly in PACER.
- Reconnecting after a credential change requires re-entering the 2FA key.

## Related Features

- [Electronic Court Filing (eFiling)](./efiling.md)
- [Workflows](../workflows/automation-rules.md)
- [USCIS Integration](./uscis.md)
