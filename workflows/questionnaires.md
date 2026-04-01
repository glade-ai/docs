# Questionnaires

## Overview

Questionnaires are structured forms that collect information from clients as part of a workflow. Your team defines questionnaire templates with sections and fields, and clients fill them out through the client portal. Responses can auto-populate PDF court forms and legal documents, and feed data into downstream workflow steps.

Glade's native questionnaire system supports template versioning, field-level validation, conditional logic, linked fields, PDF fill mappings, AI-assisted autofills, and real-time sync as clients complete forms.

## Creating and Editing Templates

### Template Basics

A questionnaire template defines the structure of a form. Each template has a name, version, status (draft, current, or abandoned), label, and optional description. Templates are scoped to your firm.

When a template is updated, a new version is created. The current version is what new questionnaire instances are created from. Old versions become abandoned.

### Sections

Sections organize fields within a questionnaire. Each section has a label, optional description, optional tutorial video link, and optional subsections. Sections can be conditionally shown or hidden based on the client's answers to other fields.

### Fields

Fields define individual form inputs. Each field belongs to a section and has properties including label, type, required flag, placeholder, hint, validation rules, options (for select fields), and display configuration.

Supported field types include: short text, long text, numeric, number, currency, date, phone number, SSN, name, US address, international address, single select, multi-select, list, table, percent, and domain-specific types like creditor select, court division select, bankruptcy statute select, and median income.

### Field Validation

Fields support validation rules including minimum and maximum values, minimum and maximum lengths, patterns, required status, and custom validators (for example, age validation).

When a field fails validation, the field itself is visually highlighted — input borders, checkboxes, radio buttons, and date pickers change to indicate the error — and an error message appears below the field. This applies to all field types including short text, long text, date, address, and select fields.

### Field Options

Select-type fields define their options as a list of choices, each with a label, key, default flag, and optional PDF fill key.

### Conditional Visibility

Sections and fields can be dynamically shown or hidden based on the values of other fields. Conditions use an expression system with variables that reference other fields or external data.

### Linked Fields

Linked fields let one field's value automatically propagate to another field within or across sections, keeping data synchronized. Changes propagate in real time as clients fill out the form.

### Referenced Lists

Fields can reference other list fields to create cross-references between data sets. For example, a creditor select field can reference a creditor list so clients choose from items they have already entered.

### Table Columns

List fields can be displayed in table view. Table columns have settings for editability and visibility, controlling how the data appears and whether clients can modify values inline. The "Visible in table view" setting is available for all fields within a list, including fields nested inside explanation sections at any depth.

### PDF Fill Mappings

PDF fill mappings connect questionnaire fields to PDF template fields, enabling automatic generation of filled court forms and legal documents from questionnaire responses. Individual fields connect to specific PDF fields, and each section can reference a PDF template.

Dynamic PDF templates support generated PDFs with custom layouts and assets, going beyond simple field-to-field mapping.

### Autofills

Autofills populate field values from external data sources, AI inference, or computed expressions. AI autofills allow AI to infer field values from uploaded documents or prior responses.

### Assignees

Assignees can be configured at the field level and at the questionnaire level, controlling which team members are responsible for specific fields or the entire questionnaire.

### Tags

Tags on questionnaire templates allow categorization with label/slug pairs.

### Inheritance Scheme

The inheritance scheme controls whether new questionnaires pre-fill values from previously completed submissions for the same template:

- **None**: No pre-filling.
- **Firm-wide**: Inherits from any prior submission by your firm.
- **Per-client**: Inherits only from the same client's prior submissions.

### Followup Reminders

Followup reminders configure automated reminders (frequency in minutes, hours, days, or weeks) for incomplete questionnaires.

### Review Workflow

A review workflow can be enabled on the template so that a questionnaire goes to "submitted for review" before being marked complete. Reviewers from your team are assigned to handle the review.

### AI Summary

An AI summary can be enabled to generate a summary of the questionnaire responses after completion. The summary voice (tone) is customizable.

### Other Settings

- A **require all fields** setting controls whether all required fields must be filled before the questionnaire can be completed.
- A questionnaire can be marked as generating a case document, which enables PDF generation from the questionnaire data.
- The form provider can be set to Glade's native system, Typeform, or Anvil.

## Using Questionnaires

### Statuses

Questionnaires progress through statuses: **in progress**, **submitted for review** (if review workflow is enabled), **completed**, and **skipped**.

### Filling Out Forms

When using Glade's native form provider, initial values can be pre-populated from field mappings tied to the client's workflow or from the inheritance scheme. Clients fill out sections and fields through the client portal, with changes auto-saved and synced in real time.

Response history tracks when responses are modified, supporting undo and audit.

Default options on single-select fields (configured in the questionnaire template) are automatically applied and saved when the questionnaire first loads. These defaults count as valid answers during validation — a field with a pre-set default is not flagged as incomplete.

### Currency Field Behavior

Currency fields default to $0.00 on first load. You can delete the value to leave the field empty — it stays blank after saving rather than resetting to $0.00. An empty currency value is treated as intentionally unset, distinct from a $0.00 value.

### List Row Detail Views

List-type fields allow you to click into individual rows to view or edit details:

- When you open a row, the page link updates so you can share it directly — anyone who opens that link sees the same row's details immediately.
- Required sub-fields in each row are validated individually. Rows with missing required fields show a red dot indicator.
- The section's error badge count includes errors from incomplete list rows and table cells, in the same way it counts errors from other field types. Error badges always appear on the source list section — for example, errors in a property list appear under "Property (Real & Personal)", not under a derived section like "Schedule D Creditors". Completing required fields in a row reduces the section count; clearing them increases it. Error badge counts update when the questionnaire is submitted, not in real time as fields are edited. Section sidebar navigation and subsection tab badges display error counts in amber.
- When a list row has validation errors, each subsection tab in the detail view (for example, **Details** or **Exemptions**) shows an error count badge so you can navigate directly to the tab with missing required fields.
- When editing a row in the detail view and the questionnaire requires all fields to be complete, saving highlights any incomplete required fields and prompts you to confirm before saving with incomplete data. This prompt also appears if you clear a required field that previously had a value. On questionnaires that do not require completion, saving always proceeds without a prompt. Fields that are hidden by conditional logic are not considered incomplete and do not trigger the prompt.
- When a list row references items in another section (for example, an exemption row linked to a property), the detail header shows the parent item's name as context so you always know which item you are editing.
- A **Save & Next** button saves the current row and opens the next row immediately — no need to return to the full list between edits. **Previous** and **Next** buttons let you move between rows; if you have unsaved changes, you will be prompted before switching.
- The Save button shows a loading indicator while the save is in progress. After saving, the view returns to the full list.

### Resource Panel

The resource panel appears on the right side of the form and displays supplementary information and tools while you work — including autofill explanations, tutorial videos, reference data, and the Exemptions Calculator. All such content opens in the panel rather than as a separate popup dialog.

The panel scrolls independently of the questionnaire content. Scrolling through the form does not move the resource panel, and scrolling the panel does not move the form.

### Source Data Access

While filling out certain forms (for example, Bankruptcy Schedules), a **Source Data** dropdown lets you reference related data without leaving the form. For bankruptcy workflows that include an Income Organizer, an **Income Organizer** option appears in the dropdown — clicking it opens the Income Organizer in a new tab with the table view already expanded, so you can review income figures alongside the schedules form. The option only appears when the workflow has an associated Income Organizer.

The questionnaire content and the resource panel scroll independently — scrolling through a long questionnaire does not affect the position of the resource panel, and vice versa.

### Exemptions Calculator

When working on bankruptcy Schedule A/B or Schedule C, an **Exemptions Calculator** panel is available alongside the questionnaire. The panel shows how exemptions apply to the properties and assets you have entered.

On Schedule C, the homestead exemption question ("Are you claiming a homestead exemption of more than $214,000?") is automatically answered based on the client's total real estate value minus total secured liabilities from Schedule D. The field updates as those values change — no manual entry is needed.

The panel has two tabs:

- **By Property**: Groups properties by category in collapsible cards. Each property shows the exemptions claimed against it as labeled pills with statute citations. Status banners indicate whether remaining exemption capacity is available (shown in purple), the exemption is fully utilized (shown in green), or the claimed amount exceeds the allowed limit (shown as a warning).
- **By Exemption**: Groups entries by statute, with each exemption card collapsible to show the properties it covers and the amounts applied to each.

Both tabs include **Expand All** and **Collapse All** controls. A **Only show non-exempt** toggle filters the view to items with non-exempt value remaining.

An **Exemptions Summary** card at the top of the panel shows the total exempted and non-exempt amounts across all properties.

When viewing from Schedule A/B, property names are clickable links that navigate to that property's entry. When viewing from Schedule C, those links are hidden.

### AI Autofills

When an AI agent autofills a group of related fields (for example, property exemptions in a bankruptcy case), re-running the agent preserves any values you have already entered or confirmed. The agent incorporates existing data rather than overwriting it, so you can re-run an analysis after adding new items without losing prior work.

### Case Data Sync Fields

Some questionnaire fields are linked to case data — they display a value pulled from the case record rather than a standalone response. These fields show the synced value by default.

You can override a synced field's value directly in the questionnaire. When you close the override modal, the updated response saves immediately and reflects in the questionnaire without requiring a separate save action.

### Access Control

If you navigate to a questionnaire you are not assigned to and are not a member of the firm it belongs to, you see a "You don't have access to this questionnaire" screen. This applies to direct links shared by others — opening the link shows the access denied message rather than an error.

### Re-opening

Questionnaires can be re-opened with a message explaining why, returning them to "in progress" status.

### Collaborators

Collaborators (additional team members) can be assigned to questionnaires with view or edit permissions.

### Completion

When a questionnaire is completed, it triggers downstream workflow steps, updates case data, generates compiled documents, creates tasks, and sends notifications.

## Edge Cases & Limitations

- Typeform and Anvil providers are supported, but Glade's native provider is the primary path. Typeform questionnaires redirect clients to an external URL. Auto-complete is only supported for the Anvil provider.
- When upgrading a questionnaire to a new template version, responses are copied from the old instance. Pre-filled initial values are not re-applied during the upgrade.
- List fields that use referenced lists depend on both the referencing and referenced fields existing in the same questionnaire template.
- List fields that are linked as destinations — populated automatically from another list in the questionnaire at filing time (for example, Schedule D Creditors mirroring the Creditors list) — are not counted as incomplete during validation. Only the source list needs to be filled.
- Deduplication of list items is available but requires specifying the field.
- Linked destination list fields (for example, a Schedule D creditors list that auto-populates from a master creditor list) are not independently validated. Completing the source list is sufficient — the destination list does not need to be filled out separately.
- Clearing a required date field and saving leaves the field in an invalid state — it is treated as empty, not as a valid cleared value, so validation correctly flags it as required.
- Editing a table row and saving preserves all column data. Columns are not dropped or lost when a row is saved after being edited.

## Related Features

- [Client Portal](../intake/client-portal.md)
- [Document Collection](./document-collection.md)
