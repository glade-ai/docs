# Bank Statements

## Overview

The Bank Statements Organizer collects a client's bank statements for a case. The client connects a bank account, and Glade retrieves the available statements from that account so your team can review them alongside the rest of the case. It is typically used in bankruptcy workflows where recent statements are part of the required financial documentation.

## Key Behaviors

### Connecting a Bank

- The client connects a bank account through the Bank Statements Organizer. Once the account is connected, Glade collects the statements available from it.
- Some banks require the client to sign in through the bank's own secure login screen. Consent to share statements is captured during that connection step, so statements load after the client finishes connecting. This applies to major banks that use a secure bank-login connection (for example, large national banks and brokerages).

### Viewing Statements

- Clients can open the Bank Statements Organizer directly from a workflow in the client portal to view the statements that have been collected.
- Firm staff view the same organizer from the dashboard or the client's case.

### Partial Retrieval

- If Glade cannot retrieve a particular statement, the bank stays connected and the statements that were retrieved are kept. A single statement that fails to load does not drop the whole bank connection or discard the statements already collected, so there is no need to reconnect the bank because of one missing statement.

## Configuration

> TODO: Document how a bank statements request is added to a workflow and any firm-level settings that control it.

## Edge Cases & Limitations

- Statements are limited to what the connected bank makes available for the requested period.

> TODO: Document the statement date range that is requested and how far back statements are collected.

## Related Features

- [Client Portal](./client-portal.md)
- [Credit Reports](./credit-reports.md)
- [Document Collection](../workflows/document-collection.md)
