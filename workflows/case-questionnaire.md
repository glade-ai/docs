# Case Questionnaire

## Overview

Case questionnaires are structured forms that collect information from clients as part of a workflow. Your team defines questionnaire templates with sections and fields, and clients fill them out through the client portal. Responses can auto-populate PDF court forms and legal documents, and feed data into downstream workflow steps.

## Key Behaviors

- A questionnaire is created from a questionnaire template, which specifies the form provider (Glade's native system, Typeform, or Anvil) and behavioral settings.
- Questionnaires progress through statuses: **in progress**, **submitted for review**, **completed**, and **skipped**.
- When using Glade's native provider, initial values can be pre-populated from field mappings tied to the client's workflow.
- Questionnaires are organized into sections, each containing fields. Sections can be conditionally shown or hidden based on the client's answers to other fields.
- Supported field types include: short text, long text, numeric, number, currency, date, phone number, SSN, name, US address, international address, single select, multi-select, list, table, percent, and domain-specific types like creditor select, court division select, bankruptcy statute select, and median income.
- Currency fields default to $0.00 on first load. You can delete the value to leave the field empty — it stays blank after saving rather than resetting to $0.00. An empty currency value is treated as intentionally unset, distinct from a $0.00 value.
- Fields support validation rules (min/max length, patterns, required status), conditional visibility, default values, and autofills from external data sources or AI.
- Questionnaire responses track who submitted them and the source of the value (e.g., manual entry, autofill, AI).
- When an AI agent autofills a group of related fields (for example, property exemptions in a bankruptcy case), re-running the agent preserves any values you have already entered or confirmed. The agent incorporates existing data rather than overwriting it, so you can re-run an analysis after adding new items without losing prior work.
- A **review workflow** can be enabled on the template so that a questionnaire goes to "submitted for review" before being marked complete. Reviewers from your team are assigned to handle the review.
- An **AI summary** can be enabled to generate a summary of the questionnaire responses after completion. The summary voice (tone) is customizable.
- When a questionnaire is completed, it triggers downstream workflow steps, updates case data, generates compiled documents, creates tasks, and sends notifications.
- Questionnaires can be re-opened with a message explaining why, returning them to "in progress" status.
- Collaborators (additional team members) can be assigned to questionnaires with view or edit permissions.
- A **require all fields** setting controls whether all required fields must be filled before the questionnaire can be completed.
- A questionnaire can be marked as generating a case document, which enables PDF generation from the questionnaire data.
- List-type fields allow you to click into individual rows to view or edit details:
  - When you open a row, the page link updates so you can share it directly — anyone who opens that link sees the same row's details immediately.
  - Required sub-fields in each row are validated individually. Rows with missing required fields show a red dot indicator.
  - The section's error badge count includes errors from incomplete list rows, in the same way it counts errors from other field types. Completing required fields in a row reduces the section count; clearing them increases it. Error badge counts update when the questionnaire is submitted, not in real-time as fields are edited.
  - When editing a row in the detail view and the questionnaire requires all fields to be complete, saving highlights any incomplete required fields and prompts you to confirm before saving with incomplete data. On questionnaires that do not require completion, saving always proceeds without a prompt.
  - When a list row references items in another section (for example, an exemption row linked to a property), the detail modal header shows the parent item's name as context so you always know which item you are editing.

## Configuration

- **Questionnaire templates** define the form provider, name, followup settings, and behavioral flags. Templates are scoped to your firm.
- **Inheritance scheme** controls whether new questionnaires pre-fill values from previously completed submissions for the same template:
  - **None**: No pre-filling.
  - **Firm-wide**: Inherits from any prior submission by your firm.
  - **Per-client**: Inherits only from the same client's prior submissions.
- **Followup reminders** configure automated reminders (frequency in minutes, hours, days, or weeks) for incomplete questionnaires.
- **Questionnaire templates** (in the native system) define the structure: sections, fields, assignees, PDF fill mappings, linked fields, and conditions. Templates have a version and status (draft, current, or abandoned).
- **PDF fill mappings** connect questionnaire fields to PDF template fields, enabling auto-generation of filled court forms and legal documents from questionnaire responses.
- **Tags** on questionnaire templates allow categorization with label/slug pairs.

## Edge Cases & Limitations

- Typeform and Anvil providers are supported, but Glade's native provider is the primary path. Typeform questionnaires redirect clients to an external URL. Auto-complete is only supported for the Anvil provider.
- Questionnaire template versioning means a questionnaire can become out of date relative to the current template version. An "update to current version" action exists, but pre-filled initial values are not re-applied during the upgrade.
- Deduplication of list items is available but requires specifying the field.

## Related Features

- [Client Portal](../intake/client-portal.md)
- [Document Collection](./document-collection.md)
- [Webforms](./webforms.md)
