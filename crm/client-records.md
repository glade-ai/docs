# Client Records

## Overview

Client records represent the relationship between a person (end user) and a creator (legal professional) on the Glade platform. Internally called "customers," these records are scoped per creator, meaning the same person can be a client of multiple creators with separate customer records for each. Creators manage their client records through the dashboard "Members" section.

## Key Behaviors

- A customer record is created when a person is connected to a creator, either through signup, form submission, booking, or manual creation by the creator.
- Each customer record ties a `personId` to a `creatorId`, establishing the relationship between a specific person and a specific creator's practice.
- Customer records store client-specific data including address (line1, line2, city, state, zip), date of birth, social security number, and communication preferences (broadcast opt-in, SMS opt-in).
- Creators can view a client's total dollar value, active subscriptions, order history, invoices, payment methods, workflows, documents, and form requests from the member detail view.
- Clients are classified as "Subscribed," "Free," or "Unverified" based on their subscription status and account verification state.
- The member list supports filtering by these classifications and searching by name, email, or phone number.
- Creators can edit a client's name, email, phone number, date of birth, SSN, and address through the "Edit Contact" modal.
- Follow-up cadence settings (cadence interval, cadence units, cadence percentage) can be configured per client to control AI-driven follow-up behavior.
- When a Stripe payment occurs, a Stripe customer ID is associated with the customer record to link payment processing.
- QuickBooks customer IDs can also be stored on customer records for accounting integration.

## Configuration

- **Follow-up cadence**: Per-client override of the creator's default follow-up cadence. Includes cadence interval (minimum 1), cadence units (e.g., days, weeks), and cadence percentage. When set, these override the creator-level defaults for that specific client.
- **Broadcast opt-in**: Controls whether the client receives broadcast messages from the creator. Defaults to `true`.
- **SMS opt-in**: Controls whether the client receives SMS notifications. Toggling this on emits an event that other services can listen to.

## Edge Cases & Limitations

- A person can have multiple customer records for the same creator if created through different flows, though the system attempts to find existing records first. When duplicates exist, the record with a Stripe customer ID is preferred.
- Archiving a client (soft delete) is blocked if the client has active workflows, upcoming bookings, active subscriptions, unpaid invoices, or pending payments. All of these must be resolved first.
- Archiving sets `archivedAt` on the person record and soft-deletes associated conversations and completes open tasks. It does not delete the customer record itself.
- The `canCreateOrganization` flag on the customer record controls whether the client can create an organization under the creator, but this is typically managed automatically.

## Related Features

- [Contacts](contacts.md)
- [Communication History](communication-history.md)
- [Notes](notes.md)
