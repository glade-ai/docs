# Filing Workflow

## Overview

Once an attorney initiates a filing, Glade runs the end-to-end PACER filing process asynchronously — uploading documents, navigating court-specific forms, paying filing fees, and reporting the assigned case number back to the firm. The filing typically completes in 7–10 minutes.

## Key Behaviors

### Filing steps

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

### Filing fees

- PACER charges a filing fee per case, determined by court and chapter type.
- Glade submits payment through PACER's credit card interface during the filing process.
- Payment is retried up to 3 times if the initial attempt fails.
- The transaction number from PACER is recorded on the submission.

### Notifications

| Event | Email | Inbox |
|-------|-------|-------|
| Filing succeeded | Case number and client name | Link to case status tab |
| Filing failed | Error summary | Link to case for retry |

## Configuration

| Setting | Description |
|---------|-------------|
| Court district | Selected per filing from the case's eFiling modal |
| Test environment | Submissions can be routed to PACER's test system for QA |

## Edge Cases & Limitations

- Filing requires a complete document packet — missing required documents cause the submission to fail.
- Filing is asynchronous and takes 7–10 minutes. The attorney does not need to keep the page open.
- If a filing partially succeeds (some documents uploaded but fee payment fails), the submission is marked as failed. The attorney may need to complete the filing manually in PACER.

## Related Features

- [PACER Integration](./README.md)
- [Connecting PACER](./connecting-pacer.md)
- [Case upload files](./case-upload-files.md)
- [Filing progress](../efiling/filing-progress.md) — watching a filing as it runs and reading its outcome.
- [Pre-filing review](../efiling/pre-filing-review/README.md)
- [Filing deficiencies](./filing-deficiencies.md)
