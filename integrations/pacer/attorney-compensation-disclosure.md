# Attorney Compensation Disclosure (Form 2030)

## Overview

Every PACER filing includes the attorney's compensation disclosure on Form 2030. This page covers where Glade takes the disclosed compensation amount from.

## Key Behaviors

The attorney compensation amount disclosed on Form 2030 is taken from the fee recorded on the case, and falls back to the case questionnaire when the case has no fee recorded.

- Glade uses the **amount the firm agreed to accept** from the case's billing details. This is the figure your team already enters when setting the case's fees, so the disclosure matches what the client was quoted without anyone re-keying it onto the questionnaire.
- If the case carries no agreed amount, Glade falls back to the compensation question on the questionnaire. It reads the amount from whichever compensation question the case's Form 2030 actually uses. Firms are on several versions of the form, and the answer may be a currency amount, typed text (including a formatted figure such as `1,600.00`), or a choice from a list — all of these are read correctly.
- The fallback previously had to find the answer on the same questionnaire the Form 2030 question belongs to. On most cases the fee is answered on a different questionnaire for that case, so the amount reached the court blank on the large majority of filings. Reading the case's recorded fee first closes that gap.
- A fee of **$0** — pro bono representation — is carried through as zero rather than treated as unanswered, from either source.

## Edge Cases & Limitations

- If the case has no recorded fee and the questionnaire question has not been answered (or the answer is not a readable amount), the compensation figure is left unset. In districts that require it, this blocks the filing until the fee is recorded on the case or the question is answered on the questionnaire.

## Related Features

- [PACER Integration](./README.md)
- [Filing workflow](./filing-workflow.md)
- [Required fields check](../efiling/pre-filing-review/required-fields.md)
