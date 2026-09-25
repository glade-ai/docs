# Template Settings

## Overview

A questionnaire template defines the structure of a form and the settings that control how questionnaires created from it behave — versioning, sections, assignees, pre-filling, reminders, review, AI summaries, and which form provider is used. Templates are maintained by your firm's template administrator.

## Key Behaviors

### Template Basics

A questionnaire template defines the structure of a form. Each template has a name, version, status (draft, current, or abandoned), label, and optional description. Templates are scoped to your firm.

When a template is updated, a new version is created. The current version is what new questionnaire instances are created from. Old versions become abandoned.

### Sections

Sections organize fields within a questionnaire. Each section has a label, optional description, optional tutorial video link, and optional subsections. Sections can be conditionally shown or hidden based on the client's answers to other fields (see [Conditional Visibility](./conditional-visibility.md)).

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

## Configuration

- A **require all fields** setting controls whether all required fields must be filled before the questionnaire can be completed.
- A questionnaire can be marked as generating a case document, which enables PDF generation from the questionnaire data.
- The form provider can be set to Glade's native system, Typeform, or Anvil.

## Edge Cases & Limitations

- Typeform and Anvil providers are supported, but Glade's native provider is the primary path. Typeform questionnaires redirect clients to an external URL. Auto-complete is only supported for the Anvil provider.
- Publishing a new template version requires release notes; see [Template Upgrades](../case-data/template-upgrades.md).

## Related Features

- [Questionnaires](../README.md)
- [Building Templates](./README.md)
- [Fields, Lists, and Tables](./fields-and-tables.md)
- [Statuses and Access](../filling-out/statuses-and-access.md)
- [Template Upgrades](../case-data/template-upgrades.md)
- [Case Documents](../../case-documents.md)
