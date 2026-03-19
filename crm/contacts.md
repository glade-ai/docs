# Contacts

## Overview

Contacts are the people your firm interacts with on Glade. The contacts system includes individual people, companies, and relationships between people (e.g., family members on the same legal matter). You view and manage contacts through the **Members** tab on your dashboard.

## Key Behaviors

- The contacts list shows everyone who has a client relationship with your firm, sortable and filterable by subscription status, verification state, and search terms.
- Each contact has core identity fields: name, email, phone number, date of birth, preferred language, address, and profile photo.
- **Companies** are separate records your firm can create to represent organizations. Each company stores a name, email, phone number, and point of contact. Companies can have employees linked to them.
- **Associated users** represent relationships between people — for example, family members sharing a legal matter. Associations are automatic in both directions: if you link Person A to Person B, Person B is also linked back to Person A, and all existing associations are connected transitively.
- When adding an associated user, you provide their name and email. If the email matches an existing user, they are linked directly. If the email is new, a new contact is created automatically.
- The member detail view provides tabs for: information, conversation, documents, forms, cases, invoices, order history, payment methods, AI follow-up cadence, and notes.
- Your 5 most recently viewed members are tracked for quick access.

## Configuration

- **Member list filters**: All, Subscribed, Free, Unverified. Additional filters exist for legal workflow states (retained, booked consultation, filed case).
- **Sort options**: Control the ordering of the member list.
- **Search**: Filter members by name, email, phone number, or profile notes.

## Edge Cases & Limitations

- Each email and phone number must be unique across all contacts. If a contact's email or phone needs to change (e.g., during deduplication), the old values are preserved internally.
- Archived contacts are excluded from the standard member list but are not permanently deleted.
- Company employee relationships and person-to-person associations are two separate concepts — linking someone as a company employee does not automatically create a person-to-person association.
- A person only appears in your contacts list if they have a client record with your firm.

## Related Features

- [Client Records](client-records.md)
- [Communication History](communication-history.md)
- [Notes](notes.md)
