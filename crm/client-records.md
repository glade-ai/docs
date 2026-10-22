# Client Records

## Overview

Client records track the relationship between a client and your firm on Glade. Each record is specific to your firm — the same person can be a client of multiple firms with separate records for each. You manage client records through the **Members** section of your dashboard.

## Key Behaviors

- A client record is created when someone connects with your firm — through signup, form submission, booking, or when you manually add them.
- Each record links a specific person to your firm, establishing them as your client.
- Client records store personal details including address, date of birth, SSN, and communication preferences (broadcast opt-in, SMS opt-in).
- **County is part of the stored address.** A client's county is kept on their record alongside street, city, state, and ZIP, rather than being worked out again each time someone needs it. See [The client's county](#the-clients-county) below.
- From a client's detail view, you can see their total dollar value, active subscriptions, order history, invoices, payment methods, cases, documents, questionnaires, and associated workflows.
- **Matters imported from MyCase are kept off the client-facing case list.** A firm that moved to Glade from MyCase carries its history across as imported matters, which are records of past work rather than cases anyone is working. They no longer appear in the case list on a contact, so the client's live case is the one your team lands on. See [Imported matters on a contact](#imported-matters-on-a-contact) below.
- Clients are classified as **Subscribed**, **Free**, or **Unverified** based on whether they have an active subscription and have verified their account.
- The member list supports filtering by these classifications and searching by name, email, phone number, or the content of a client's profile notes.
- You can edit a client's name, email, phone number, date of birth, SSN, and address through the **Edit Contact** modal.
- Follow-up cadence settings can be configured per client to control how frequently automated reminders are sent.
- **Stopping follow-ups is recorded and attributed.** When someone at your firm turns off automated follow-ups for a client, Glade records who stopped them and when, and shows that on the client's record — so a client who has gone quiet is not a mystery about whether anyone decided to stop chasing them. See [Stopping and resuming client follow-ups](#stopping-and-resuming-client-follow-ups) below.
- **Possible duplicates are flagged while you create a client.** Typing into a **Create new client** form warns you about existing clients with the same email, phone number, or full name, and lets you use the existing client instead. See [Possible duplicate clients](#possible-duplicate-clients) below.
- **The new-client form on a new case captures date of birth and an internal note.** See [Details captured when creating a new client](#details-captured-when-creating-a-new-client) below.
- **Client lists and profiles are visible only to your firm's staff.** Someone outside your firm — including a signed-in client or another firm's staff — cannot open your client list or view or edit a client's profile. A profile opens only for a person who is your firm's client, lead, or team member, or who is on one of your firm's cases.
- **Each firm keeps its own copy of a shared client's SSN.** When the same person is a client of two firms, each firm sees and edits only the SSN it entered. Saving or clearing the SSN at your firm never changes or removes the other firm's copy.
- When a client makes a payment through Stripe, their payment profile is linked to the client record automatically.
- QuickBooks customer IDs can also be linked for accounting integration.

### Possible duplicate clients

When staff create a client, Glade checks your firm's existing clients as they type and warns before a duplicate is created, so intake does not have to search the client list first.

- **What counts as a match.** An existing client is flagged when they share the exact email, phone number, or full name being entered. Matching is exact, not partial:
  - Email ignores capitalization.
  - Phone compares digits only, so formatting, spacing, and a leading US country code do not matter — `(404) 555-0134` matches `+1 404 555 0134`. Both the client's phone and contact phone are checked.
  - Name compares the whole name, ignoring capitalization and extra spaces.
- **Checks start once a value is complete enough** — a full email address, a phone number of at least 10 digits, or a name of at least two words. Partial entries are ignored rather than flagged.
- **The warning shows what matched** and lists up to five clients. Email matches come first, then clients matching on more details, then the most recently added.
- **Where it appears.** The warning shows under the phone field on the **Create new client** tab when you start a case, on the **Create new client** tab when you book an appointment, and on the **Create client** panel.
- **Use this client** on the case and booking forms selects that client. The case or booking continues on their record instead of a new one.
- **Open client** on the **Create client** panel opens that client's record. Holding Command (Mac) or Control (Windows) while clicking opens it in a new tab.
- **When more than five clients match,** the warning still lists five, and a line under the list reads **More existing clients match than are shown here.**
- Archived clients and people who are not your firm's clients are never flagged.

### Details captured when creating a new client

When you create a new case for a new client, the **Create new client** tab includes two additional fields:

- **Date of birth** — saved to the client's record and shown on their profile.
- **Internal note** — a short note, such as why the person is calling. It is saved as an internal note on the new case, where the attorney reads it, and also appears in the client's combined notes tagged with that case. It is never visible to the client and follows the usual internal note rules, including notifying anyone tagged in it. See [Internal notes in case conversations](communication-history.md#internal-notes-in-case-conversations).

- The note is optional and limited to 4,000 characters. A note that is too long stops the case from being created until it is shortened.
- If the case is created but the note could not be saved, the case still exists and you are warned that the note was not saved, so you can add it to the case instead of creating the case again.
- These fields appear only when creating a new client. Starting a case for an existing client does not offer the internal note field.

### Imported matters on a contact

Imported MyCase matters used to sit on the contact page beside the live case, and both were opened just as readily — so staff and clients alike kept working from the historical record instead of the current one.

- **The case list on a contact leaves imported matters out**, along with any imported matters related to them, so what you see there is the work in progress.
- **Your firm's case tracker is unchanged.** Imported matters are all still listed there, and the tracker can be filtered to show only them when you need the history.
- Nothing has been deleted or altered. This changes where imported matters appear, not whether they exist, and the same matters are hidden from the client in their portal.

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

See [Scheduling](../appointments/scheduling/README.md) for how the address is collected and which appointment types ask for one.

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
- Creating a client still matches an existing person by email only. Entering an email already on file attaches the new case to that person and keeps their existing name, even if you typed a different name (for example, spouses who share an email). The duplicate warning makes this visible before you save; it does not change it. A different email always creates a separate person, even when the name and phone match an existing client.
- An email match that differs only in capitalization from what is stored may still create a new person rather than using the existing one. Use **Use this client** from the warning to be sure the existing client is used.
- A shared client's SSN entered before SSNs were kept per firm cannot be attributed to a firm.
- Removing a client who has no remaining cases or lead with your firm means their profile can no longer be opened by your staff.
- Archiving a client is blocked if they have active cases, upcoming bookings, active subscriptions, unpaid invoices, or pending payments. All of these must be resolved first.
- When you archive a client, their open tasks are completed and their conversations with your firm are archived. The client record itself is preserved for historical reference.
- The activity entries recording a follow-up stop are written to the client's cases that exist at that moment. A case started afterwards does not receive a backdated entry, though the client record still shows that follow-ups are stopped.
- Follow-ups stopped before this was recorded show no attribution — the setting is in effect, but there is no record of who turned it off or when.
- County is blank on every client record until an address is saved that carries one. Existing records are not backfilled, so a firm should not read a blank county as "no county on file for this address".
- An address collected at booking is the client's one current address. Recording where a client lived at the time of an earlier booking is not supported.
- Imported matters are reached from the firm's case tracker rather than from the contact. If your team used the contact page to open a client's MyCase history, use the tracker and filter to imported matters instead.
- Only matters carrying the MyCase import status are held back. A matter migrated some other way, or one taken up as live work, appears on the contact as an ordinary case.

## Related Features

- [Contacts](contacts.md)
- [Scheduling](../appointments/scheduling/README.md) — booking can collect the client's address and county onto their record
- [Communication History](communication-history.md)
- [Notes](notes.md)
