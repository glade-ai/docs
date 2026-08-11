# Credit Counseling

## Overview

Pre-filing credit counseling is a required step in bankruptcy workflows: each debtor must complete an approved credit counseling course and produce a certificate before the case can be filed. The credit counseling pane tracks this step for every debtor on the case, whether counseling was arranged through Glade or completed elsewhere. Firm staff manage the step from the dashboard; clients complete their counseling and see the step's status in their portal.

## Key Behaviors

- The credit counseling step is tracked **per debtor**, so a joint case shows a separate status and certificate for each filer.
- When a debtor completes counseling, their certificate is attached to the step and the step is marked complete.
- **Firm certificate upload**: When a debtor already holds a valid certificate that isn't reflected in Glade — for example, they completed counseling outside Glade, or the certificate never arrived automatically — firm staff can upload it directly from the credit counseling pane. An **"Already have a certificate?"** section appears for any debtor still missing a certificate; uploading the file attaches it and closes the step. The pane refreshes to show the completed state once the upload succeeds.
- **Skipping a failed step**: If a debtor's counseling enrollment fails (shown as "Enrollment failed"), firm staff can skip the step so the workflow can move forward. A **Skip task** option appears on the failed step; confirming it marks the step skipped and the case can continue. Without this, a failed enrollment would leave the step stuck with no way to progress.
- **A client-paid course unlocks as soon as the payment goes through.** When the client pays for their own credit counseling course and the checkout completes at the standard price with no discount applied, the purchase is recorded and the client can start the course. Previously a checkout of this kind was charged successfully but not recorded, so enrollment stayed blocked and the client was left unable to begin a course they had already paid for.
- Completing or skipping the step updates the case's tasks and progress like any other workflow step. See [Status Tracking](./status-tracking.md).
- **Post-filing debtor education certificates** attach the same way as pre-filing counseling certificates, for each debtor separately. **Debtor Education Certificate (Debtor 1)** and **Debtor Education Certificate (Debtor 2)** are available as document types, so a certificate can be filed under its own name rather than under a generic type. On some cases, attaching a debtor education certificate previously failed with an error and the certificate could not be recorded against the step at all.
- Debtor education is a post-filing course, so its certificate is not part of the initial petition filing package. It is stored on the case and filed separately.

## Configuration

- **Certificate uploads** accept PDF files only.
- The certificate upload section is shown per debtor and only while that debtor is still missing a certificate; it is hidden once the step is completed or skipped.

## Edge Cases & Limitations

- The firm certificate upload and the skip option are available only to firm staff in the dashboard. Clients do not see the upload section in their portal.
- The **Skip task** option only appears for a debtor whose enrollment has failed and only for team members who are allowed to skip tasks. It does not appear for steps that are already completed or skipped.
- Client-paid checkouts that were charged but never recorded before this was corrected do not repair themselves. If a client paid for a course and still cannot start it, contact Glade to have the purchase applied.

## Related Features

- [Status Tracking](./status-tracking.md)
- [Document Collection](./document-collection.md)
- [Task Templates](./task-templates.md)
