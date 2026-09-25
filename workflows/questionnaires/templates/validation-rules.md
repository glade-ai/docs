# Validation Rules

## Overview

Fields support validation rules that flag missing or incorrect answers, and your firm's template administrator can write rules that check one field against another across the form. Findings from these rules appear on the field and in the [Petition Check](../petition/petition-check.md).

## Key Behaviors

### Field Validation

Fields support validation rules including minimum and maximum values, minimum and maximum lengths, patterns, required status, and custom validators (for example, age validation).

When a field fails validation, the field itself is visually highlighted — input borders, checkboxes, radio buttons, and date pickers change to indicate the error — and an error message appears below the field. This applies to all field types including short text, long text, date, address, and select fields.

Dropdown fields follow the same layout as every other field type: the label turns red, the box is outlined, and the message appears once, below the box. Previously a dropdown such as **District of:** printed its message twice — once above the box and once below — while the field beside it showed a single message underneath, so the same error looked different on two adjacent fields.

### Validation rules on a cell of a table or list

Your firm's template administrator can write validation rules that check one field against another across the form. A rule can now be anchored on a **cell inside a table or a list** — for example, Form 122A-1 line 5 for Debtor 1 — rather than only on a standalone field. Rules written that way are evaluated and their findings appear in the Petition Check results alongside every other issue.

- These rules previously did not run at all. A rule anchored on a cell was skipped silently: it was switched on, it appeared in the rule list, and it never produced a finding, whether the answer was right or wrong. If your firm wrote rules against a table cell and never saw them fire, that is why. A template could look fully checked while a substantial share of its rules never ran; on the standard bankruptcy schedules template this covered a large part of the business-disclosure cross-checks.
- **A rule is checked once per column of a table, or once per row of a list**, and each column or row that fails produces its own finding pointing at that cell. On a joint case, a rule on a two-debtor table is checked for both debtors.
- A rule reads the cell in the row it is anchored to, so a check comparing Debtor 1's figure against Debtor 2's compares the right two cells rather than the first value it finds in the column.
- **A column that nobody has filled in is still checked.** A table column left untouched is a real column with unanswered cells, not an absent one.
- A rule can be narrowed to a **single column** where it is only meant to apply to one debtor.
- Where a rule is written incorrectly — it points at a cell that cannot be found, for example — that is reported once against the rule itself rather than repeated on every row.
- **Expect to see findings on petitions that previously reported none.** A questionnaire that passed the check before may now raise issues on answers that were always wrong but never examined. These are real findings, not a new restriction.

Because a rule written for one debtor is otherwise checked against both, a rule that means "at least one debtor" needs to be either narrowed to a column or rewritten to ask the question once across the whole table. Otherwise a joint case where only one debtor runs a business can raise a blocking finding on the other debtor's column that nobody can clear.

> TODO: Confirm which rules your firm's templates ship with this enabled, and where a rule is narrowed to a single column in the template editor. The set of rules switched on at release was still being reviewed rule by rule.

### When a rule's answers have not been given yet

A rule that compares fields cannot reach a verdict until the fields it reads have been answered. Where one of them is still blank, Glade reports the blank rather than the comparison:

- The rule's own message is withheld, and a finding reading **Needed to check '<field name>'** appears on the blank field instead, carrying the rule's severity. The finding names the field the rule is anchored on, so it is clear which check is waiting.
- The finding sits on the field that needs the answer, which is the one you can act on — not on the field the rule reports against.
- Once the blank field is answered, the finding clears and the rule is evaluated normally, raising its own message only if the answers genuinely disagree.

Previously a rule fired its full message as soon as one of its inputs was blank — telling a filer their answers contradicted each other before they had given one of the answers. Working down a long form produced a run of contradiction warnings that cleared themselves as the filer caught up.

**Not every blank means "not answered yet".** Your firm's template administrator can mark an individual field a rule reads as one that is allowed to be blank, so the rule is evaluated with the blank treated as nothing rather than as a missing answer. The distinction is between an amount that is blank because there is none — no income of that kind, a column a single filer does not have — and an answer that is blank because the filer has not reached it. The setting is per field per rule, so the same field can be required in one rule and optional in another.

### Rules that compare two answers

Some rules exist to confirm that two answers match — an address entered in two places, identity details repeated across forms — or that they differ, such as a creditor's address that must not be the debtor's own.

- **A blank answer on either side passes.** A comparison rule does not fire on an answer that has not been filled in yet, so working through a questionnaire from the top does not produce a cascade of mismatch warnings on fields you have not reached. Missing answers are reported by the ordinary required-field check instead.
- Once both answers are present, the comparison is made and any mismatch is reported as a normal finding, with the message your firm's template administrator wrote on the rule.

> TODO: Reconcile with "When a rule's answers have not been given yet" above — that section describes a **Needed to check** finding on the blank field, while this one says a blank side passes. Confirm whether match/differ rules are an exception.

## Edge Cases & Limitations

- Clearing a required date field and saving leaves the field in an invalid state — it is treated as empty, not as a valid cleared value, so validation correctly flags it as required.
- Required-field validation skips list rows that will not be filed. Rows merged into another as duplicates (for example, deduplicated creditors) and rows explicitly marked to omit from the petition are not checked for missing required fields, so leftover data on those rows does not block submission.
- Messages your firm's template administrator wrote on a validation rule are shown exactly as written and are not shortened.

## Related Features

- [Questionnaires](../README.md)
- [Building Templates](./README.md)
- [Petition Check](../petition/petition-check.md)
- [Cross-Form Consistency Checks](../petition/cross-form-checks.md)
- [Submitting a Questionnaire](../filling-out/submitting.md)
- [Conditional Visibility](./conditional-visibility.md)
