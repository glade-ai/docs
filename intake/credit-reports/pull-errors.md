# When a Pull Fails

## Overview

When a credit report pull fails, Glade shows an error modal that lets you retry or skip the step, and — for common, known failure types — a specific message explaining what to fix. This page also covers the skip option and how Glade recovers a report that was retrieved successfully but never finalized.

## Key Behaviors

### Error Handling

If a credit report pull fails:

- An error modal appears explaining that the pull was unsuccessful.
- From the error modal you can:
  - **Retry**: Reopens the credit report purchase modal so you can attempt the pull again.
  - **Cancel**: Clears the error state and shows a skip option, letting you continue the intake flow without a credit report.
- Closing the error modal without taking an action preserves the error state. You can click the credit report card again later to bring the error modal back and choose what to do.

### Specific failure messages

For common, known failure types Glade shows a specific, actionable message instead of a generic "pull failed" error, and stops retrying immediately so you see the result without waiting through repeat attempts:

- **Invalid firm credentials**: tells you that the credit reporting service rejected your firm's credentials and to update them in Settings before retrying.
- **Account locked**: tells you that your firm's account with the credit reporting service is locked and to contact their support before retrying.
- **Invalid borrower data**: tells you that the credit bureau rejected the borrower's information and to verify the client's name, address, SSN, and date of birth before retrying.
  - A state written out in full — `Georgia` rather than `GA` — is no longer one of the causes. Glade converts the state to its two-letter abbreviation before sending the request, so a client record holding the full name pulls normally. This applies wherever the pull is started from, including older intake screens and cases whose address was recorded long before the pull. A state that is not a real US state or territory is still rejected, and the message names the value that could not be read.
- **Access denied**: tells you that access was denied for this report and to contact support with the request ID shown in the message.

On a **joint pull**, each borrower's failure is reported separately, with its own specific reason and the borrower's name. When both the main debtor and co-debtor fail, you see what went wrong for each person — rather than a single generic message for only the first failure — so you can correct the right borrower's information before retrying. Each borrower's name is shown exactly as it was submitted to the credit bureau.

Unknown error codes are still retried automatically. When one bureau returns an error inside an otherwise-usable multi-bureau report, the pull is not retried — the partial report is preserved.

### Skip Option

If a credit report is not available or not needed, you can skip the step. The skip option appears after canceling an error, or may be available from the start depending on your workflow configuration.

### Reports retrieved but not finalized

If a credit report is pulled successfully but the workflow's **Get Credit Report** step does not clear right away — for example, the report was retrieved but the finalizing step was interrupted by a timeout — Glade reconciles it automatically. Retrying the pull completes the existing report instead of pulling a new one, so you are not charged a second time, and a periodic background check completes any stranded report on its own (typically within about 15 minutes). You do not need to re-pull a report that already came back successfully.

## Edge Cases & Limitations

- The pull attempt limit is enforced per case. Once the limit is reached, no further pulls can be initiated for that case.

## Related Features

- [Credit Reports](./README.md)
- [Pulling a Credit Report](./pulling-a-report.md)
- [Pulling a Report Again](./pulling-again.md)
- [Settings](../../back-office/settings.md)
