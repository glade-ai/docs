# Case Questionnaire

## Overview

Case questionnaires are structured forms that collect information from clients as part of a workflow. They are represented by the `FormRequest` entity in `noodle-api` and backed by questionnaire templates in the `webforms` service (forms-backend). Creators define questionnaire templates with sections and fields, and clients fill them out through the client portal. Responses can be used to auto-populate PDF forms and feed data into downstream workflow steps.

## Key Behaviors

- A form request is created from a `FormRequestTemplate`, which specifies the form provider (`noodle`, `typeform`, or `anvil`), the provider locator (template slug or ID), and behavioral settings.
- Form requests progress through statuses: `in-progress`, `submitted-for-review`, `completed`, and `skipped`.
- When using the Noodle provider, a questionnaire instance is created in the forms-backend service. Initial values can be pre-populated from field mappings tied to the user's workflow.
- Questionnaires are organized into sections (`SectionTemplate`), each containing fields (`FieldTemplate`). Sections can be conditionally shown/hidden based on expression logic.
- Supported field types include: `short-text`, `long-text`, `numeric`, `number`, `currency`, `date`, `phone-number`, `ssn`, `name`, `address-us`, `address-international`, `single-select`, `multi-select`, `list`, `table`, `percent`, and domain-specific types like `creditor-select`, `court-division-select`, `bankruptcy-statute-select`, and `median-income`.
- Fields support validation rules (min/max length, patterns, required status), conditional visibility expressions, default values, and autofills from external data sources or AI agents.
- Questionnaire responses are saved per field per questionnaire instance. Responses track who submitted them (`submittedById`), the source of the value (e.g., manual, autofill, AI), and support list/table row structures via `listRowResponseId`.
- The `enableReviewState` flag on the template enables a review workflow where a form request transitions to `submitted-for-review` before being marked complete. Reviewers are tracked via `FormRequestReviewer`.
- The `enableAiSummary` flag triggers an AI-generated summary of the questionnaire responses after completion. The summary voice can be customized via `aiSummaryVoice`.
- When a form request completes, it emits a `FORM_REQUEST_COMPLETED` event that triggers downstream workflow steps, case data updates, compiled document generation, task creation, and notifications.
- Form requests can be re-opened with a `reOpenMessage` explaining why, returning them to `in-progress` status.
- Collaborators (additional team members) can be assigned to form requests with view or edit permissions.
- The `completionRequiresAllRequiredFields` flag on the template controls whether all required fields must be filled before the form can be completed.
- The `isCaseDocument` flag marks a form request as generating a case document, enabling PDF generation from questionnaire data.

## Configuration

- **Form request templates** (`FormRequestTemplate`) define the questionnaire's provider, name, slug, inheritance scheme, followup settings, and behavioral flags. Templates are scoped to a creator.
- **Inheritance scheme** (`none`, `creator`, `customer`) controls whether new form requests inherit values from previously completed submissions for the same template. `creator` inherits from any prior submission; `customer` inherits only from the same client's prior submissions.
- **Followup cadence** configures automated reminders (cadence value + units: minutes, hours, days, weeks) for incomplete form requests.
- **Questionnaire templates** in forms-backend define the structure: sections, fields, assignees, PDF fill mappings, linked fields, and conditions. Templates have a version and status (`draft`, `current`, `abandoned`).
- **PDF fill mappings** connect questionnaire fields to PDF template fields, enabling auto-generation of filled court forms and legal documents from questionnaire responses.
- **Tags** on form request templates allow categorization via a list of `{slug, label}` pairs.

## Edge Cases & Limitations

- Typeform and Anvil providers are supported but the Noodle (native) provider is the primary path. Typeform form requests use an external redirect URL; Anvil form requests require a `weldDataEid`.
- Auto-complete is only supported for the Anvil provider; attempting auto-complete with other providers throws an error.
- Questionnaire template versioning means a form request can become out-of-date relative to the current template version. An "update to current version" endpoint exists to migrate a form request to the latest template, but initial values are not re-applied during the upgrade.
- The `response` field on `FormRequest` stores the raw provider response as unvalidated JSONB; its shape varies by provider.
- Deduplication of list items is available via a dedicated endpoint but requires specifying the field key.

## Related Features

- [Client Portal](./client-portal.md)
- [Document Collection](./document-collection.md)
- [Webforms](./webforms.md)
