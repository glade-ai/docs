# Settings

## Overview

Settings encompass the creator-level configuration that controls how the back office behaves. This includes custom workflow statuses, workflow roles, workflow templates, payment and billing configuration, notification preferences, AI settings, branding, and third-party integrations (Stripe, QuickBooks, PACER). Settings are scoped per creator and managed through the dashboard.

## Key Behaviors

### Custom Statuses

- Creators define workflow statuses that cases progress through. Each status has a `slug` (unique per creator), `title`, `icon` (from a fixed set of icon names), and `colour`.
- Two behavioral flags control special behavior: `usesArchiveBehavior` (treats cases in this status as archived) and `disablesFollowups` (stops automated follow-up reminders for cases in this status).
- A set of default statuses is provisioned when a creator is set up, including Data Collection, Processing, Filed and Pending, Completed, Archived, Retainer Sent, and others. Default status slugs are protected from certain operations.
- Status slugs are generated via `generateUniqueSlug` to ensure uniqueness within a creator.

### Workflow Roles

- Creators define named roles (e.g., "Paralegal", "Documents Team") that team members can be assigned to. Each role has a `name`, `creatorId`, and `rank` for display ordering.
- Workflow roles are used to segment team members in reports and to determine default case assignment behavior via `TeamMember.defaultWorkflowRoleId`.

### Workflow Templates

- Workflows define the template for a case: steps, contexts, invoices, owner assignments, and fee structure.
- Key workflow settings include `isLocked`, `isArchived`, `isEnabled`, `enableUscisUpdates`, `enablePacerSubmissions`, `sendEmailToCreatorOnCompletion`, `sendEmailToCreatorOnFirstPayment`, `canInitiateAssociatedWorkflows`, and `preserveWorkflowAssignment`.
- Workflows have a `state` of `current`, `draft`, or `stale`, and a `version` integer for tracking revisions.
- The `noodleFee` field sets the platform fee percentage, and `estimatedTotalFees` provides an optional fee estimate displayed to clients.
- Workflows have a `type` of `basic` or `attorney-case`, and an optional `caseType` for categorization.

### Payment & Billing

- `defaultCurrency` sets the creator's currency for payments and invoices.
- `stripeAccountId` and `stripeAccountType` (Connect, Express, or NoodleMOR) control Stripe integration.
- `statementDescriptor` sets the text that appears on client bank/card statements.
- `noodleApplicationFee` sets the platform application fee at the creator level.
- **QuickBooks settings** (`QuickBooksSettings`) control when invoices are synced to QuickBooks: never (`None`), when payable (`Payable`), or on first payment (`FirstPayment`).
- `confidoFirmId` and `confidoFirmToken` configure the Confido payment integration.

### Notifications

- `chatMessageNotification` controls how the creator is notified of chat messages: via SMS or not at all.
- `notifyOnEveryCustomerMessage` sends a notification for every customer message when enabled.
- `notificationPhoneNumber` is the phone number used for SMS notifications.
- `slackChannelId` configures Slack integration for notifications.
- `creatorSupportEmail` and `creatorSupportEmailSenderName` customize the sender for outbound emails.
- `creatorCustomConfirmationEmailMessage` allows custom text in payment confirmation emails.

### AI Settings

- `isAiEnabled` toggles AI features for the creator.
- `chatPrompt` and `chatWelcomeMessage` configure the AI chat experience for clients.
- `aiSystemMessage` and `aiRules` provide system-level instructions for AI behavior.

### Branding

- `primaryColour` sets the creator's brand color (7-character hex).
- `logoForBrandingId` and `logoCompactId` reference `Asset` records for the creator's logos.
- `creatorDomain` sets a custom domain for the creator's public-facing pages.
- `hasCustomOgImage` indicates whether a custom Open Graph image is configured.
- `successPaymentRedirectUrl` sets where clients are redirected after successful payment.

### Followup Cadence

- `followupCadence` (integer), `followupCadenceUnits` (e.g., days, weeks), and `followupCadencePercentage` configure automated follow-up reminders for outstanding client tasks.

### Credit Reports

- `creditReportPullAttemptLimit` sets the maximum number of credit report pull attempts.
- `creditReportIndividualCustomPrice` and `creditReportJointCustomPrice` allow custom pricing for credit report pulls (overriding defaults).

## Configuration

Settings are primarily configured through the dashboard account page and individual workflow settings pages. Most settings are stored directly on the `Creator` entity. QuickBooks settings are in a separate `QuickBooksSettings` entity keyed by `creatorId`.

## Edge Cases & Limitations

- Custom status slugs must be unique per creator but are not globally unique. The slug generation utility handles deduplication within a creator scope.
- The `timezone` field on `Creator` is a free-form string. Invalid timezone values cause the system to fall back to UTC in reporting contexts, but no validation is enforced at the entity level.
- `stripeAccountType` is nullable, meaning creators may exist without a configured payment provider. Payment-related features are unavailable until Stripe is set up.
- QuickBooks settings are optional; if no `QuickBooksSettings` record exists for a creator, invoice sync is disabled.
- AI settings (`aiSystemMessage`, `aiRules`, `chatPrompt`) accept arbitrary strings with no length validation at the entity level.
- Workflow role rank values are integers but uniqueness is not enforced, so two roles can share the same rank.

## Related Features

- [Case Management](./case-management.md) — custom statuses drive case progression; workflow templates define case structure.
- [Staff Management](./staff-management.md) — workflow roles and system roles are defined in settings.
- [Reporting](./reporting.md) — creator timezone, custom statuses, and workflow roles affect report output.
