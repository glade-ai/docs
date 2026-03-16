# Webforms

## Overview

Webforms is the internal service (codebase: `webforms/forms-backend`) that powers Glade's native questionnaire system. It manages questionnaire templates, questionnaire instances, field definitions, responses, PDF fill mappings, and AI-assisted autofills. The noodle-api service communicates with webforms via an HTTP interface to create questionnaires, fetch templates, update responses, and retrieve mapping data.

## Key Behaviors

- **Questionnaire templates** define the structure of a form. Each template has a slug, version, status (`draft`, `current`, `abandoned`), label, and optional description. Templates are scoped to a `creatorId`.
- **Section templates** organize fields within a questionnaire. Each section has a slug, key, rank, label, optional description, optional tutorial video link, and optional subsections. Sections can be conditionally shown or hidden via a `conditionExpressionId` that references an expression entity.
- **Field templates** define individual form fields. Each field belongs to a section and a questionnaire template, with properties including key, label, type, rank, required flag, placeholder, hint, validation rules, options (for select fields), and view configuration.
- **Questionnaire instances** are created when a form request is initiated. Each instance references a questionnaire template and tracks its status: `in-progress`, `submitted`, `submitted-for-review`, `snapshot`, `upgrading`, or `upgraded`.
- **Questionnaire responses** store per-field values for a questionnaire instance. Responses track the submitter, source (manual entry, autofill, AI, mapping, etc.), visibility, and list row associations. Values are stored as JSONB and vary by field type.
- **Linked fields** enable one field's value to automatically propagate to another field within or across sections, keeping data synchronized.
- **Conditional visibility** uses expression entities to dynamically show or hide sections and fields based on the values of other fields.
- **Autofills** populate field values from external data sources, AI inference, or computed expressions. The `FieldTemplateAutofill` entity connects a field to its autofill source.
- **AI agent autofills** allow AI models to infer field values from uploaded documents or prior responses. These are tracked via `AiInferenceRequest` and `QuestionnaireAgent` entities.
- **PDF fill** maps questionnaire field values to PDF template fields, enabling automatic generation of filled legal forms. Each section can reference a `PdfTemplate`, and individual fields connect to PDF fields via `PdfFill` entities.
- **Dynamic PDF templates** (`DynamicPdfTemplate`) support generated PDFs with custom layouts and assets, going beyond simple field-to-field PDF fill.
- **Real-time sync** on the frontend uses watchers to propagate changes across linked fields, trigger autofills, evaluate section conditions, and auto-save responses as the client fills out the form.
- **Assignees** can be configured at the field level via `FieldAssigneeTemplate` and at the questionnaire level via `QuestionnaireAssigneeTemplate`, controlling which team members are responsible for specific fields or the entire questionnaire.
- **Response saves** are tracked via `QuestionnaireResponseSave` to support undo/history and audit of when responses were modified.
- **Questionnaire snapshots** (`QuestionnaireSnapshot`) capture point-in-time copies of a questionnaire's state.
- **Data references** (`DataReference`) link external data sources to questionnaire templates for use in autofills and expressions.
- **Table columns** (`TableColumn`) configure how list fields are displayed in table view, with column-level settings for editability and visibility.

## Configuration

- **Questionnaire template versioning**: Templates go through `draft` and `current` statuses. When a template is updated, a new version is created. The `current` version is what new questionnaire instances are created from. Old versions become `abandoned`.
- **Field validation**: Fields support validation rules including min/max values, min/max lengths, patterns, and custom validators (e.g., age validation). Validation is defined as a JSONB `validation` column on the field template.
- **Field options**: Select-type fields define their options as a JSONB array of `{key, label, isDefault, pdfFillKey}` objects.
- **Referenced lists**: Fields can reference other list fields to create cross-references between data sets (e.g., linking a creditor select to a creditor list).
- **Expression system**: Expressions (`Expression` entity) with variables (`ExpressionVariable`) drive conditional logic for section/field visibility and computed values. Variables reference other fields or external data.
- **API keys**: The forms-backend service uses API key authentication (`ApiKey` entity) for inter-service communication.

## Edge Cases & Limitations

- Questionnaire responses store values as untyped JSONB (`value: unknown`); the actual shape depends on the field type and is not enforced at the database level.
- The `mediumDeletedAt` field on responses is a soft-delete variant used specifically for marking deduplicated list items, distinct from the standard `deletedAt` soft delete.
- The `originalQuestionnaireId` column on both `Questionnaire` and `QuestionnaireResponse` is nullable and intended to be backfilled, indicating this is a transitional schema.
- When upgrading a questionnaire to a new template version, responses are cloned from the old instance. Initial value mappings are not re-applied during the upgrade.
- The `fromQuestionnaireId` on `Questionnaire` tracks which questionnaire instance this one was cloned from (e.g., during version upgrades).
- List fields that use `referencedList` create cross-references that depend on both the referencing and referenced fields existing in the same questionnaire template.

## Related Features

- [Case Questionnaire](./case-questionnaire.md)
- [Client Portal](./client-portal.md)
- [Document Collection](./document-collection.md)
