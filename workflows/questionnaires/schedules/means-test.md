# Means Test

## Overview

The means test forms — Form 122A-1 and 122A-2 for Chapter 7, Form 122C-1 and 122C-2 for Chapter 13 — are filled largely by autofills drawing on the Income Organizer, the Master Creditor List, and IRS and Census reference data. This page covers how non-consumer Chapter 7 cases are handled and how secured debt deductions are carried onto the forms.

## Key Behaviors

### Non-Consumer Chapter 7 Means Test

Some Chapter 7 cases are non-consumer debt cases — the debtor's debts are primarily business rather than consumer in nature. Those cases follow the "no presumption of abuse" branch of Form B122A-1 (line 14a) and never need Form B122A-2 (the full means test calculation).

When the client's questionnaire indicates the case is non-consumer Chapter 7, Glade handles the means test paperwork automatically:

- The Form B122A-1 "no presumption" answer is filled in for the client. No manual entry is needed.
- The B122A-2 means test answers are skipped. Auto-fills that would have populated B122A-2 fields are blocked, so your team does not have to wipe them before filing.
- The B122A-2 PDF is not generated for the case, and any previously generated copy is removed from the case documents. Form B122A-1 (and the B122A-1 Supplement, where the district requires it) continue to be generated.

If a case was set up before this automation rolled out, your firm can request a one-time cleanup of existing non-consumer Chapter 7 cases — contact Glade support to coordinate.

### Secured Debt Deductions on the Means Test

The autofills that carry secured debts onto the means test forms — mortgages, vehicles, and other secured debts on Form 122A-2 (Chapter 7) and Form 122C-2 (Chapter 13) — read the case's Master Creditor List and only bring across creditors that are actually being filed:

- Creditors marked as omitted from the petition, creditors that have been removed, and the hidden duplicate entries grouped under another creditor are left out. Previously these were copied onto the form, so zeroed-out accounts and credit-report duplicates appeared as separate deduction rows that had to be deleted by hand.
- Where a creditor has no linked property, the property description entered on the creditor itself is used, so the collateral column is filled rather than left blank.
- **Arrearage cure amounts** can be populated on line 34 of Forms 122A-2 and 122C-2 from the arrearages recorded on the Master Creditor List. Each active creditor with an arrearage above zero produces one row carrying the creditor name, the secured property, and the total cure amount. Creditors with a zero arrearage, and creditors excluded as above, produce no row.
- The **monthly cure amount** on that line is not set by this autofill — it continues to be calculated from the total cure amount, so re-running the autofill does not disturb it.

### Related means test behavior elsewhere

- IRS standard deduction amounts and median income populate from reference data on open — see [Autofills From Reference Data](../autofills/how-autofills-work.md#autofills-from-reference-data).
- Current monthly income and long-form deduction lines name their calculator as the source and keep hand overrides — see [Manual Overrides](../autofills/manual-overrides.md#overriding-a-schedule-i-or-means-test-figure-the-calculator-produced).
- The **means test summary** field is a read-only display field — see [Fields, Lists, and Tables](../templates/fields-and-tables.md#fields).
- Means test lookups are selected by filing district — see [The Filing District an Agent Works Out](../autofills/ai-agents.md#the-filing-district-an-agent-works-out).

## Edge Cases & Limitations

- Cases set up before the non-consumer automation rolled out need a one-time cleanup requested through Glade support.

## Related Features

- [Questionnaires](../README.md)
- [Schedule Tools](./README.md)
- [Schedule I and Income](./income.md)
- [Creditors](./creditors.md)
- [How Autofills Work](../autofills/how-autofills-work.md)
- [Income Organizer](../../income-organizer/README.md)
