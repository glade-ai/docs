# Client Records

## Overview

Client records track the relationship between a client and your firm on Glade. Each record is specific to your firm — the same person can be a client of multiple firms with separate records for each. You manage client records through the **Members** section of your dashboard.

## Key Behaviors

- A client record is created when someone connects with your firm — through signup, form submission, booking, or when you manually add them.
- Each record links a specific person to your firm, establishing them as your client.
- Client records store personal details including address, date of birth, SSN, and communication preferences (broadcast opt-in, SMS opt-in).
- From a client's detail view, you can see their total dollar value, active subscriptions, order history, invoices, payment methods, cases, documents, questionnaires, and associated workflows.
- Clients are classified as **Subscribed**, **Free**, or **Unverified** based on whether they have an active subscription and have verified their account.
- The member list supports filtering by these classifications and searching by name, email, phone number, or the content of a client's profile notes.
- You can edit a client's name, email, phone number, date of birth, SSN, and address through the **Edit Contact** modal.
- Follow-up cadence settings can be configured per client to control how frequently automated reminders are sent.
- **Stopping follow-ups is recorded and attributed.** When someone at your firm turns off automated follow-ups for a client, Glade records who stopped them and when, and shows that on the client's record — so a client who has gone quiet is not a mystery about whether anyone decided to stop chasing them. See [Stopping and resuming client follow-ups](#stopping-and-resuming-client-follow-ups) below.
- When a client makes a payment through Stripe, their payment profile is linked to the client record automatically.
- QuickBooks customer IDs can also be linked for accounting integration.

### Stopping and resuming client follow-ups

Automated follow-ups to a client can be turned off — for example when the client has asked for space, or when a case is being handled outside the normal cadence. Glade keeps a record of that decision rather than leaving it as an unattributed setting.

- **Who and when** — the team member who stopped follow-ups and the time they did it are saved with the client record, and the current stop is visible on the client's detail view. Anyone picking the client up later can see the decision was made deliberately and by whom.
- **Recorded on every case** — an entry is added to the activity history of each of the client's current cases at the moment follow-ups are stopped, naming the person who stopped them. The decision is visible from the case, not only from the client record.
- **No duplicate entries** — re-saving the client without changing the setting does not add another entry. Only an actual change to the setting is recorded.
- **History is kept when follow-ups resume** — turning follow-ups back on clears the current stop, but the earlier entries stay in the cases' activity history, so a client who was paused and later resumed keeps a readable trail of both.

## Configuration

- **Follow-up cadence**: Override your firm's default follow-up schedule for a specific client. Includes the interval (e.g., every 3), units (days, weeks), and percentage. When set, these override the firm-level defaults for that client only.
- **Broadcast opt-in**: Controls whether the client receives broadcast messages from your firm. On by default.
- **SMS opt-in**: Controls whether the client receives SMS notifications.

## Edge Cases & Limitations

- Duplicate client records can occasionally be created if the same person connects through different flows. When duplicates exist, the record linked to a Stripe payment profile is preferred.
- Archiving a client is blocked if they have active cases, upcoming bookings, active subscriptions, unpaid invoices, or pending payments. All of these must be resolved first.
- When you archive a client, their open tasks are completed and their conversations with your firm are archived. The client record itself is preserved for historical reference.
- The activity entries recording a follow-up stop are written to the client's cases that exist at that moment. A case started afterwards does not receive a backdated entry, though the client record still shows that follow-ups are stopped.
- Follow-ups stopped before this was recorded show no attribution — the setting is in effect, but there is no record of who turned it off or when.

## Related Features

- [Contacts](contacts.md)
- [Communication History](communication-history.md)
- [Notes](notes.md)
