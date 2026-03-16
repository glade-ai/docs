# Client Portal

## Overview

The client portal is where clients interact with your firm's workflows. Clients access the portal through a link you send them and can view and complete assigned tasks including questionnaires, document uploads, invoices, bookings, and messaging.

## Key Behaviors

- Clients reach the portal through a link you share or through a workflow landing page that describes the workflow and provides an entry point.
- The portal URL is branded to your firm using your unique URL slug (e.g., `yourfirm.glade.app/...`).
- Clients start a workflow by following a link that walks them through the workflow's initial steps.
- Each workflow step can include questionnaires, document collection, payments, bookings, e-signatures, and messaging.
- Clients sign up or sign in through the portal. Each client is associated with your firm's account.
- You can configure workflow steps to automatically assign tasks to yourself or to the client, so tasks are ready as soon as a workflow starts.
- The portal includes a branded "Client login portal" accessible from your public page.

## Configuration

- You configure the portal experience through workflow templates that define the sequence of steps, triggers, and actions.
- Workflow landing pages are available for specific practice areas (e.g., bankruptcy, immigration, personal injury) and describe the workflow before a client begins.
- Products control pricing and sale state (free, not for sale, or on sale) for workflows that require payment.
- Followup reminders can be configured on questionnaire templates and document request templates with a customizable frequency (minutes, hours, days, or weeks) to remind clients of pending tasks.

## Edge Cases & Limitations

- The portal uses your firm's URL slug for routing. If you change your slug, existing links sent to clients stop working.
- Workflow initiation requires a specific step link; there is no generic "start workflow" entry point.
- Unverified users (clients who have not confirmed their account) may have limited portal functionality.

## Related Features

- [Case Questionnaire](./case-questionnaire.md)
- [Document Collection](./document-collection.md)
- [Webforms](./webforms.md)
