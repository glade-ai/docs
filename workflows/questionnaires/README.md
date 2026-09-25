# Questionnaires

## Overview

Questionnaires are structured forms that collect information from clients as part of a workflow. Your team defines questionnaire templates with sections and fields, and clients fill them out through the client portal. Responses can auto-populate PDF court forms and legal documents, and feed data into downstream workflow steps.

Glade's native questionnaire system supports template versioning, field-level validation, conditional logic, linked fields, PDF fill mappings, AI-assisted autofills, and real-time sync as clients complete forms.

## Topics

### [Building Templates](./templates/README.md)

- [Template Settings](./templates/template-settings.md) — versions, sections, assignees, tags, inheritance, reminders, review workflow, AI summary, and form provider.
- [Fields, Lists, and Tables](./templates/fields-and-tables.md) — field types, select options, linked and referenced fields, and table columns.
- [Validation Rules](./templates/validation-rules.md) — field validation and rules that check one answer against another.
- [Conditional Visibility](./templates/conditional-visibility.md) — showing and hiding sections and fields.
- [PDF Fill Mappings](./templates/pdf-fill-mappings.md) — mapping answers to court forms, supplemental forms, and printed totals.

### [Autofills](./autofills/README.md)

- [How Autofills Work](./autofills/how-autofills-work.md) — when an autofill writes, combined values, calculated totals, and reference data.
- [Autofill Status Indicators](./autofills/status-indicators.md) — what each indicator means and background recalculation.
- [Manual Overrides](./autofills/manual-overrides.md) — how typed values are protected, including Schedule I and Means Test calculator lines.
- [Locked Fields](./autofills/locked-fields.md) — fields held to their autofilled value.
- [AI Agents](./autofills/ai-agents.md) — agent-filled fields, re-running agents, the filing district, and explanations.

### [Filling Out Questionnaires](./filling-out/README.md)

- [Statuses and Access](./filling-out/statuses-and-access.md) — statuses, the client's view after submitting, access control, and collaborators.
- [Filling Out Forms](./filling-out/filling-out-forms.md) — pre-filling, simultaneous editing, and template defaults.
- [Field Behaviors](./filling-out/field-behaviors.md) — phone, currency, court division, debtor county, and SOFA free-text dates.
- [Working With Lists](./filling-out/working-with-lists.md) — row detail views, removing and restoring rows, and concurrent edits.
- [Layout and Navigation](./filling-out/layout-and-navigation.md) — resource panel, Source Data, tables, large questionnaires, and mobile.
- [Printing a Questionnaire](./filling-out/printing.md) — printing a section from your browser.
- [Submitting a Questionnaire](./filling-out/submitting.md) — fields with errors, Fields Need Attention, submit anyway, and completion.

### [Case Data](./case-data/README.md)

- [Case Data Sync](./case-data/case-data-sync.md) — synced fields and lists, turning sync off, and deleting and restoring entities.
- [Re-opening and Re-syncing](./case-data/reopening-and-resync.md) — re-opening, Get back in sync, and Compare case data.
- [Template Upgrades](./case-data/template-upgrades.md) — release notes and what an upgrade does to answers and case data.

### [Schedule Tools](./schedules/README.md)

- [Exemptions Calculator](./schedules/exemptions-calculator.md) — exemption coverage, the exemptions agent, the homestead answer, and the Texas schedule.
- [Schedule A/B Property](./schedules/property.md) — liens, equity, Property summary, and Part 3 and line 19 printing.
- [Creditors](./schedules/creditors.md) — adding creditors, duplicates, alphabetized schedules, and the creditor matrix.
- [Schedule I and Income](./schedules/income.md) — Income Organizer import and lines 8f and 8h.
- [Means Test](./schedules/means-test.md) — non-consumer Chapter 7 cases and secured debt deductions.
- [Chapter 13 Plan Calculator](./schedules/chapter-13-plan-calculator.md) — modeling and generating the Chapter 13 plan.

### [Petition](./petition/README.md)

- [Petition Check](./petition/petition-check.md) — the consolidated list of what still needs attention.
- [Cross-Form Consistency Checks](./petition/cross-form-checks.md) — contradictions between forms in the package.
- [Generating a Draft Petition](./petition/draft-petition.md) — drafts, signing copies, and automatic rebuilds.
- [Signatures](./petition/signatures.md) — signature choices and signer names.

## Edge Cases & Limitations

- Typeform and Anvil providers are supported, but Glade's native provider is the primary path. Typeform questionnaires redirect clients to an external URL. Auto-complete is only supported for the Anvil provider.

## Related Features

- [Client Portal](../../intake/client-portal/README.md)
- [Document Collection](../document-collection/README.md)
- [Case Documents](../case-documents.md)
- [Income Organizer](../income-organizer/README.md)
- [Signature Pages](../signature-pages.md)
