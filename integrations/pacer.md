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
   - Uploads supplemental documents based on chapter type — Chapter 7: income statements, means test; Chapter 13: repayment plan, income statements. For Chapter 7 business-debt cases claiming an exemption from the means test presumption of abuse, the **Statement of Debtor's Temporary Exclusion from Presumption of Abuse (B122A-1Supp)** is available as a document type in the ECF document filename dropdown and is uploaded as part of the supplemental documents.
   - Submits credit counseling certificates and compensation disclosures.
   - Extracts the assigned case number from the court's confirmation screen.
   - Pays the filing fee via the firm's credit card on file with PACER.
5. On success, Glade records the case number and notifies the attorney via email and inbox notification with a link to the case.
6. On failure, the attorney receives a failure notification with error details and can retry from the case view.

### Filing packet document types

Each document in the filing packet must be labeled with the correct ECF document type. The document type dropdown in the filing packet lists named options for all commonly filed documents. Selecting the correct type ensures courts can identify each file — courts including FLMB and FLSB reject filings that contain unrecognized filenames.

- For **Chapter 7 business-debt cases** where the debtor is claiming exemption from the means test presumption of abuse, upload the B122A-1 Supplement and select **Statement of Debtor's Temporary Exclusion from Presumption of Abuse (B122A-1Supp)** from the document type dropdown. This is supported for all available districts. Filing this document labeled as "Other" causes a submission failure.
- When a court requires individual debtor identification documents, select **PhotoID (Debtor 1)** or **PhotoID (Debtor 2)** for each debtor's photo identification, and **DeBN (Debtor 1)** or **DeBN (Debtor 2)** for each debtor's Declaration of Electronic Notice. The Debtor 1 variant is for the primary debtor; the Debtor 2 variant is for the co-debtor in a joint case.
- For **Western District of Pennsylvania (PAWB)** Chapter 7 cases, **Local Form 1 — Declaration Re: Electronic Filing of Petition, Schedules & Statements** is available in the document type dropdown. This form is submitted through the EDSS portal alongside the SSN Statement — it is not part of the standard ECF filing packet. A Local Form 1 slot appears in the per-district document checklist for PAWB Chapter 7 workflows once the document is labeled and uploaded.
- For **Florida Southern (FLSB)** Chapter 13 cases, **Local Form 67 — Certification of Compliance** is available in the document type dropdown. The form auto-surfaces in the FLSB Chapter 13 required-document checklist, and ad-hoc uploads from the case documents picker are accepted under common filename variants (with or without spaces, hyphens, underscores, or the full form name).
- For **Ohio Southern (OHSB)** Chapter 7 joint-debtor filings, **Statement 1015-2 — Joint Debtor Compliance (OHSB)** is available in the document type dropdown for the Joint Debtor Compliance Statement form (Statement 1015-2 with No Prior). Label the uploaded form with this document type so it is recognized at filing time — uploading it as **Other** prevents the OHSB filing engine from picking it up.
- Glade also accepts non-canonical filename variants for **Verification of Creditor Matrix** uploads, so files named with run-together or otherwise normalized variants pass the filing packet's filename check instead of being rejected.
- Use a named document type whenever one exists in the dropdown. The generic "Other" option is for documents that do not match any named type.
- When you assign a custom filename to a document being added to PACER, Glade now preserves spaces, hyphens, parentheses, periods, plus signs, apostrophes, and accented letters in the filename. Filenames such as `Pay Advices`, `Tax Return 2024`, and `Photo ID (Debtor 1)` flow through to PACER as typed instead of being collapsed into a single run-on word. Only characters that filesystems or PACER cannot accept (such as path separators and control characters) are removed.
- Filenames that contain only special characters and would resolve to an empty name are rejected at the form before they can be saved, so you see the validation message immediately rather than encountering a runtime error during filing.

### Filing Packet AI Review

Filing Packet AI Review is currently turned off. Filing packet uploads no longer trigger an automated AI review, the document review status panel and review badges have been removed from the PACER preview pane, and the Filing Packet AI Review configuration page is no longer in use. The feature is paused while the review experience is reworked.

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

### 341 meeting notices

Glade processes incoming court notices about 341 meetings (meetings of creditors) and displays the name of the trustee who will conduct the meeting.

- When a 341 meeting notice identifies the conducting trustee by name — for example, via a video or phone conference format — Glade shows that person as the trustee for the meeting.
- The conducting trustee may differ from the case trustee listed elsewhere in the notice. Glade prioritizes the person actually conducting the meeting, not other named parties such as case-party trustees.

### South Carolina (SCB) Chapter 7 individual filings

- Individual Chapter 7 cases filed in the South Carolina Bankruptcy Court collect an additional questionnaire question about the local DeBN form: clients answer **Activate** or **Decline** for the Debtor's Election Re: Electronic Noticing. The answer is passed through to PACER so the SCB filing engine fills the right radio on the local form.
- The question is shown only on Chapter 7 individual filings (it is hidden on joint petitions and on non-Chapter 7 filings) and is labeled to indicate it applies only to South Carolina filings — clients in other districts can ignore it.
- If the question is left unanswered on a SCB Chapter 7 individual filing, the answer is omitted from the PACER submission. The SCB filing engine treats the missing answer as a configuration gap and surfaces it as a filing error.

### Chapter 7 individual presumption-of-abuse page

When a Chapter 7 individual case explicitly indicates "no presumption" on B122A-1 line 14, Glade now fills the matching presumption fields on B122A-1 lines 40 and 42 with that same answer instead of leaving them blank. Because the lines are populated, PACER no longer renders the standalone "Presumption of Abuse" page during filing — the filing proceeds without that extra interstitial. Other income and expense fields wiped by the no-presumption answer continue to be cleared as before. The override applies only to Chapter 7 filings; cases on other chapters that carry stale prior answers from an earlier Chapter 7 session are not affected.

### Case transfers

When a bankruptcy case is transferred to a different court and assigned a new case number, PACER sends electronic notices to the new case number. Glade automatically associates those incoming notices with the original workflow, so your case activity timeline stays complete without manual re-linking. The association is based on the transfer notice in the PACER email, which identifies the originating case number.

### Required fields check before filing

Before a filing can be submitted, Glade validates that all required debtor fields are present. If any are missing, the filing is blocked at both the pre-filing preview and the ECF submission modal, and the missing fields are listed by name so your team can address them before re-attempting.

- For individual Chapter 7 and Chapter 13 filings, the **credit counseling completion date** is required. If it is missing from the case questionnaire, the eFiling modal shows a warning listing the missing fields.
- For joint filings with two debtors, both the primary and co-debtor credit counseling completion dates must be present.
- For individual Chapter 7 filings, the **marital filing status** is also required. Submission is blocked if the answer is missing from the questionnaire, and the missing field is named in the eFiling error so the team can fill it before retrying. For joint Chapter 7 filings, when the questionnaire indicates the petition is filed jointly but the marital filing status answer was not provided, Glade infers "Married, filing jointly" automatically — joint Chapter 7 filings no longer fail because of an unanswered marital status question.
- Glade checks these fields in the questionnaire data — if the information has been collected but not yet saved, save the questionnaire before initiating the filing.
- Missing fields are shown with labels — for example, "Credit counseling completion date (Debtor 1)" — so you can identify exactly what needs to be filled in. An **Open questionnaire** link in the error state takes you directly to the case questionnaire.
- If a filing attempt fails because required fields are still missing at the point of submission, the eFiling modal names the specific missing fields so your team knows exactly what to complete before retrying.

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
