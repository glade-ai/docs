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

### Who pays for the course

Your firm chooses whether it pays for credit counseling or the client does. The choice is made once per firm, per counseling provider, and every firm starts out paying for counseling itself — no existing arrangement changes unless you change it.

- **Firm-paid** (the default): counseling is billed to your firm, and it appears on your firm's regular Glade billing as before. The client is enrolled directly with no payment step.
- **Client-paid**: the client buys the course themselves before they are enrolled, and it is left off your firm's billing entirely.

### The client's purchase step

When your firm has chosen client-paid counseling, the client's credit counseling step asks them to buy the course before enrollment rather than enrolling them straight away.

- The step shows the course being purchased and its current price, so the client sees what they are paying for before they commit.
- The step explains that the combined pre-filing and post-filing course is paid for by credit or debit card, and that this charge is separate from the firm's legal fees. This distinction matters: the course fee is not a legal fee and is not covered by a retainer or a payment plan on the firm's invoice.
- The client completes the purchase through Glade's checkout, which opens in a new tab, and is returned to their case afterwards.
- Enrollment is requested once the purchase is complete. Glade confirms the purchase belongs to that client and covers the course being requested before the client is enrolled, so a mismatched or unrelated payment does not enroll them.
- Everything after enrollment — the course link, the certificate, and how the certificate is attached to the case — works exactly as it does for firm-paid counseling.

## Configuration

- **Certificate uploads** accept PDF files only.
- The certificate upload section is shown per debtor and only while that debtor is still missing a certificate; it is hidden once the step is completed or skipped.
- **Who pays** — set per counseling provider in your firm's provider settings, as either firm-paid or client-paid. Firms that have not changed it are firm-paid.

## Edge Cases & Limitations

- The firm certificate upload and the skip option are available only to firm staff in the dashboard. Clients do not see the upload section in their portal.
- The **Skip task** option only appears for a debtor whose enrollment has failed and only for team members who are allowed to skip tasks. It does not appear for steps that are already completed or skipped.
- Client-paid checkouts that were charged but never recorded before this was corrected do not repair themselves. If a client paid for a course and still cannot start it, contact Glade to have the purchase applied.
- Client-paid counseling has to be paid by credit or debit card. It cannot be added to the firm's invoice, put on a payment plan, or paid by bank transfer.
- Whether the client pays is a firm-wide setting per provider, not a per-case one. A firm cannot have some cases client-paid and others firm-paid for the same provider.
- Client-paid counseling has to be set up before a client reaches the step. Switching a firm to client-paid does not add a purchase step to a client who has already been enrolled.

## Related Features

- [Status Tracking](./status-tracking.md)
- [Document Collection](./document-collection.md)
- [Task Templates](./task-templates.md)
- [Credit Counseling & Debtor Education Integration](../integrations/abacus-credit-counseling.md) — provider setup, enrollment, and certificates.
