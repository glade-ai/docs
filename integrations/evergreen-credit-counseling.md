# Evergreen Credit Counseling Integration

## Overview

Glade connects to Evergreen Financial Counseling so firms can enroll bankruptcy clients in required credit counseling without leaving the platform. Evergreen is an alternative pre-filing credit counseling provider to Abacus: a firm connects its Evergreen account once from the integrations area, and from then on credit counseling enrollments and course links can run through Evergreen. Enrollment, the course link, and the completion certificate flow through the same credit counseling workflow step described in [Credit Counseling & Debtor Education](./abacus-credit-counseling.md).

## Key Behaviors

### Connecting Evergreen

- Attorneys connect their firm to Evergreen from the integrations area of the dashboard, where Evergreen appears as its own tile ("Evergreen Financial Counseling") alongside Abacus.
- The connect screen offers two ways to set up the firm:
  - **I have an attorney code** — enter the firm's existing Evergreen attorney code and attorney name, then save.
  - **Register a new attorney** — enter the firm name, attorney first and last name, and the firm's address (street, city, state, ZIP) to register the firm with Evergreen directly from Glade.
- Once connected, the tile shows a **Settings** action and the Evergreen logo so it is easy to recognize in the integrations list. If connecting or registering fails, the screen stays open and shows a message so the details can be corrected and retried.

### Managing the connection

- Opening **Settings** for a connected firm shows the saved attorney code partially masked (only the last four characters are shown) and a **Remove** button to disconnect the firm from Evergreen.

### Enrolling a client and completing the course

- When a credit counseling step runs for a firm connected to Evergreen, enrollment and course delivery work the same way as with other providers: the client receives the enrollment, launches the course from inside Glade through the course link, and the completion certificate flows back to the case. See [Credit Counseling & Debtor Education](./abacus-credit-counseling.md) for the full enrollment, certificate, and permissions behavior.
- Each enrolled person sees their own course link. Glade shows the signed-in user their own assigned link; otherwise it shows the primary debtor's link.

### Debtor education opens when the case is filed

Most Evergreen workflow templates have only one credit counseling step, for the pre-filing briefing, so clients were previously never asked to take the post-filing debtor education course. Glade now opens that second course on its own.

- When a case is filed — or a case number is recorded on it — and the client has enrolled in the Evergreen pre-filing briefing, Glade opens post-filing debtor education for the client. The client receives the **Get Post-Filing Debtor Education** enrollment task and a chat message, just as they would from a workflow step.
- No template changes are needed. If a template does include a later credit counseling step for debtor education, that step attaches to the course already opened instead of sending the client a second request.
- The second course is enrolled under the same Evergreen client record as the briefing, rather than creating a new client at Evergreen.
- Debtor education opens once per case. Filing events that repeat, or a case number being corrected, do not send the client another request.
- On firm-paid counseling, your firm is charged for debtor education when the client enrolls, as its own line item — not when the course is opened. See [When firm-paid counseling reaches your bill](../workflows/credit-counseling.md#when-firm-paid-counseling-reaches-your-bill).

## Configuration

| Setting | Description |
|---------|-------------|
| Firm provider connection | Set up once per firm from the dashboard integrations area, either with an existing Evergreen attorney code or by registering the firm with Evergreen. |
| Disconnect | Remove the Evergreen connection at any time from the integration's **Settings** screen. |

## Edge Cases & Limitations

- The integration is for U.S. bankruptcy credit counseling.
- Evergreen is an alternative to Abacus for pre-filing credit counseling. The provider that handles a given enrollment is determined by the firm's connected provider.
- If connecting or registering fails, the setup screen stays open with an error message so the firm can correct the details and try again.
- Debtor education opens automatically only for a filed case whose client has already enrolled in the Evergreen pre-filing briefing. A case with no Evergreen briefing, or with no case number, is left alone. If the briefing enrollment happens after filing, debtor education opens once that enrollment succeeds.
- Clearing a case number does not open debtor education.

> TODO: Confirm whether clients on cases filed before this change have been sent the debtor education request yet. Existing filed cases are picked up by a one-time catch-up rather than automatically.

> TODO: Confirm against the backend whether Evergreen enrollments share the same $25 enrollment fee, automatic certificate attachment to the filing package, and automatic district detection documented for Abacus/Sage. These behaviors are likely shared (the credit counseling step is provider-neutral) but were not verified for Evergreen specifically.

## Related Features

- [Credit Counseling & Debtor Education](./abacus-credit-counseling.md)
- [Workflows](../workflows/README.md)
- [Client Portal](../intake/client-portal/README.md)
