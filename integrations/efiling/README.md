# Electronic Court Filing (eFiling)

## Overview

Glade integrates with electronic court filing systems to let you submit cases directly from the platform. Your team submits filings through the case's eFiling modal, and Glade tracks the submission's progress in real time, sends inbox notifications when status changes occur, and links those notifications back to the relevant case view.

The PACER connection itself, supported courts, the automated filing steps, and court notices are covered under [PACER Integration](../pacer/README.md).

## Key Behaviors

- Initiating a filing submission from a case opens the eFiling submission modal, where you confirm and submit the filing.
- If the case's Schedule I (monthly income) exceeds Schedule J (monthly expenses), a **surplus warning** appears in the eFiling modal before you submit. This signals that the debtor's income exceeds their reported expenses, which may be relevant to the case outcome. You can review and address the discrepancy or proceed with the filing.

## Topics

- [Filing packet](./filing-packet/README.md) — document types, required documents, adding documents, PDF and image conversion, and Chapter 13 plan status.
- [Pre-filing review](./pre-filing-review/README.md) — the automated blocking and advisory checks run before a petition can be submitted.
- [Why a filing is blocked](./blocked-filings.md) — how the eFiling modal explains a blocked filing, and the inline **Fix this** action for district setup.
- [Filing progress](./filing-progress.md) — progress steps, the progress panel, live preview, replays, paused filings, and inbox notifications.

## Configuration

> TODO: Document any per-workflow or per-firm eFiling configuration options, such as enabling PACER submissions on a workflow template.

## Related Features

- [PACER Integration](../pacer/README.md)
- [Workflows](../../workflows/automation-rules.md) — workflows can include eFiling steps as part of an automated case sequence.
- [Status Tracking](../../workflows/status-tracking/README.md) — the Case Status tab where eFiling notifications deep-link.
