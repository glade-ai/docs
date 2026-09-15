# Zapier Integration

## Overview

The Zapier integration lets a firm send new leads into Glade from wherever they arrive — a web form, a call tracking service, a marketing platform, a spreadsheet — without Glade needing to support each of those tools directly. Your firm connects Zapier once, and any Zap you build can hand a lead over. Each delivery creates a client record (or matches an existing one), records where the lead came from, and files any call text as a transcript on that client. It is set up by a firm administrator in settings.

## Key Behaviors

### What arrives with a lead

- **The person**: first name, last name, email address, and phone number. These are what Glade matches on and what the client record is built from.
- **Where the lead came from**: the lead source, the marketing source, the contact source, and the opportunity source are each recorded separately, rather than being combined into one field. A firm that tracks a campaign and a channel independently keeps them independent.
- **Notes** written by whoever took the lead.
- **A call transcript**, where the lead came from a recorded or transcribed conversation.
- **The case it belongs to**, optionally, where your Zap knows which matter the lead relates to.

### The client record

- **An existing client is reused rather than duplicated.** A lead matching somebody already at your firm is recorded against that person.
- **A new client is created quietly.** They are not sent an account creation email, are not enrolled in SMS, and are not added to broadcast lists. A lead is not a client relationship yet, and the integration does not treat it as one.
- **Each accepted lead adds an internal note on the person**, recording that it arrived through Zapier, which Zap sent it, and when Glade received it. Any notes your Zap supplied are included in it. This is the audit trail for where a client on your list came from.
- **Notes and transcripts stay separate.** A transcript is filed as a transcript, not pasted into a note.

### Call transcripts

- **A transcript is filed on the client** and appears alongside their other recorded calls, in the same place as transcripts from your phone system — see [3CX Phone System Integration](./3cx.md).
- **It attaches to a case where that is unambiguous.** If the client has exactly one active case, the transcript goes onto it. If your Zap names the case, it goes onto that one.
- **Where the client has several active cases and your Zap does not say which**, the transcript stays on the person rather than being filed against a guess. It is not lost — it is on the client, just not on a matter.
- A case your Zap names has to belong to the same firm and the same client. A case that does not is refused rather than used.

### Retries and duplicates

Zaps retry. The integration is built for that.

- **The same lead delivered twice produces one client and one transcript**, not two. A retry is recognized and the original record is reused, including its internal note.
- Glade recognizes a repeat from the identifier your Zap sends with the lead, or — where there is none — from the content of the delivery itself, so a Zap that does not send an identifier still does not double up.

### Leads that need a person to look at them

- An identity Glade cannot resolve confidently, or one that appears to belong to another firm, is held for manual review rather than being written to a record. Nothing is created from a lead Glade is not sure about.
- Access is scoped to your firm throughout. A lead cannot reach another firm's clients or cases through the integration, and another firm's connection cannot reach yours.

## Configuration

Set up under your firm's settings, by a firm administrator.

- **Connecting**: generate a connection key for your firm, then give it to your Zap so Glade recognizes the deliveries as yours. Anyone at your firm can see whether the integration is connected; only an administrator can generate, rotate, or revoke the key.
- **The key is shown once, when you generate it.** Copy it into Zapier at that point — it cannot be displayed again. Generate a new one if it is lost.
- **Rotating and revoking**: rotating issues a new key, and revoking switches the integration off. In both cases the previous key stops working immediately, so a Zap still using it is rejected until you update it. Rotate if the key may have been exposed; revoke to stop deliveries entirely.
- **What your Zap sends** is built in Zapier, not in Glade. Map your source's fields onto the lead details listed above.

> TODO: Confirm where the Zapier connection lives in Settings, what the status and key-generation controls are labeled, and where a firm finds the field reference for building the Zap.

## Edge Cases & Limitations

- The four source fields are recorded as they arrive. Choosing them from your firm's own lists — the way a lead source is picked on a client record — is not yet available, so a value sent by a Zap can sit outside the [lead source list](../back-office/settings.md#lead-sources) your firm maintains. Agree the spellings with whoever builds the Zap, or the same channel ends up recorded several ways.
- Revoking or rotating a key takes effect immediately and is not reversible. A Zap that has not been updated fails until it is given the new key.
- A transcript that lands on the person rather than a case stays there. Moving it onto a matter afterwards is not something the integration does — name the case in the Zap if it needs to arrive attached.
- A client created from a lead has no portal access and has not agreed to be contacted. Enroll them deliberately if you intend to message them.
- The integration brings leads in. It does not send anything from Glade back out to Zapier.

## Related Features

- [3CX Phone System Integration](./3cx.md) — call transcripts from your phone system, filed the same way.
- [Analytics Tracking](./analytics-tracking.md) — the other route by which attribution reaches a client record.
- [Contacts](../crm/contacts.md) — the client records leads are matched against and created as.
- [Back Office Settings](../back-office/settings.md#lead-sources) — your firm's own list of lead sources.
