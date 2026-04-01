# Credit Reports

## Overview

Glade lets your team pull credit reports for clients as part of the intake process. Credit reports are typically used in bankruptcy workflows to review a client's credit profile before preparing filings. You initiate a pull from within the case, and Glade retrieves the report from the credit reporting service.

## Key Behaviors

### Pulling a Credit Report

- Credit report pulls are initiated from within a client's case or intake workflow.
- When you start a pull, Glade opens a modal to confirm the client's identity and consent before requesting the report.
- After confirming, Glade retrieves the report and displays it within the workflow.
- The action buttons in the modal are disabled while the request is in progress, preventing accidental duplicate submissions.

### Error Handling

If a credit report pull fails:

- An error modal appears explaining that the pull was unsuccessful.
- From the error modal you can:
  - **Retry**: Reopens the credit report purchase modal so you can attempt the pull again.
  - **Cancel**: Clears the error state and shows a skip option, letting you continue the intake flow without a credit report.
- Closing the error modal without taking an action preserves the error state. You can click the credit report card again later to bring the error modal back and choose what to do.

### Skip Option

If a credit report is not available or not needed, you can skip the step. The skip option appears after canceling an error, or may be available from the start depending on your workflow configuration.

## Configuration

| Setting | Description |
|---------|-------------|
| Pull attempt limit | Set in firm settings — limits the maximum number of credit report pull attempts per case. |

## Edge Cases & Limitations

- Credit report pulls are billed from the first pull at the standard rate. There is no trial or free pull before billing begins.
- The pull attempt limit is enforced per case. Once the limit is reached, no further pulls can be initiated for that case.

## Related Features

- [Client Portal](./client-portal.md)
- [Case Management](../back-office/case-management.md)
- [Settings](../back-office/settings.md)
