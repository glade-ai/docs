# Task Templates

## Overview

Task templates are predefined, reusable configurations that set up an entire workflow in one step — including the service, invoices, questionnaires, document requests, custom terms, and the automation step sequences. Instead of building a workflow from scratch, your firm can apply a template and get a fully configured workflow immediately. Templates are available for common legal practice areas such as immigration, bankruptcy, and personal injury.

## Key Behaviors

- Each template is identified by a unique name and categorized by practice area: immigration, bankruptcy, personal injury, or general.
- When a template is applied, the system creates all the components defined in it: the service, invoices, questionnaires, document requests, custom terms, consultation offerings, and automation workflows with their step sequences.
- A template defines:
  - **Service**: The legal service offering that the workflow is attached to, including its name and category.
  - **Invoices**: Invoice templates with line items, pricing, and payment settings.
  - **Questionnaires**: Client intake forms with settings for auto-completion, reminder frequency, and form type.
  - **Document requests**: Requests for the client to upload specific documents, including file specifications and grouping.
  - **Custom terms**: Legal agreements with dynamic variables and signature settings.
  - **Consultations**: Booking-based consultation offerings with pricing.
  - **Workflows**: One or more automation workflows, each containing sequences of triggers and actions.
- Each workflow within a template includes its own:
  - **Step sequences**: Ordered chains of triggers (events to wait for) followed by actions (messages with attachments).
  - **Data fields**: Information collected during the workflow (client details, case-specific information, selections).
  - **Compiled documents**: References to documents generated or collected during the workflow.
  - **Fee and notification settings**: Platform fees, estimated total fees, and email preferences.
- Template components reference each other by name. For example, a message action can include an invoice attachment by referencing the invoice's name within the template.
- Templates support conditional attachments — certain attachments on a message can appear only when specific conditions are met.
- Default team member assignments can be specified in the template and are applied to the workflow when it is created.

## Configuration

- **Template name**: Unique identifier used to look up and apply the template.
- **Practice area**: Legal category — immigration, bankruptcy, personal injury, or general.
- **Version**: Template version number for tracking updates.
- **Per-workflow settings** (each workflow in a template can have its own):
  - USCIS updates enabled/disabled
  - PACER submissions enabled/disabled
  - PDF generation enabled/disabled
  - Email notification on completion
  - Ability to start related workflows on completion
  - Preserve team assignments on duplication
  - Case type classification
  - Platform fee and estimated total fees

## Edge Cases & Limitations

- Template names must be globally unique across all templates.
- If applying a template fails partway through, some components may be partially created. The process is not all-or-nothing.
- All components in a template reference each other by name. If a referenced name does not exist within the template, the process fails.
- The version number is informational only. The system does not enforce version compatibility.

## Related Features

- [Automation Rules](./automation-rules.md) — the workflows that templates create
- [Triggers](./triggers.md) — trigger types used in template step sequences
- [Status Tracking](./status-tracking.md) — how cases created from templates track progress
