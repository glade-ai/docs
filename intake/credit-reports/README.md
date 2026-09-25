# Credit Reports

## Overview

Glade lets your team pull credit reports for clients as part of the intake process. Credit reports are typically used in bankruptcy workflows to review a client's credit profile before preparing filings. You initiate a pull from within the case, and Glade retrieves the report from the credit reporting service.

## Topics

- [Pulling a Credit Report](./pulling-a-report.md) — starting a pull, joint-filing safeguards, adding a second debtor later, and how entered client details are saved to the profile and case.
- [When a Pull Fails](./pull-errors.md) — the error modal, specific failure messages, the skip option, and automatic recovery of reports that were retrieved but not finalized.
- [Pulling a Report Again](./pulling-again.md) — re-pulling a named debtor after a security freeze, what a re-pull costs, and re-enrolling after a Chapter 7 to 13 conversion.
- [Importing Creditors from a Report](./importing-creditors.md) — how report accounts become creditors on the case: name formatting, original creditors on collection accounts, owned real estate, joint cases, and older reports.

## Configuration

| Setting | Description |
|---------|-------------|
| Pull attempt limit | Set in firm settings — limits the maximum number of credit report pull attempts per case. |

## Edge Cases & Limitations

- Credit report pulls are billed from the first pull at the standard rate. There is no trial or free pull before billing begins.
- The pull attempt limit is enforced per case. Once the limit is reached, no further pulls can be initiated for that case.

## Related Features

- [Client Portal](../client-portal/README.md)
- [Case Management](../../back-office/case-management.md)
- [Settings](../../back-office/settings.md)
