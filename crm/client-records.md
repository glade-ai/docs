# Client Records

## Overview

Client records track the relationship between a client and your firm on Glade. Each record is specific to your firm — the same person can be a client of multiple firms with separate records for each. You manage client records through the **Members** section of your dashboard.

## Key Behaviors

- A client record is created when someone connects with your firm — through signup, form submission, booking, or when you manually add them.
- Each record links a specific person to your firm, establishing them as your client.
- Client records store personal details including address, date of birth, SSN, and communication preferences (broadcast opt-in, SMS opt-in).
- **County is part of the stored address.** A client's county is kept on their record alongside street, city, state, and ZIP, rather than being worked out again each time someone needs it. See [The client's county](#the-clients-county) below.
- From a client's detail view, you can see their total dollar value, active subscriptions, order history, invoices, payment methods, cases, documents, questionnaires, and associated workflows.
- Clients are classified as **Subscribed**, **Free**, or **Unverified** based on whether they have an active subscription and have verified their account.
- The member list supports filtering by these classifications and searching by name, email, phone number, or the content of a client's profile notes.
- You can edit a client's name, email, phone number, date of birth, SSN, and address through the **Edit Contact** modal.
- Follow-up cadence settings can be configured per client to control how frequently automated reminders are sent.
- **Stopping follow-ups is recorded and attributed.** When someone at your firm turns off automated follow-ups for a client, Glade records who stopped them and when, and shows that on the client's record — so a client who has gone quiet is not a mystery about whether anyone decided to stop chasing them. See [Stopping and resuming client follow-ups](#stopping-and-resuming-client-follow-ups) below.
- When a client makes a payment through Stripe, their payment profile is linked to the client record automatically.
- QuickBooks customer IDs can also be linked for accounting integration.

### The client's county

Which county a client lives in decides where a bankruptcy case is filed, so it is worth having on the record rather than looked up each time it is needed.

- **County is saved with the rest of the address.** When a client's address is entered — on a new booking, on a new case, or by editing the record — the county that goes with it is worked out from the address and stored on the client's record.
- Previously the county was worked out fresh every time the create-client form was opened and never kept, so nobody could see afterwards which county had been used.
- **It is only filled in where an address was captured with one.** Clients already on your books have no county recorded until their address is next saved. A blank county is not an error.
- Leaving the county out when you update a client does not wipe a county already on the record. To change it, enter the new value.
- The county is stored on the client's record for your firm, not shared to the person's records at other firms.

> TODO: Confirm whether the county is shown and editable in the **Edit Contact** modal, or only set from the address as it is entered.

### Address captured when a client books

An appointment type can be set to ask for the client's address at the point of booking. That address — street, city, state, ZIP, and county — is written to the client's record for your firm, the same record the **Members** section shows.

- The booking reads the address off the client's record rather than keeping its own copy, so a booking always shows where the client lives now and correcting an address once corrects it everywhere it appears.
- A client who moves therefore has their earlier bookings show the new address. There is no record of the address as it stood when a past booking was made.

See [Scheduling](../appointments/scheduling.md) for how the address is collected and which appointment types ask for one.

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
- County is blank on every client record until an address is saved that carries one. Existing records are not backfilled, so a firm should not read a blank county as "no county on file for this address".
- An address collected at booking is the client's one current address. Recording where a client lived at the time of an earlier booking is not supported.

## Related Features

- [Contacts](contacts.md)
- [Scheduling](../appointments/scheduling.md) — booking can collect the client's address and county onto their record
- [Communication History](communication-history.md)
- [Notes](notes.md)
