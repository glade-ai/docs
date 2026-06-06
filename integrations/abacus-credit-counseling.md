# Credit Counseling & Debtor Education Integration

## Overview

Glade integrates with outside education providers so attorneys can enroll bankruptcy clients in the two courses required for discharge — pre-filing credit counseling (Course 1) and post-filing debtor education (Course 2) — without leaving the platform. Pre-filing credit counseling runs through Abacus; post-filing debtor education runs through Sage. Glade selects the right course and provider automatically based on whether the client's case has been filed yet, so the attorney's team uses the same credit counseling step for both. The integration replaces the manual step of opening the provider's portal, re-typing client information, and copying the course link back into Glade. Enrollment, the course link, and the completion certificate all flow through the workflow step assigned to the client.

## Key Behaviors

### Setting up the integration

- Attorneys connect their firm to Abacus from the integrations area of the dashboard. The setup flow registers the firm with Abacus and stores the credentials needed to enroll clients.
- The same connection covers post-filing debtor education through Sage — there is no separate Sage setup to complete.
- Once connected, a workflow can include a credit counseling step. The same step handles both pre-filing credit counseling and post-filing debtor education.

### Enrolling a client

- When a credit counseling step runs, the client (or the attorney's team) opens the credit counseling pane on that workflow step.
- Glade picks the course type and provider automatically: before the case is filed, the client is enrolled in pre-filing credit counseling through Abacus; once the case has been filed, the client is enrolled in post-filing debtor education through Sage. The team does not choose the provider.
- The enrollment form is prefilled from the case record — primary debtor name, date of birth, address, phone, email, and spouse details on joint filings. Names fall back to the client profile when the case data does not have first and last name split out.
- Phone numbers that include a leading country code (for example, `+1 (312) 555-1234`) are accepted — the country code is stripped automatically before submission.
- The client's federal district is determined automatically from their address — there is no district field to fill in. Glade resolves it behind the scenes, falling back to the address ZIP code when needed, which covers the large majority of clients.
- For joint filings, spouse first name, last name, SSN last four, and date of birth are required before the form can be submitted.
- On submission, Glade sends the enrollment to the provider and stores the course link returned for the client.

### Completing the course

- The pane updates to show the assigned course link as soon as enrollment succeeds. The client can launch the course from inside Glade.
- When the provider posts back a certificate of completion, Glade attaches the PDF to the case automatically and marks the record complete. This works the same way for pre-filing credit counseling and post-filing debtor education. Primary and spouse certificates appear as separate download links.
- Joint filings are not marked complete until certificates for every enrolled debtor have been received.

### Permissions

Each credit counseling record has its own permission list. The attorney's team manages which client-portal users can view and act on the record — for example, when only one spouse should see and complete the course.

## Configuration

| Setting | Description |
|---------|-------------|
| Firm provider connection | Set up once per firm from the dashboard integrations area. The same connection covers both Abacus credit counseling and Sage debtor education. |
| Workflow step | Add a credit counseling step to a workflow template so it runs as part of intake. The same step covers pre-filing credit counseling and post-filing debtor education. |
| Permissions | Per-record control of which portal users see the enrollment and certificates. |

## Edge Cases & Limitations

- The integration is for U.S. bankruptcy education only — pre-filing credit counseling (Abacus) and post-filing debtor education (Sage).
- Whether a client gets credit counseling or debtor education is driven by whether the case has been filed. A case that has not been filed yet always enrolls in pre-filing credit counseling.
- Workflows created before per-case case data was always available still prefill the enrollment form — the form falls back to the workflow's own data store when no case ID is set.
- If a debtor is re-enrolled in Abacus's test environment, Glade reuses the same Abacus client ID by reassigning it from any completed record that still held it. This has no effect in production because Abacus issues unique IDs for real enrollments.
- In rare cases where the client's district cannot be determined from their address automatically, enrollment may need a corrected or more complete address before it can be sent.

## Related Features

- [Workflows](../workflows/README.md)
- [Document Collection](../workflows/document-collection.md)
- [Client Portal](../intake/client-portal.md)
