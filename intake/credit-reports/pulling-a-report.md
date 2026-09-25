# Pulling a Credit Report

## Overview

Your team pulls a client's credit report from within the case or intake workflow. Glade confirms the client's identity and consent in a modal, retrieves the report from the credit reporting service, and saves the details you entered back to the client's profile and the case. On joint cases, Glade guards against mixed-up debtor details and lets you add a second debtor's report later without re-pulling the first.

## Key Behaviors

### Starting a pull

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

#### Date of birth carries into the case

The date of birth used for a credit report pull is written into the case's data, so questionnaires that ask for the debtor's date of birth are pre-filled with it instead of asking for it a second time.

- When the bureau's report includes a date of birth, that date is used — the one the bureaus report most often, if they differ — even if a different date was typed on the pull form.
- When the report has no date of birth, the date entered on the pull form is used.
- On a joint pull, the co-debtor's date of birth is carried into the case the same way.
- This applies whether the pull was started by your team or by the client.

Previously the date of birth entered for the pull was saved on the client's profile but never reached the case, so it had to be entered again in the questionnaire.

## Configuration

| Setting | Description |
|---------|-------------|
| Pull attempt limit | Set in firm settings — limits the maximum number of credit report pull attempts per case. |

## Edge Cases & Limitations

- Credit report pulls are billed from the first pull at the standard rate. There is no trial or free pull before billing begins.
- The pull attempt limit is enforced per case. Once the limit is reached, no further pulls can be initiated for that case.
- A report stored before the date of birth began carrying into the case gets its date of birth the next time the report is processed again, not straight away. On an older case, enter the date of birth in the questionnaire if it is still blank.

## Related Features

- [Credit Reports](./README.md)
- [When a Pull Fails](./pull-errors.md)
- [Pulling a Report Again](./pulling-again.md)
- [Importing Creditors from a Report](./importing-creditors.md)
- [Settings](../../back-office/settings.md)
