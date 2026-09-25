# Cross-Form Consistency Checks

## Overview

Some answers have to agree with each other across different forms in the petition package. Glade compares them and reports a contradiction while the questionnaire is being authored, rather than leaving it to be found at the court.

## Key Behaviors

The checks currently cover business and self-employment income, which has been the most common source of a self-contradicting petition — gig or business income picked up on **Schedule I line 8a** while the petition's own business question is left unanswered.

- **Business income reported without the sole-proprietor disclosure.** When Schedule I line 8a or **Form 122A-1 line 5** (gross receipts) reports business income, but petition **question 12** — *"Are you a sole proprietor of any full or part time business?"* — does not reflect it, the check flags the discrepancy.
- **Business income reported without a matching Statement of Financial Affairs answer.** When Schedule I line 8a reports business income but **SOFA question 27** does not, the check flags the discrepancy.
- **Findings point at the answer you need to change.** The sole-proprietor check reports against question 12 itself, so you are taken to the field that needs correcting rather than to a neighboring one.
- These findings are **blocking**, which means they raise the submit-anyway confirmation described under [Submitting with Incomplete Fields](../filling-out/submitting.md#submitting-with-incomplete-fields) rather than preventing submission outright. An attorney who has reviewed the discrepancy and is satisfied the answers are correct can still submit.

## Edge Cases & Limitations

- A further check comparing question 12 against **SOFA question 4** (business gross income) and **SOFA question 27** is built but not yet switched on. It is held back because the two questions cover different periods — question 12 asks about a business the debtor runs *now*, while question 27 looks back four years and question 4 covers the two prior calendar years. A debtor whose business closed before filing answers question 27 *Yes* and question 12 *No*, both correctly, and the check would interrupt them anyway.

> TODO: Confirm which petition questionnaire templates these checks are active on. They are turned on per template rather than across the board, so a firm may not see them on every petition questionnaire yet.

## Related Features

- [Questionnaires](../README.md)
- [Petition](./README.md)
- [Petition Check](./petition-check.md)
- [Validation Rules](../templates/validation-rules.md)
- [Schedule I and Income](../schedules/income.md)
