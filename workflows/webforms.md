# Webforms

## Overview

Webforms is Glade's native questionnaire system. It powers questionnaire templates, questionnaire instances, field definitions, responses, PDF fill mappings, and AI-assisted autofills. This is the engine behind the questionnaire experience that clients and your team interact with through the client portal.

## Key Behaviors

- **Questionnaire templates** define the structure of a form. Each template has a name, version, status (draft, current, or abandoned), label, and optional description. Templates are scoped to your firm.
- **Sections** organize fields within a questionnaire. Each section has a label, optional description, optional tutorial video link, and optional subsections. Sections can be conditionally shown or hidden based on the client's answers to other fields.
- **Fields** define individual form inputs. Each field belongs to a section and has properties including label, type, required flag, placeholder, hint, validation rules, options (for select fields), and display configuration.
- **Questionnaire instances** are created when a questionnaire is started. Each instance references a template and tracks its status: in progress, submitted, submitted for review, snapshot, upgrading, or upgraded.
- **Responses** store the value for each field in a questionnaire instance. Responses track the submitter, the source of the value (manual entry, autofill, AI, mapping, etc.), and support list/table row structures.
- **Linked fields** let one field's value automatically propagate to another field within or across sections, keeping data synchronized.
- **Conditional visibility** dynamically shows or hides sections and fields based on the values of other fields.
- **Autofills** populate field values from external data sources, AI inference, or computed expressions.
- **AI autofills** allow AI to infer field values from uploaded documents or prior responses.
- **PDF fill** maps questionnaire field values to PDF template fields, enabling automatic generation of filled legal forms. Individual fields connect to specific PDF fields, and each section can reference a PDF template.
- **Dynamic PDF templates** support generated PDFs with custom layouts and assets, going beyond simple field-to-field mapping.
- **Real-time sync** propagates changes across linked fields, triggers autofills, evaluates section conditions, and auto-saves responses as the client fills out the form.
- **Assignees** can be configured at the field level and at the questionnaire level, controlling which team members are responsible for specific fields or the entire questionnaire.
- **Response history** tracks when responses are modified, supporting undo and audit.
- **Snapshots** capture point-in-time copies of a questionnaire's state.
- **Data references** link external data sources to questionnaire templates for use in autofills and computed expressions.
- **Table columns** configure how list fields are displayed in table view, with column-level settings for editability and visibility.

## Configuration

- **Questionnaire template versioning**: Templates go through draft and current statuses. When a template is updated, a new version is created. The current version is what new questionnaire instances are created from. Old versions become abandoned.
- **Field validation**: Fields support validation rules including min/max values, min/max lengths, patterns, and custom validators (e.g., age validation).
- **Field options**: Select-type fields define their options as a list of choices, each with a label, key, default flag, and optional PDF fill key.
- **Referenced lists**: Fields can reference other list fields to create cross-references between data sets (e.g., linking a creditor select field to a creditor list).
- **Expression system**: Expressions with variables drive conditional logic for section/field visibility and computed values. Variables reference other fields or external data.

## Edge Cases & Limitations

- When upgrading a questionnaire to a new template version, responses are copied from the old instance. Pre-filled initial values are not re-applied during the upgrade.
- List fields that use referenced lists depend on both the referencing and referenced fields existing in the same questionnaire template.

## Related Features

- [Case Questionnaire](./case-questionnaire.md)
- [Client Portal](../intake/client-portal.md)
- [Document Collection](./document-collection.md)
