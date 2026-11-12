# Attorney Compensation Disclosure (Form 2030)

## Overview

Every PACER filing includes the attorney's compensation disclosure on Form 2030. This page covers where Glade takes the disclosed compensation amount from.

## Key Behaviors

The attorney compensation amount disclosed on Form 2030 comes from the attorney's answer on the case's Form 2030 (B2030) questionnaire. If that answer is blank, Glade uses the fee recorded in the case's billing details.

- **The B2030 answer comes first.** Glade uses the "agreed to accept" amount the attorney entered on Form 2030, so PACER receives the same figure printed on the disclosure. Before, Glade sent the billing figure first. That figure could include the court filing fee, so PACER sometimes got a higher number than the attorney disclosed (for example $1,938 instead of $1,600 when the extra $338 was the Chapter 7 filing fee).
- Glade reads the amount from whichever compensation question the case's Form 2030 actually uses. Firms use several versions of the form, and the answer may be a currency amount, typed text (including a formatted figure such as `1,600.00`), or a choice from a list. All of these are read correctly.
- **The case's billing details are the fallback.** If the B2030 answer is blank, not a readable amount, or negative, Glade uses the **amount the firm agreed to accept** from the case's billing details, which is worked out from the case's invoices.
- **Court filing fees are kept out of the billing figure.** Invoice lines named as filing fees ("Filing Fee", "eFiling Fee", "Refiling Fee" and similar) count as the court filing fee at any amount and are not treated as attorney pay. Lines named **Court Costs**, Court Cost, Court Fees, Filing Costs, or Initial Installment of Court Costs count as the filing fee only when the line total is exactly the standard court filing fee: **$338** for Chapter 7 or **$313** for Chapter 13. A Court Costs line at any other amount is treated as attorney pay. If an invoice has both an explicit filing-fee line and a Court Costs line, only the filing-fee line counts, so the fee is not subtracted twice.
- Lines that bundle attorney or legal fees with the filing fee (for example "Attorney Fees & Costs + Court Filing Fee", "Legal Services", "Attorneys' fees", "Attorney Costs") are treated as attorney pay. A line that only mentions an attorney, such as "Filing fee advanced by Attorney", still counts as a filing fee.
- A fee of **$0** (pro bono representation) is sent as zero, not treated as unanswered. A B2030 answer of $0 is sent as $0 even when the billing details show an amount.

## Edge Cases & Limitations

- If the Form 2030 question has not been answered (or the answer is not a readable amount) and the case has no recorded fee, the compensation figure is left unset. In districts that require it, this blocks the filing until the question is answered on the questionnaire or the fee is recorded on the case.
- The billing figure is recalculated the next time one of the case's invoices changes. A case whose invoices have not changed since these rules took effect may still hold an older figure.
- Installment payments toward the filing fee (for example $78 or $100) on a line named Court Costs are not counted as filing fees, because they do not equal the standard fee. Make sure the Form 2030 answer is filled in on these cases so PACER receives the right amount.
- A bundled attorney-fee-plus-filing-fee line is counted entirely as attorney pay. The court fee inside the bundle is not split out.

## Related Features

- [PACER Integration](./README.md)
- [Filing workflow](./filing-workflow.md)
- [Required fields check](../efiling/pre-filing-review/required-fields.md)
