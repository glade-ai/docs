# Credit Counseling & Debtor Education Integration

## Overview

Glade integrates with outside education providers so attorneys can enroll bankruptcy clients in the two courses required for discharge — pre-filing credit counseling (Course 1) and post-filing debtor education (Course 2) — without leaving the platform. Pre-filing credit counseling runs through Abacus; post-filing debtor education runs through Sage. Glade selects the right course and provider automatically based on whether the client's case has been filed yet, so the attorney's team uses the same credit counseling step for both. The integration replaces the manual step of opening the provider's portal, re-typing client information, and copying the course link back into Glade. Enrollment, the course link, and the completion certificate all flow through the workflow step assigned to the client.

## Key Behaviors

### Setting up the integration

- Attorneys connect their firm to Abacus from the integrations area of the dashboard. The setup flow registers the firm with Abacus and stores the credentials needed to enroll clients.
- Connecting, updating, or disconnecting the integration requires the firm admin role. Viewing whether the integration is connected does not — any team member on the firm can open the credit counseling integration settings and see its connection status. Previously this status check was limited to admins, so non-admin team members hit a permissions error even when they were only checking whether the firm was connected.
- The same connection covers post-filing debtor education through Sage — there is no separate Sage setup to complete.
- Abacus is not the only pre-filing credit counseling provider. A firm can instead connect **Evergreen Financial Counseling** for pre-filing credit counseling; see [Evergreen Credit Counseling](./evergreen-credit-counseling.md). The credit counseling step works the same way regardless of which provider the firm has connected.
- Once connected, a workflow can include a credit counseling step. The same step handles both pre-filing credit counseling and post-filing debtor education.

### Enrolling a client

- When a credit counseling step runs, the client (or the attorney's team) opens the credit counseling pane on that workflow step. When the firm has the integration connected, triggering the step also sends the enrollment request to the client automatically — the team no longer has to open the step and send it by hand, and the client receives the enrollment form right away. If no provider is connected, the step behaves as before and the enrollment is sent manually.
- Glade picks the course type and provider automatically: before the case is filed, the client is enrolled in pre-filing credit counseling through Abacus; once the case has been filed, the client is enrolled in post-filing debtor education through Sage. The team does not choose the provider.
- The credit counseling row shows the course type in its label — **Get Pre-Filing Credit Counseling** for pre-filing counseling and **Get Post-Filing Debtor Education** for post-filing debtor education — so it is clear which course is being requested. A **Skip** control sits inline on the row for steps that do not apply.
- Enrolling a client carries a flat enrollment fee of $25, billed to the firm and shown on the credit counseling pane before the enrollment is sent.
- **A client who already has a valid certificate on file is not enrolled again.** When the case already holds a credit counseling certificate that has not passed its 180-day validity window — whether it came through Glade or was attached from an outside provider — the credit counseling step does not send an enrollment request, does not create the enrollment task, does not post the enrollment message to the client, and is not billed. Any enrollment task already sitting open on the case is closed. This prevents a client who arrives with their own certificate from being asked to take, and the firm from paying for, a course they have already completed.
- On joint filings, this is assessed per debtor, so a case where only one spouse has a certificate on file still enrolls the other.
- An expired certificate does not count. If the certificate on file is more than 180 days old, enrollment proceeds normally.
- The enrollment form is prefilled from the case record — primary debtor name, date of birth, address, phone, email, and spouse details on joint filings. Name, email, and phone fall back to the client profile when those values are missing from the case record (common for newly added clients).
- Phone numbers that include a leading country code (for example, `+1 (312) 555-1234`) are accepted — the country code is stripped automatically before submission.
- The client's federal district is determined automatically from their address — there is no district field to fill in. Glade resolves it behind the scenes, falling back to the address ZIP code when needed, which covers the large majority of clients.
- For joint filings, spouse first name, last name, SSN last four, and date of birth are required before the form can be submitted.
- On submission, Glade sends the enrollment to the provider and stores the course link returned for the client.

### Completing the course

- The pane updates to show the assigned course link as soon as enrollment succeeds. The client can launch the course from inside Glade.
- When the provider posts back a certificate of completion, Glade attaches the PDF to the case automatically and marks the record complete. This works the same way for pre-filing credit counseling and post-filing debtor education. Primary and spouse certificates appear as separate download links.
- The certificate also appears in the workflow's Documents tab and is automatically included in the bankruptcy petition filing package, mapped to the credit counseling document slot — so it is ready to file without re-uploading.
- Joint filings are not marked complete until certificates for every enrolled debtor have been received.

### The completion date on the certificate

The date the client actually finished the briefing is read off the certificate and recorded on the case, separately for the primary debtor and the spouse.

- Previously the date on record was the moment the certificate reached Glade rather than the date printed on it. For a briefing completed through a provider outside Glade and attached to the case later, the two can be months apart — and for an externally attached certificate there was no completion date on record at all.
- This applies both to certificates the provider posts back and to certificates your team attaches from outside Glade. Which debtor a certificate belongs to is taken from the record it was filed against, so a spouse's certificate is recorded against the spouse.
- If a debtor re-takes a briefing whose certificate had expired, the newer certificate's date replaces the older one on the case.
- Pre-filing credit counseling and post-filing debtor education certificates are both attached the same way, but only the pre-filing briefing's completion date is used for the pre-filing checks below.
- Certificates already on file before this became available keep the date Glade recorded when they arrived. Re-run the extraction on a certificate if you need the printed date picked up.

### Certificate recency before filing

Because a pre-filing briefing must be completed within 180 days of the petition being filed, the pre-filing review checks each debtor's certificate date before a filing can be submitted.

- A briefing completed more than 180 days ago is raised as a **blocking** finding — the filing does not proceed until an attorney reviews and signs off on it.
- A briefing that is inside the 180 days but nearing the end of it is raised as an **advisory** finding, so you can see a certificate that is about to expire while there is still time to have the client re-take the course. Advisories do not block a filing.
- On joint filings, each debtor's certificate is checked separately, so one debtor's expired briefing is reported on its own.
- Where the printed date could not be read off a certificate, the date Glade received it is used for the check instead.

> TODO: Confirm these recency and expiring-soon checks are switched on in production. They ship as part of the pre-filing review rule set, which is enabled per environment, and an earlier rollout deliberately held the credit counseling checks back.

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
- In rare cases where the client's district cannot be determined from their address automatically, enrollment may need a corrected or more complete address before it can be sent. Coverage is extended as gaps are found — Jacksonville and the rest of Duval County, Florida were recently added, so clients at those addresses no longer fail to enroll because their district could not be resolved.
- A certificate uploaded to the wrong case or for the wrong course cannot be removed by your team. Contact Glade support to have it cleared so the correct certificate can be attached.

## Related Features

- [Workflows](../workflows/README.md)
- [Document Collection](../workflows/document-collection.md)
- [Client Portal](../intake/client-portal.md)
