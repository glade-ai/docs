# Settings

## Overview

Settings control how your firm's back office behaves. This includes custom workflow statuses, workflow roles, workflow templates, payment and billing configuration, notification preferences, AI settings, branding, and third-party integrations (Stripe, QuickBooks, PACER). Settings are managed through the dashboard.

## Key Behaviors

### Custom Statuses

- Your firm defines the workflow statuses that cases progress through. Each status has a title, icon (from a fixed set), and color.
- Two special behaviors can be enabled per status:
  - **Archive behavior** — cases in this status are treated as archived
  - **Disable follow-ups** — automated follow-up reminders stop for cases in this status
- A set of default statuses is created when your firm is set up, including Data Collection, Processing, Filed and Pending, Completed, Archived, Retainer Sent, and others.
- Custom statuses can be **archived** when they are no longer in active use. Archiving a status removes it from the workflow step dropdown so it cannot be assigned to new steps, but any existing workflow steps that already reference the status continue to work correctly — active cases are not affected.
- All statuses — including the default statuses created when your firm was set up — can be archived. Default statuses cannot be deleted, but they can be archived and unarchived.
- When you archive a status that is currently assigned to one or more active workflows, a confirmation dialog shows how many workflows use it. You can proceed with archiving — those workflows are not affected — or cancel to leave the status active.
- To view archived statuses on the Custom Statuses settings page, turn on the **Show archived** toggle. Each archived status shows **Unarchive** and **Delete** actions.
- Archiving a status is reversible — use **Unarchive** to make it available in the workflow step dropdown again.

### Workflow Roles

- Your firm defines named roles (e.g., "Paralegal", "Documents Team") that team members can be assigned to. Each role has a display rank that controls ordering in lists and reports.
- Workflow roles are used to segment team members in reports and to set a default role for case assignments.

### Workflow Templates

- Workflow templates define the structure of a case: steps, contexts, invoices, owner assignments, and fee structure.
- Key template settings include:
  - Whether the template is locked, archived, or enabled
  - Whether USCIS updates or PACER submissions are enabled
  - Whether your firm receives an email when a case is completed or when a first payment is received
  - Whether associated workflows can be initiated from this template
  - Whether team member assignments carry over to associated workflows
- Templates have a state of "current", "draft", or "stale", and a version number for tracking revisions.
- You can set a platform fee percentage and an optional estimated total fees amount displayed to clients.
- Templates are either "basic" or "attorney-case" type, with an optional case type for categorization.

### Payment & Billing

- **Default currency** sets the currency used for payments and invoices.
- **Stripe integration** connects your firm to Stripe for payment processing. The account type can be Connect, Express, or Managed.
- **Statement descriptor** sets the text that appears on client bank or card statements.
- **QuickBooks integration** controls when invoices are synced to QuickBooks: never, when payable, or on first payment.
- **Confido integration** can be configured for alternative payment processing.

### Notifications

- **Chat message notifications** control how your firm is notified of client chat messages: via SMS or not at all.
- **Notify on every customer message** sends a notification for every incoming client message when enabled.
- **Notification phone number** is the phone number used for SMS notifications.
- **Slack integration** sends notifications to a configured Slack channel.
- **Support email** settings customize the sender name and address for outbound emails to clients. For attorney firms whose outbound mail goes from the shared Glade support address, the sender display name shown to clients defaults to the firm's name when no custom sender name has been set — so emails arrive labeled with the firm name rather than no name at all. A custom **support email sender name** still takes precedence when configured.
- **Custom confirmation email message** lets you add custom text to payment confirmation emails.

### AI Settings

- **AI toggle** enables or disables AI features for your firm.
- **Chat prompt and welcome message** configure the AI chat experience that clients see.
- **System message and rules** provide instructions that control how the AI behaves when interacting with clients.

### Branding

- **Brand color** sets your firm's primary color (hex value).
- **Logos** include a full logo and a compact logo for different display contexts.
- **Custom domain** sets a custom domain for your firm's public-facing pages.
- **Custom Open Graph image** controls the preview image shown when your pages are shared on social media.
- **Payment redirect URL** sets where clients are redirected after a successful payment.

### Follow-up Cadence

- Controls how often automated follow-up reminders are sent to clients with outstanding tasks. You configure the interval (e.g., every 3 days), the unit (days or weeks), and the percentage of task completion that triggers the reminder.

### Filing Packet AI Review

When your firm uses AI-assisted document review for filing packets, you can customize the review instructions for each document type. This lets you tailor how the AI evaluates specific documents — for example, adding firm-specific checks or adjusting focus areas.

- Access **Filing Packet AI Review Configs** from your dashboard to view and manage review instructions across all 20 supported document types.
- Each document type shows the default review instructions. You can add an **override** (replaces the default entirely) or an **append** (adds to the default instructions).
- Rows with active customizations are marked with a **Customized** tag so you can see at a glance which document types have firm-specific settings.
- To remove a customization and revert to the default, use the **Clear** button on that row.

### Petition Settings

Petition Settings control how signature pages are rendered in petition documents generated by Glade. Access this page from your account's business details section.

- **Signature pages mode** controls where attorney and client signatures appear in generated petition PDFs:
  - **Full Page** (default) — signature blocks are placed on a dedicated full page at the end of the document, separated from the main form content.

Changes to petition settings apply to new documents generated after the change. Previously generated petition documents are not affected.

### Credit Reports

- **Pull attempt limit** sets the maximum number of credit report pull attempts per case.
- Credit report pulls are billed from the first pull at the standard rate — there is no free-pull threshold.

## Configuration

Settings are primarily configured through the dashboard account page and individual workflow template settings pages.

## Edge Cases & Limitations

- Custom status names must be unique within your firm. If you try to create a duplicate, the system generates a unique variation automatically.
- If your firm's timezone is not set or is invalid, reports and CSV exports default to UTC.
- Payment features are unavailable until Stripe is connected.
- QuickBooks invoice sync is disabled unless you explicitly configure QuickBooks settings.
- AI settings (system message, rules, chat prompt) accept free-form text with no length limit enforced in the interface.
- Two workflow roles can share the same display rank, which may result in unpredictable ordering.

## Related Features

- [Case Management](./case-management.md) — custom statuses drive case progression; workflow templates define case structure.
- [Staff Management](./staff-management.md) — workflow roles and system roles are defined in settings.
- [Reporting](./reporting.md) — firm timezone, custom statuses, and workflow roles affect report output.
