# Contacts

## Overview

Contacts are the people (persons) that a creator interacts with on the Glade platform. The contacts system encompasses individual person records, company records, and associated user relationships. Creators view and manage their contacts through the dashboard "Members" tab, which lists all people who have a customer relationship with that creator.

## Key Behaviors

- The contacts list displays all people linked to a creator through customer records, sorted and filterable by subscription status, verification state, and search terms.
- Each person record stores core identity fields: name, email, phone number, contact phone number, date of birth, preferred language, address, and profile photo.
- Persons have one of three roles: `admin`, `creator`, or `customer`.
- Companies are separate entities scoped to a creator, storing a company name, email, phone number, point of contact, and a randomly generated display color. Companies can have employees linked through a `company_employees` join table.
- Companies support CRUD operations: list (with search by name), create, read by ID, and update. All company operations require creator authorization.
- Associated users represent relationships between people (e.g., family members sharing a legal matter). The association is bidirectional -- when person A is associated with person B, person B is also associated with person A, and all existing associations are transitively linked.
- New associated users can be created by providing a name and email. If the email matches an existing user, the association is only allowed if the user is not already associated. If the email is new, a person record with the `customer` role is created.
- The member detail view provides tabs for information, conversation, documents, forms, workflows, invoices, order history, payment methods, AI follow-up cadence, and notes.
- Recent members are tracked in the frontend (up to 5) and displayed for quick access.

## Configuration

- **Member list filters**: `all`, `subscribed_members`, `free_members`, `unverified_contacts`. Additional status-based filters exist for legal workflow states (retained, booked consultation, filed case).
- **Sort options**: Applied to the member list query to control ordering.
- **Search**: Filters members by name, email, or phone number.

## Edge Cases & Limitations

- Person email and phone number columns have unique constraints. When these need to change (e.g., deduplication), the old values are stored in a `backupAuthData` text field.
- The `archivedAt` timestamp on a person record acts as a soft archive for contacts. Archived persons are excluded from the standard member list.
- Company employee associations are stored separately from the person-to-person `associated_users` relationship. These are two distinct concepts.
- The contacts list query joins through the `customers` table, so a person only appears in a creator's contacts if a customer record exists for that (person, creator) pair.

## Related Features

- [Client Records](client-records.md)
- [Communication History](communication-history.md)
- [Notes](notes.md)
