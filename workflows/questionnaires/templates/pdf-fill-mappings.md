# PDF Fill Mappings

## Overview

PDF fill mappings connect questionnaire fields to PDF template fields, enabling automatic generation of filled court forms and legal documents from questionnaire responses. This page covers how mappings work, supplemental forms Glade can generate, and how generated forms lay out and total their figures.

## Key Behaviors

- Individual fields connect to specific PDF fields, and each section can reference a PDF template.
- Dynamic PDF templates support generated PDFs with custom layouts and assets, going beyond simple field-to-field mapping.
- Generated forms paginate by content: a section that runs longer than a single page continues onto the next page. Previously a section was kept together as one block, so anything that no longer fit was pushed whole to the following page — leaving a large blank area at the bottom of the page before it. This was most visible on Schedule A/B, where the residence details plus a long property list pushed the entire section down a page.

### Supplemental and local court forms

Alongside the official bankruptcy forms, Glade can generate supplemental forms that a district requires or that support an answer on an official form. One is newly available:

- **Schedule I line 8a business statement** — the *Financial Review of the Debtor's Business* attachment that supports the business-income line on Schedule I. A section on the questionnaire collects each business's name, its gross receipts, and the twenty official expense lines; total expenses and net income are calculated for you. The generated attachment prints **one page per business**. The section appears only when Schedule I line 8a carries an amount for either debtor — including a business reporting a loss, since a negative figure on line 8a is still business income to disclose.

Three corrections to how that attachment is produced:

- **It stays in the petition packet.** The attachment is no longer dropped when the petition's documents are regenerated. Previously it was removed from the packet on every regeneration, so a firm that had filled the section in could compile the petition and find the statement gone, with nothing on screen to say why.
- **Only real businesses print.** Opening the section pre-renders a set of blank business rows, and every row with anything on it used to produce a page — two businesses could generate a twenty-four-page supplement, twenty-two pages of it near-blank. A row now reaches the attachment only when it has a business name or a gross amount on it.
- **The pages are numbered.** The footer continues the numbering of the form the attachment follows. Because Form 106I is two pages, the first business prints as page 3, the second as page 4, and so on.

These apply to documents generated from here on; re-generate the petition on a case prepared earlier to pick them up.

The Texas exemptions schedule is also generated as a supplemental form — see [Exemptions Calculator](../schedules/exemptions-calculator.md#texas-exemptions-schedule).

Both forms are added to your firm's questionnaire template by Glade rather than switched on in the template editor. Contact support if your firm files in these situations and does not see the section.

> TODO: Confirm which firms and templates these sections have been added to. They are rolled out per firm rather than to everyone at once.

### Totals on a form that prints whole-dollar amounts

Where your firm's petition prints amounts as whole dollars, a total on the generated form is added up from the rounded figures **printed on the lines above it**, so the column adds up as read. A total that was rounded separately from its own lines could be a dollar or two away from their sum, which is the kind of discrepancy a trustee queries.

This covers totals on the columns of a table as well as standalone totals. Schedule I is the case where it was reported: lines 5a–5e printed their rounded amounts, but line 6 showed the rounded exact sum rather than the sum of the printed lines, and line 7 was rounded independently again rather than carrying the corrected total.

- Only the printed total changes. The underlying answers, and the figures in the questionnaire, are unaffected.
- **Re-generate the petition** on a case prepared earlier to pick this up. Documents already generated keep the figures they were generated with.
- Firms whose petitions print exact amounts to the cent are unaffected.

## Edge Cases & Limitations

- Corrections to generated forms apply to documents generated from then on. Petitions already generated are not rebuilt; re-generate the petition to pick up a correction.

## Related Features

- [Questionnaires](../README.md)
- [Building Templates](./README.md)
- [Schedule A/B Property](../schedules/property.md) — line 17, line 19, and Part 3 printing
- [Schedule I and Income](../schedules/income.md)
- [Exemptions Calculator](../schedules/exemptions-calculator.md)
- [Generating a Draft Petition](../petition/draft-petition.md)
