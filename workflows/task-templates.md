# Task Templates

## Overview

Task templates (called `WorkflowTemplate` in the codebase) are predefined, reusable configurations that define an entire workflow setup — including products, invoices, form requests, document requests, custom terms, and the workflow step sequences. They allow creators to instantiate a fully configured workflow from a template rather than building one from scratch. Templates are primarily used for legal practice areas such as immigration, bankruptcy, and personal injury.

## Key Behaviors

- A template is stored as a JSON document in the `workflow_templates` table, identified by a unique `slug` and categorized by legal practice area (`immigration`, `bankruptcy`, `personal-injury`, or `unknown`).
- When a template is applied, the system clones its configuration into real entities: products, product types, invoices, form request templates, document requests, custom terms, workflow contexts, and workflow steps with their trigger-action chains.
- The template JSON structure defines:
  - **Product and product type**: The service offering that the workflow is attached to, including slug and title.
  - **Invoices**: Invoice templates with line items, pricing, and payment configuration.
  - **Form requests**: Questionnaire templates with settings for auto-completion, followup cadence, and provider configuration.
  - **Document requests**: Document upload requests with file specifications, grouping, and integration settings.
  - **Custom terms**: Legal terms/agreements with dynamic variables and signature configuration.
  - **Consultations**: Booking-based consultation offerings with pricing.
  - **Workflows**: One or more workflow definitions, each containing threads of trigger-action step sequences.
- Each workflow within a template defines its own:
  - **Threads**: Ordered sequences of trigger-initiate steps followed by send-message actions with attachments.
  - **Context variables**: Data fields collected during the workflow (person info, additional info, selections).
  - **Compiled documents**: References to documents generated or collected during the workflow.
  - **Fees and settings**: Noodle fee, estimated total fees, email notification preferences.
- The clone process resolves references by slug — template components reference each other by slug (e.g., a message attachment references an invoice template by slug), and the clone process maps these to real entity IDs.
- Templates support expression-based conditional logic on message attachments, allowing certain attachments to appear only when conditions are met.
- Owner assignments can be specified at the template level (`ownerPersonIds`) and are applied to the workflow upon cloning.

## Configuration

- **slug**: Unique identifier for the template. Used to look up and apply the template.
- **category**: Legal practice area classification — `immigration`, `bankruptcy`, `personal-injury`, or `unknown`.
- **version**: Template version number, stored in the JSON payload.
- **Workflow-level settings** (per workflow in the template):
  - `enableUscisUpdates`: Enable USCIS tracking.
  - `enablePacerSubmissions`: Enable PACER filing integration.
  - `hasGeneratedPdfs`: Whether the workflow generates compiled PDFs.
  - `sendEmailToCreatorOnCompletion`: Email notification on completion.
  - `canInitiateAssociatedWorkflows`: Allow spawning associated workflows.
  - `preserveWorkflowAssignment`: Preserve owner assignments on duplication.
  - `caseType`: Optional case type classification.
  - `noodleFee` / `estimatedTotalFees`: Fee configuration.

## Edge Cases & Limitations

- Template slugs must be globally unique across all templates.
- The clone process is not atomic across all entities — if it fails partway through, partial entities may be created.
- Templates reference building blocks (form requests, document requests, invoices) by slug. If a slug collision occurs or a referenced slug does not exist in the template definition, the clone process fails.
- Expressions within templates are cloned as new expression entities; they do not share references with the original template expressions.
- The `version` field in the template JSON is informational and is not enforced by the system for compatibility checks.

## Related Features

- [Automation Rules](./automation-rules.md) — the workflow definitions that templates instantiate
- [Triggers](./triggers.md) — trigger types used in template thread definitions
- [Status Tracking](./status-tracking.md) — how workflows created from templates track progress
