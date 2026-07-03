# Credit Reports

## Overview

Glade lets your team pull credit reports for clients as part of the intake process. Credit reports are typically used in bankruptcy workflows to review a client's credit profile before preparing filings. You initiate a pull from within the case, and Glade retrieves the report from the credit reporting service.

## Key Behaviors

### Pulling a Credit Report

- Credit report pulls are initiated from within a client's case or intake workflow.
- When you start a pull, Glade opens a modal to confirm the client's identity and consent before requesting the report.
- After confirming, Glade retrieves the report and displays it within the workflow.
- The action buttons in the modal are disabled while the request is in progress, preventing accidental duplicate submissions.
- All phone numbers you enter in the modal — including the client's mobile number and contact phone — are included in the request to the credit reporting service. If a bureau requires a phone number that the report previously failed to match against, having mobile and contact phone present alongside the primary number reduces "invalid borrower data" rejections.

### Joint Filing Safeguards

In a joint credit report pull, you enter the main debtor and the co-debtor on separate, visually similar steps, which makes it easy to accidentally enter one person's information for the other. Before the report is pulled, Glade compares the two dates of birth you entered. If they are identical, a confirmation appears naming each debtor (for example, "Main debtor and co-debtor have the same date of birth — is this correct?").

- Identical dates of birth can be legitimate (for example, twins), so this only asks you to confirm. You can confirm and continue, or go back to correct the entry.
- The check runs only on joint pulls. Single-debtor pulls are unaffected.

### Adding a Second Debtor to an Existing Pull

On a joint case, you can pull the second debtor's credit report after the first debtor's report has already come back — for example, when a spouse is added to the case later. When you do this, Glade pulls and bills for only the newly added debtor:

- A debtor whose report has already been pulled is skipped. Glade does not request their report from the credit bureau a second time, so there is no second hard inquiry on their credit file and no duplicate charge.
- Only the newly added debtor's report is pulled, and it is placed correctly as the secondary debtor so their information populates the right fields.
- Because pricing on a joint report differs from a single-debtor report, a firm that adds a second debtor after an initial single pull may want to review the invoice for the case to confirm the total is correct.

### Client Data Write-Through

When you fill in a client's information in the credit report modal — including name, address, date of birth, phone number, contact phone, and SSN — Glade automatically saves those fields back to the client's profile for any fields that are not already set. You only need to enter the information once: it is available in future credit report pulls and other workflows without re-entry. Contact phone is saved alongside the primary phone number so the client's profile reflects every number you entered in the modal, not just the first one.

- If any part of the client's address is already on file, the entire address block is left unchanged to avoid mixing data from different sources.
- Only empty fields are filled in. Existing values are never overwritten.
- If the write-through fails, the credit report pull still completes normally.

### Error Handling

If a credit report pull fails:

- An error modal appears explaining that the pull was unsuccessful.
- From the error modal you can:
  - **Retry**: Reopens the credit report purchase modal so you can attempt the pull again.
  - **Cancel**: Clears the error state and shows a skip option, letting you continue the intake flow without a credit report.
- Closing the error modal without taking an action preserves the error state. You can click the credit report card again later to bring the error modal back and choose what to do.

#### Specific failure messages

For common, known failure types Glade shows a specific, actionable message instead of a generic "pull failed" error, and stops retrying immediately so you see the result without waiting through repeat attempts:

- **Invalid firm credentials**: tells you that the credit reporting service rejected your firm's credentials and to update them in Settings before retrying.
- **Account locked**: tells you that your firm's account with the credit reporting service is locked and to contact their support before retrying.
- **Invalid borrower data**: tells you that the credit bureau rejected the borrower's information and to verify the client's name, address, SSN, and date of birth before retrying.
- **Access denied**: tells you that access was denied for this report and to contact support with the request ID shown in the message.

On a **joint pull**, each borrower's failure is reported separately, with its own specific reason and the borrower's name. When both the main debtor and co-debtor fail, you see what went wrong for each person — rather than a single generic message for only the first failure — so you can correct the right borrower's information before retrying. Each borrower's name is shown exactly as it was submitted to the credit bureau.

Unknown error codes are still retried automatically. When one bureau returns an error inside an otherwise-usable multi-bureau report, the pull is not retried — the partial report is preserved.

### Skip Option

If a credit report is not available or not needed, you can skip the step. The skip option appears after canceling an error, or may be available from the start depending on your workflow configuration.

### Imported real-estate addresses

When Glade imports addresses from a credit report into the case as real-estate assets, it imports only addresses the client actually owns. Glade uses the credit report's owner-match indicator on each address to make this determination, so prior addresses where the client lived but did not own the property are no longer imported as real-estate assets even if they have transaction history.

## Configuration

| Setting | Description |
|---------|-------------|
| Pull attempt limit | Set in firm settings — limits the maximum number of credit report pull attempts per case. |

## Edge Cases & Limitations

- Credit report pulls are billed from the first pull at the standard rate. There is no trial or free pull before billing begins.
- The pull attempt limit is enforced per case. Once the limit is reached, no further pulls can be initiated for that case.
- If a credit report is pulled successfully but the workflow's **Get Credit Report** step does not clear right away — for example, the report was retrieved but the finalizing step was interrupted by a timeout — Glade reconciles it automatically. Retrying the pull completes the existing report instead of pulling a new one, so you are not charged a second time, and a periodic background check completes any stranded report on its own (typically within about 15 minutes). You do not need to re-pull a report that already came back successfully.

## Related Features

- [Client Portal](./client-portal.md)
- [Case Management](../back-office/case-management.md)
- [Settings](../back-office/settings.md)
