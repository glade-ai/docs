# Client Portal

## Overview

The client portal is the customer-facing interface where clients interact with their creator's (legal professional's) workflow. Clients access the portal via a creator-scoped URL (`/{creatorSlug}/...`) and can view and complete assigned tasks including form requests (questionnaires), document uploads, invoices, bookings, and messaging. The portal is part of the `noodle-frontend` Next.js application.

## Key Behaviors

- Clients reach the portal through a link sent by the creator or through the workflow template landing page (`/workflow-templates/{slug}`), which describes the workflow and provides an entry point.
- The portal URL structure is `/{creatorSlug}/...` with sub-routes for form requests, document requests, invoices, documents, custom terms, and workflow initiation.
- Clients initiate a workflow via `/{creatorSlug}/initiate-workflow/{stepId}`, which walks them through the workflow's trigger steps.
- Each workflow step can include form requests (questionnaires), document collection, payments, bookings, e-signatures, and messaging.
- Authentication is handled via sign-up/sign-in modals; clients are identified by a `Person` entity and associated with a `Customer` per creator.
- Creators can auto-assign themselves or the customer to tasks in workflows via configuration on form request templates and document request templates (`autoAssignCreatorInWorkflows`, `autoAssignCustomerInWorkflows`).
- The portal provides a "Client login portal" as a branded entry point, accessible from the creator's public page.

## Configuration

- Creators configure their portal through workflow templates that define the sequence of steps, triggers, and actions.
- Workflow template landing pages are available at `/workflow-templates/{slug}` and include practice-area-specific variants (e.g., bankruptcy, immigration, personal injury).
- Products control pricing and sale state (`free`, `not_for_sale`, `on_sale`) for workflows that require payment.
- Followup cadences (frequency and units: minutes, hours, days, weeks) can be configured on form request templates and document request templates to remind clients of pending tasks.

## Edge Cases & Limitations

- The portal relies on the creator slug for routing; if a creator changes their slug, existing links break.
- Workflow initiation requires stepping through a specific step ID; there is no generic "start workflow" entry point without a step reference.
- The `Person` entity tracks both verified and unverified users; unverified users may have limited portal functionality.

## Related Features

- [Case Questionnaire](./case-questionnaire.md)
- [Document Collection](./document-collection.md)
- [Webforms](./webforms.md)
