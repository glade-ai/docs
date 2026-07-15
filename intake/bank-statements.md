# Bank Statements

## Overview

The Bank Statements Organizer collects a client's bank statements for a case. The client connects a bank account, and Glade retrieves the available statements from that account so your team can review them alongside the rest of the case. It is typically used in bankruptcy workflows where recent statements are part of the required financial documentation.

## Key Behaviors

### Connecting a Bank

- The client connects a bank account through the Bank Statements Organizer. Once the account is connected, Glade collects the statements available from it.
- Some banks require the client to sign in through the bank's own secure login screen. Consent to share statements is captured during that connection step, so statements load after the client finishes connecting. This applies to major banks that use a secure bank-login connection (for example, large national banks and brokerages).
- When a bank statements step is active on a client's case, a **Connect Bank Account** task appears in the client's portal home task list, alongside their other outstanding tasks. Opening the task takes the client straight to the Bank Statements Organizer. Previously the organizer was only reachable from within the workflow itself, so the step could be easy to miss on the home page. The task clears on its own once the client connects the account or the step is skipped.

### Viewing Statements

- Clients can open the Bank Statements Organizer directly from a workflow in the client portal to view the statements that have been collected.
- Firm staff view the same organizer from the dashboard or the client's case.

### Partial Retrieval

- If Glade cannot retrieve a particular statement, the bank stays connected and the statements that were retrieved are kept. A single statement that fails to load does not drop the whole bank connection or discard the statements already collected, so there is no need to reconnect the bank because of one missing statement.

### Connected Accounts Become Assets on the Case

On bankruptcy cases, connecting a bank does more than collect statements — each account that comes across is added to the case record as an asset, so the client's bank accounts populate the schedules automatically instead of being re-entered by hand. Previously only the statement PDFs reached the case, and the account details had to be typed into the schedules separately.

- One asset is created per connected account, carrying the account type (checking, savings, certificate of deposit, retirement, and so on), a description, the account's current balance as its value, the institution's name, and the account number.
- Because the accounts land in the case record, they flow through to the bankruptcy schedules (Schedule A/B), to questionnaires that draw on case data, and to the plan tools — the same places any other asset on the case appears.
- Reconnecting the same bank, or a later sync of the same account, updates the existing asset rather than adding a second copy of it.
- Credit cards and loans are not added as assets. Those are debts rather than property, and belong with the case's creditors.
- Accounts are only added on bankruptcy cases. Connecting a bank on any other kind of case collects statements as before and creates no assets.
- Account syncing and statement collection are independent. If one account cannot be read, the others are still added, and the statements are unaffected.

**A value that changes an existing answer is held for your review.** If a connected account's figure differs from something already recorded on the case — a balance a client entered on a questionnaire, a value your team typed in, or a figure taken from a credit report — the bank's version does not overwrite it. The difference is flagged for an attorney to accept or reject, so bank data never silently replaces an answer someone gave deliberately.

## Configuration

> TODO: Document how a bank statements request is added to a workflow and any firm-level settings that control it.

## Edge Cases & Limitations

- Statements are limited to what the connected bank makes available for the requested period.
- A bank connection that is not attached to a case collects statements but creates no assets — there is no case record to add them to.
- An account added from a connected bank and an account the client or your team entered by hand are not automatically recognized as the same account, so the same real account can appear twice on the schedules. Check the asset list for duplicates after a bank is connected, and merge or remove the extra entry before filing.

> TODO: Confirm how the account number is displayed on the resulting asset (in full, or masked to the last four digits).

> TODO: Document the statement date range that is requested and how far back statements are collected.

## Related Features

- [Client Portal](./client-portal.md)
- [Credit Reports](./credit-reports.md)
- [Document Collection](../workflows/document-collection.md)
