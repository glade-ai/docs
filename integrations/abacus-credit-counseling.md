# Abacus Credit Counseling Integration

## Overview

Glade integrates with Abacus so attorneys can enroll bankruptcy clients in pre-filing credit counseling without leaving the platform. The integration replaces the manual step of opening Abacus's portal, re-typing client information, and copying the course link back into Glade. Enrollment, the course link, and the completion certificate all flow through the workflow step assigned to the client.

## Key Behaviors

### Setting up the integration

- Attorneys connect their firm to Abacus from the integrations area of the dashboard. The setup flow registers the firm with Abacus and stores the credentials needed to enroll clients.
- Once connected, a workflow can include a credit counseling step that uses Abacus.

### Enrolling a client

- When a credit counseling step runs, the client (or the attorney's team) opens the credit counseling pane on that workflow step.
- The enrollment form is prefilled from the case record — primary debtor name, date of birth, address, phone, email, and spouse details on joint filings. Names fall back to the client profile when the case data does not have first and last name split out.
- Phone numbers that include a leading country code (for example, `+1 (312) 555-1234`) are accepted — the country code is stripped automatically before submission.
- The district code field shows examples of valid codes (such as `ILN`, `NE`, `TXN`). Abbreviations like `NEB` are rejected by Abacus and should not be used.
- For joint filings, spouse first name, last name, SSN last four, and date of birth are required before the form can be submitted.
- On submission, Glade sends the enrollment to Abacus and stores the course URL returned for the client.

### Completing the course

- The pane updates to show the assigned course link as soon as enrollment succeeds. The client can launch the course from inside Glade.
- When Abacus posts back a certificate of completion, Glade attaches the PDF to the case automatically and marks the credit counseling record complete. Primary and spouse certificates appear as separate download links.
- Joint filings are not marked complete until certificates for every enrolled debtor have been received.

### Permissions

Each credit counseling record has its own permission list. The attorney's team manages which client-portal users can view and act on the record — for example, when only one spouse should see and complete the course.

## Configuration

| Setting | Description |
|---------|-------------|
| Firm Abacus connection | Set up once per firm from the dashboard integrations area. |
| Workflow step | Add a credit counseling step to a workflow template so it runs as part of intake. |
| Permissions | Per-record control of which portal users see the enrollment and certificates. |

## Edge Cases & Limitations

- The integration is for U.S. bankruptcy credit counseling only.
- Workflows created before per-case case data was always available still prefill the enrollment form — the form falls back to the workflow's own data store when no case ID is set.
- If a debtor is re-enrolled in Abacus's test environment, Glade reuses the same Abacus client ID by reassigning it from any completed record that still held it. This has no effect in production because Abacus issues unique IDs for real enrollments.
- District codes must match Abacus's expected format. Invalid codes are rejected at enrollment time with an error from Abacus.

## Related Features

- [Workflows](../workflows/README.md)
- [Document Collection](../workflows/document-collection.md)
- [Client Portal](../intake/client-portal.md)
