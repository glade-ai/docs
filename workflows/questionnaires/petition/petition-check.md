# Petition Check

## Overview

Before a client or preparer submits a petition questionnaire, a **Petition Check** dialog gives a single, consolidated view of everything still needing attention, instead of surfacing problems one field or section at a time. This page covers the dialog, how findings are ordered and worded, and how findings appear on the fields themselves.

## Key Behaviors

### The Petition Check dialog

- Summary tiles at the top count the outstanding **validation errors**, the **sections affected**, the **incomplete dates**, and the **incomplete signatures**, so you can gauge the overall state at a glance.
- Below the tiles, every outstanding issue is grouped by section and subsection in an expandable list. Each entry shows the field label and what is wrong, and a **Go to field** action takes you straight to that field — switching sections if needed, scrolling it into view, and focusing it.
- Issues on list rows are included in both the counts and the list. Previously, required-field issues inside a list row — for example, blank fields on a row of the Master Property List — could be dropped from the section badges and this summary when the row took its section from the parent list, so a list with many missing fields might read as a single issue or none. All of a row's outstanding issues now appear.
- Standalone date fields — such as a date of birth or the date a debt was incurred — appear in the normal issue list and section badges alongside every other field, rather than being separated into their own tile where they were easy to overlook.
- **Issues on fields the form never shows are left out.** A section that is divided into subsection tabs displays its fields inside those tabs. A leftover field belonging to no tab is not displayed anywhere, so it can never be filled in — and when such a field was marked required, it produced a permanent blocking issue with no way to resolve it, sometimes with nothing but a generic label to identify it. **Go to field** had nowhere to take you. These issues no longer appear in the Petition Check dialog, in the section and subsection badge counts, or in the count that gates submission. Fields you can actually reach are unaffected, including fields on sections that have no subsection tabs at all and the means-test summary fields that appear on every tab.

### Working through the results

Once a check has run, the results stay available while you work through them:

- A shield icon with a count of the outstanding findings remains in the questionnaire header. Selecting it reopens the results you already have, without running the check again — so going back to the list after correcting a field is immediate.
- The count stays current as you fix errors on the form. Resolving a field lowers the number without a second check.
- Previously the results dialog closed as soon as you navigated to a field, and getting back to the findings meant re-running the whole check, which is slow and interrupts correction work.
- **The results open whatever the check found.** A run that turned up only advisory or informational findings used to show a "No validation issues found" message and no dialog, while reopening the same results from the header shield listed them in full — so the same check appeared to contradict itself between the first click and the second. Both routes now open the results for any finding, and the "no issues found" message appears only when the check genuinely found nothing.
- **Go to field stays on the field.** Choosing **Go to field** — from the results dialog, from the count badge on a subsection tab, or from the count beside a list row's title — scrolls to the failing field and leaves it in view, including when the field is in a different section. Previously the page could scroll to the field and then jump back to the top or to the badge you clicked, or never leave the top at all. Changing sections from the sidebar still starts you at the top of the new section.

### Order of issues

**Issues are listed in the order they appear on the form.** Working the list from top to bottom walks you down the questionnaire in one pass, rather than sending you back and forth through it:

- Within a section, entries follow the subsection tabs left to right, then field order within each tab. An issue on a field that sits above the tab strip comes before the tabbed subsections.
- Issues on a list or table row sit with the field they belong to, instead of being collected after every ordinary field in the section. A table reads down each row before moving to the next column, and a list reads each row's fields together — so both of a joint case's debtors are grouped rather than interleaved.
- A list's own issue comes before the issues on its rows.
- Severity no longer controls the order. Blockers and advisories are interleaved in form order, and each entry is tagged with its severity so you can still tell them apart. Previously every blocker was listed ahead of every advisory, which reordered the list around a distinction the entries gave no visible sign of.
- **Go to first error** lands on the earliest failing field in the form rather than an arbitrary one.
- The order is stable. Re-running the check on an unchanged questionnaire produces the same list in the same order; previously it could come back differently each time.

### How findings are worded

Each row is laid out as the field label, the subsection it sits in, and then the finding itself in a speech bubble pointing at the Glade AI mark, so a several-sentence cross-check explanation reads as commentary from the assistant rather than competing for urgency with a four-word required-field message. Findings previously printed inline in warning orange, at the same weight whether they were one word or a paragraph.

The findings themselves are written to say only what is wrong, since the row already names the field:

- A missing answer reads **Required** rather than restating the whole question back to you — a difference that mattered most on long labels, where a single question could fill five lines of the dialog.
- Related wordings follow the same pattern: **At least one entry required**, **Invalid date**, **Must be a valid number**.
- **Findings about part of a field keep naming that part.** On a name, address, or amount that is only partly filled, the finding still reads `'Last Name' is required`, `'ZIP Code' is required`, or `'Amount' is required` — the label alone does not tell you which piece is missing.
- Messages your firm's template administrator wrote on a validation rule are shown exactly as written and are not shortened.

### Signature, date, and currency answers

Glade validates signature, date, and currency answers precisely so the check's counts match what you see on the form:

- A signature that is missing its date flags the date field itself, not just a generic "signature and date are required" message, so you can tell which part is missing.
- A signature mark with no name after it (an empty electronic-signature placeholder) is not accepted as a completed signature.
- A date that is present but not a recognizable date is flagged as **invalid** rather than passing silently. A date entered as free-form text, instead of picked from the calendar, counts as filled.
- A currency amount marked **Unknown** or overridden with explanatory text counts as an answered field and is no longer reported as missing.

### Findings appear on the field itself

Not every finding blocks a submission, and the ones that do not are now shown on the field they name, not only in the check dialog.

- An advisory or informational finding prints as a note directly beneath its field, with its severity named and the message written out in full. A cell inside a table or a list row carries its note the same way.
- The field is not marked as failing: its border and label stay as they are, and the finding does not gate the submit. Only blocking findings turn a field red, and they appear as they always have — a blocking finding is not repeated as a second note.
- Colour follows severity consistently everywhere a finding is shown. Blocking findings are red, advisory findings amber, and informational findings grey — the same treatment in the field note, the Petition Check dialog, and the subsection popover.
- Findings listed in the subsection popover are now tagged with their severity, matching the Petition Check dialog. Previously the popover printed every message in the same warning colour with no tag, so an advisory note and a blocker looked identical. Where the popover collapses several findings into a single "N issues in the list" line, that line takes the strictest severity among them.

Previously **Go to field** on an advisory finding took you to a field that looked completely clean — the message existed in the dialog and in the subsection popover, but nowhere on the form — which read as a broken check rather than as a finding you were meant to act on.

### A finding on a row of a list names the row

A finding on a cell inside a list names the entry the row describes, so several findings on the same column of the same list can be told apart.

- The row's name appears under the field label — the creditor, the property, or whatever the row is about. It is read from the row's own answers: the sub-field your firm's template marks as the row's title, or, on the Master Property List, the category and description together.
- **Go to field opens that row.** It opens the row's editor on the right subsection with the cell in question focused, instead of scrolling to the top of the list. Where the row has been removed since the check ran, it falls back to scrolling to the list rather than opening a different row.
- Where a subsection's findings are collapsed into a single **N issues in the list** line, that line names the rows it covers — up to three of them, then a count of the rest.
- Table findings are unchanged: a table repeats the same fields across its columns, and those findings already name the column they belong to.

Previously a finding on a list cell showed its field label and nothing else, so four advisories on one Master Creditor List all read **Account Number** and named none of the creditors they were about — and **Go to field** landed on the top of the list, so whichever row happened to be on screen was the one that got read.

For rules written against table and list cells, and rules that compare two answers, see [Validation Rules](../templates/validation-rules.md).

## Edge Cases & Limitations

- Validation issues on a **list row** name the field but not the row. A list of vehicles with the make missing on two rows produces two issues that read alike, with nothing to distinguish one vehicle from the other. Table cells do name their column; list rows do not yet.

> TODO: The limitation above conflicts with "A finding on a row of a list names the row". Confirm whether it still applies anywhere (for example, the section badge error dialog) or can be removed.

## Related Features

- [Questionnaires](../README.md)
- [Petition](./README.md)
- [Cross-Form Consistency Checks](./cross-form-checks.md)
- [Validation Rules](../templates/validation-rules.md)
- [Submitting a Questionnaire](../filling-out/submitting.md)
- [Generating a Draft Petition](./draft-petition.md)
