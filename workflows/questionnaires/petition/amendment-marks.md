# Amendment Marks

## Overview

When a case's schedules are amended, some courts expect the amended forms to show what changed: answers that were removed are struck through, and answers that were added or changed are emphasized, so the court and the trustee can see the changes without comparing two versions side by side. Firm staff mark these answers on the Bankruptcy Schedules questionnaire, and the marks print on the generated petition forms. A mark can be put on a whole list row, a single answer, or one cell of a list or table row.

## Key Behaviors

### The two marks

| Mark | Prints as | Effect on totals |
|------|-----------|------------------|
| **Removed** | Struck through | The answer is left out of the totals that read it. |
| **Added** | Bold, italic, and underlined | None — the answer counts as usual. |

A mark can be cleared, which returns the answer to normal printing and, for a removed answer, puts it back into the totals.

### What can be marked

- **A whole list row**, such as a creditor or a property.
- **A single answer**, such as a Schedule J expense line.
- **One cell of a list or table row**, such as one debtor's figure on a Schedule I income line, leaving the other debtor's figure unmarked.
- Single answers and cells are marked from the **Amend this answer** menu on the field. Calculated fields, such as totals, have the menu too.
- Only firm staff can add or clear marks. Clients cannot.

### A struck answer keeps its value

Striking an answer does not delete it. The answer keeps its value and prints with a line through it, so the amended form shows what was there before.

- **Totals that read a struck answer recalculate without it.** Striking a $1,600 rent line on Schedule J lowers the Schedule J totals by $1,600, and striking a Debtor 1 overtime figure on Schedule I lowers that debtor's gross income and every total that follows from it, including the Schedule J figures that read Schedule I. Clearing the mark restores the totals.
- **Striking a calculated field is print-only.** A struck total prints struck through, but the figures that read it are not changed, so striking a total never zeroes what depends on it.
- **Recalculated totals are not marked automatically.** When a struck answer changes a total, the total is not marked as changed on its own. Mark it by hand from its own **Amend this answer** menu if the court expects it.
- **Show-and-hide rules still read the struck value.** A struck "Yes" does not hide the questions that follow it, so the struck answer and its details still print.
- The **Petition Check** does not flag a total for disagreeing with its inputs because one of them is struck.
- AI agents that read the questionnaire treat a struck answer as unanswered.
- The statistical figures sent with the electronic filing leave out struck answers and struck cells — for example, a struck Schedule I wage figure is not counted in that debtor's gross wages.
- Whole-dollar rounding on petition PDFs recalculates rounded totals without struck answers, so the printed totals match the questionnaire.

### Where marks print

- Marks print on every petition form the Bankruptcy Schedules questionnaire produces, including the voluntary petition and its attachments, Schedules A/B through J (including the Schedule I line 8a business statement and Schedule J-2), the Summary and Declaration, the Statement of Financial Affairs, the Statement of Intention, Form 121, the Form 122 means test forms, Form 2030, the Verification of Creditor Matrix, and supported local forms.
- **The form preview matches the PDF.** The live form preview shows struck and added answers the same way the generated PDF prints them, so what you check in the preview is what is filed.
- **A struck row wins over its cells.** A cell marked added inside a struck row prints struck. A cell struck inside a row marked added prints struck only, not struck and emphasized.

## Configuration

> TODO: Confirm how amendment marks are turned on for a firm, and which template versions and forms carry them. Marking requires a Bankruptcy Schedules template version that allows struck rows, and single-answer marks print on a form only once that form's updated template has been published.

## Edge Cases & Limitations

- **Hidden fields cannot be marked.** Only answers that are currently shown can be marked. A struck answer that a later change hides does not print, struck or not.
- **Converting a joint case to individual drops Debtor 2's answers rather than striking them.** When a case's filing type changes from joint to individual, Debtor 2's answers disappear from the amended schedules instead of printing as removed, even if they were struck first. See [Converting Between Joint and Individual Filing](../../joint-and-individual-filing/converting-filing-type.md).
- **Unanswered fields cannot be marked.** A field with no answer has nothing to format, so it offers no menu.
- **Struck list rows still count in the filing statistics.** The statistical figures sent with the electronic filing leave out struck single answers and cells, but a struck list row is still counted — for example, a struck Schedule C row still counts toward total exemptions.
- **A few values print without their mark.** Answers printed inside repeated blocks that do not belong to a single list cell — such as the individual Schedule I line 8f and 8h source rows, Schedule A/B Part 3 lines, and Schedule C's exemption value — print plain.
- **A mark that cannot be saved is refused.** Marking a cell through a list that shows another list's rows — such as a creditor's amount on the Schedule E/F screen, whose rows belong to the Master Creditor List — must be saved to the underlying list. A mark sent to the wrong list returns an error rather than appearing to succeed. Previously such a strike looked applied but saved nothing.

> TODO: Confirm that striking a creditor's cell from the Schedule D, E/F, G, or H screen is now saved to the Master Creditor List row.

## Related Features

- [Petition](./README.md)
- [Generating a Draft Petition](./draft-petition.md)
- [Petition Check](./petition-check.md)
- [Working With Lists](../filling-out/working-with-lists.md)
- [Schedule I and Income](../schedules/income.md)
- [Amending a Filing](../../../integrations/pacer/amending-a-filing.md)
