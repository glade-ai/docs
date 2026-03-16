# Client Records

## Overview

Client records track the relationship between a client and your firm on Glade. Each record is specific to your firm — the same person can be a client of multiple firms with separate records for each. You manage client records through the **Members** section of your dashboard.

## Key Behaviors

- A client record is created when someone connects with your firm — through signup, form submission, booking, or when you manually add them.
- Each record links a specific person to your firm, establishing them as your client.
- Client records store personal details including address, date of birth, SSN, and communication preferences (broadcast opt-in, SMS opt-in).
- From a client's detail view, you can see their total dollar value, active subscriptions, order history, invoices, payment methods, cases, documents, and questionnaires.
- Clients are classified as **Subscribed**, **Free**, or **Unverified** based on whether they have an active subscription and have verified their account.
- The member list supports filtering by these classifications and searching by name, email, or phone number.
- You can edit a client's name, email, phone number, date of birth, SSN, and address through the **Edit Contact** modal.
- Follow-up cadence settings can be configured per client to control how frequently automated reminders are sent.
- When a client makes a payment through Stripe, their payment profile is linked to the client record automatically.
- QuickBooks customer IDs can also be linked for accounting integration.

## Configuration

- **Follow-up cadence**: Override your firm's default follow-up schedule for a specific client. Includes the interval (e.g., every 3), units (days, weeks), and percentage. When set, these override the firm-level defaults for that client only.
- **Broadcast opt-in**: Controls whether the client receives broadcast messages from your firm. On by default.
- **SMS opt-in**: Controls whether the client receives SMS notifications.

## Edge Cases & Limitations

- Duplicate client records can occasionally be created if the same person connects through different flows. When duplicates exist, the record linked to a Stripe payment profile is preferred.
- Archiving a client is blocked if they have active cases, upcoming bookings, active subscriptions, unpaid invoices, or pending payments. All of these must be resolved first.
- When you archive a client, their open tasks are completed and their conversations with your firm are archived. The client record itself is preserved for historical reference.

## Related Features

- [Contacts](contacts.md)
- [Communication History](communication-history.md)
- [Notes](notes.md)
