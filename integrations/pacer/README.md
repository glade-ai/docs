# PACER Integration

## Overview

Glade integrates with PACER (Public Access to Court Electronic Records) to automate bankruptcy case filing in federal courts. Firms connect their PACER credentials, and Glade handles the end-to-end filing process — uploading documents, navigating court-specific forms, paying filing fees, and reporting the assigned case number back to the firm. The filing runs asynchronously and typically completes in 7–10 minutes.

Preparing the filing packet, the pre-filing review, and watching a filing as it runs are covered under [Electronic Court Filing (eFiling)](../efiling/README.md).

## Topics

- [Connecting PACER](./connecting-pacer.md) — entering PACER credentials, and what a "PACER login failed" message means.
- [Supported courts](./supported-courts.md) — the bankruptcy courts and chapters Glade can file in.
- [Filing workflow](./filing-workflow.md) — the steps of an automated filing, filing fees, and success/failure notifications.
- [Case upload files](./case-upload-files.md) — when the debtor, creditor, and Creditor Matrix files are built, and how negative amounts are caught.
- [Attorney compensation disclosure (Form 2030)](./attorney-compensation-disclosure.md) — where the disclosed fee comes from.
- [Chapter handling](./chapter-handling.md) — switching chapter at compile time, matters with both a Chapter 7 and Chapter 13 workflow, and the Chapter 7 presumption-of-abuse page.
- [South Carolina DeBN elections](./south-carolina-debn.md) — how SCB Chapter 7 electronic-noticing elections are read and filed.
- [Filing deficiencies](./filing-deficiencies.md) — cases accepted with rejected documents that must be re-filed by hand.
- [Case numbers](./case-numbers.md) — viewing the case number, recording a case filed outside Glade, and case numbers across several workflows.
- [Amending a filing](./amending-a-filing.md) — compiling selected documents for an amendment.
- [Court notices](./court-notices/README.md) — the notice address, hearings and 341 meetings, case number matching, and proofs of claim.

## Configuration

| Setting | Description |
|---------|-------------|
| PACER credentials | Email and 2FA key, entered in integration settings |
| Court district | Selected per filing from the case's eFiling modal |
| Test environment | Submissions can be routed to PACER's test system for QA |

## Edge Cases & Limitations

- Only bankruptcy cases (Chapters 7 and 13) are supported. Other case types (civil, criminal, appellate) are not available.
- Courts outside the supported list cannot be filed to through Glade.
- Filing is asynchronous and takes 7–10 minutes. The attorney does not need to keep the page open.

## Related Features

- [Electronic Court Filing (eFiling)](../efiling/README.md)
- [Workflows](../../workflows/automation-rules.md)
- [USCIS Integration](../uscis.md)
