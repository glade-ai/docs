# 3CX Phone System Integration

## Overview

The 3CX integration lets a firm's 3CX phone system look a caller up in Glade while the phone is still ringing. When a call comes in, 3CX matches the caller's number against the firm's Glade clients and shows the staff member who answers who is calling and where their case stands — instead of leaving them to search for the client after picking up. The same lookup can drive a firm's automated call flow, so calls are routed on the caller's case details rather than on a menu the caller has to work through. Once a call is finished, 3CX can also send its transcript back so the conversation is recorded on the client's file.

## Key Behaviors

- **Callers are matched on phone number or email address.** A phone number matches on its last ten digits, so a number stored with a country code, dashes, or brackets still matches the number 3CX reports.
- **A match returns the client's contact details** — their name, email address, and phone numbers — along with a link that opens that client directly in Glade.
- **A match also returns where the case stands**, so a call flow can act on it without a second lookup:
  - the case number,
  - the case sub-type,
  - the date the meeting of creditors was held,
  - the date the case was dismissed,
  - the date the Chapter 13 plan was confirmed.
- **The lookup is scoped to your firm.** A phone number or email belonging to another firm's client returns nothing. There is no way to reach another firm's records through the integration.
- **No match returns an empty result rather than an error**, so an unrecognized number — a wrong number, or a caller who is not yet a client — does not interrupt the call flow.
- Case details are returned where they are available. A caller who is a client but has no case open yet is still matched on their contact details.

### Key dates a call flow can branch on

The lookup returns three dates read from the court notices on the caller's case, so a call flow can route on where the case has actually reached rather than on a status label.

- **Meeting of creditors held** — the date of the 341 meeting-held notice.
- **Dismissed** — the date of the order dismissing the case. A *motion* to dismiss is not a dismissal, so a case where one has been filed but not granted carries no dismissal date.
- **Plan confirmed** — the date of the order confirming the Chapter 13 plan.
- Each date is returned in day/month/year form, and **empty where the case has no notice of that kind**. Empty means "this has not happened, or the court has not sent a notice saying so" — it is not an error.
- **Log number** returns the caller's client identifier in Glade, for firms whose call flow branches on it.

> **These dates replace the previous status and office values, and existing call flows must be remapped.** The lookup no longer returns a case status or an office/division label at all, and the meeting-of-creditors value is a date rather than a yes/no flag. A flow that branches on any of the three keeps running but takes the wrong branch, so re-point it before the change reaches your firm:
>
> - the meeting-of-creditors variable now holds a date or nothing, not a flag — test for a date rather than for a "yes"
> - add variables for the dismissal date and the plan confirmation date, which were not available before
> - retire the branches that test case status and office or division

The change is what makes date-based routing possible: a flow can now ask *when* the 341 was held, or whether a plan was confirmed before a given date, which the old flag and status codes could not express.

### Recording a finished call in Glade

As well as looking a caller up while the phone is ringing, 3CX can send a finished call's transcript back to Glade, so the conversation is on the client's record instead of only in the phone system.

- **A transcript is filed against the client it belongs to**, matched on the calling number the same way the lookup matches it, and appears on that client's transcripts alongside their other recorded calls.
- **A caller the lookup did not recognize can be created as a client.** Where the number matches nobody at your firm, 3CX can ask Glade to create a client record from the call so the transcript has somewhere to live rather than being discarded. The new client is recorded as having come from 3CX and is **not** sent a welcome email.
- **Only answered calls with a transcript are recorded.** A missed or unanswered call, and an answered call whose transcription came through empty, is skipped rather than filed as a blank entry. A skipped call is reported back to the phone system as handled, so it is not sent again and again. Previously an empty transcript was refused as a faulty call, and 3CX retried it indefinitely.
- **The time a call took place is read in your firm's timezone.** Phone systems report a finished call's time either as a full date and time with a timezone on it, or as the plain wall-clock reading on the PBX itself — `9/15/2026 3:20 PM`. Both are accepted, and a wall-clock reading is taken to be your firm's local time. A firm whose phone system sends the plain form previously had **every** call refused, so nothing from it was ever filed, and the phone system retried each one.
- **The same call is only recorded once.** If the phone system sends a call again — after a retry, for example — it is recognized as the call already on file and does not produce a second entry.
- The caller is always matched on the last ten digits of the calling number. A call carrying an identifier from another system is matched on the number instead, and a call from a number Glade cannot place is refused rather than filed against a guess.

Recording calls is set up in your firm's 3CX configuration, separately from the caller lookup — the lookup keeps working on its own if you do not turn call recording on. Your 3CX administrator needs the configuration details from Glade support to enable it.

> TODO: Confirm where a client's call transcripts are read in the app, and whether a client created from an unmatched call is distinguishable in the client list beyond its 3CX lead source.

### Case details for clients imported from another system

A firm that moved to Glade from another practice-management system may have clients whose case number, chapter, and county were never recorded as case fields — they live in a note that came across with the import.

- When those fields are empty on the client's record, the lookup reads the case number and case sub-type from the imported note instead, so the caller's case number and chapter still reach the phone system.
- Fields recorded properly on the case always take precedence. The note is only consulted where a field would otherwise come back empty.
- The note is only a fallback for these details. It does not create a case in Glade, so the caller still shows as a client without an open case elsewhere in the app.
- The three key dates are read from the court notices on the case and are never taken from an imported note, so an imported matter with no notices in Glade returns none of them.

## Configuration

Your firm sets the integration up itself, from **Account → Integrations**, where **3CX** appears alongside the other integrations.

| Setting | Description |
|---------|-------------|
| Access credential | The key that identifies your firm to the lookup. Your firm generates it from Account → Integrations and enters it into 3CX once, in both the CRM lookup configuration and the call-flow configuration. |
| Lookup by | Phone number or email address. Both are supported; 3CX normally sends the caller's number. |
| Key dates | The meeting-of-creditors, dismissal, and plan-confirmation dates are returned automatically wherever the case has the matching court notice. Nothing is configured in Glade; map them to variables in your 3CX call flow. |
| Call recording | Whether finished calls are sent back to Glade as transcripts, and whether an unrecognized caller creates a client record. Configured in 3CX by your phone administrator using details from Glade support; off until they set it up. |

### Managing the access credential

Opening **3CX** from the Integrations list gives your firm the actions it previously had to ask Glade support to run:

- **Connect** generates the firm's key and shows it. Any member of your firm can do this.
- Once connected, the key can be **shown again and copied** from the same place, so nobody needs to have saved it at the moment it was created. It is masked until you choose to reveal it.
- **Regenerate** issues a fresh key. The previous key stops working immediately, so 3CX has to be updated with the new one before the lookup will answer again.
- **Disconnect** revokes the key. Lookups stop being answered at once — a key that was pasted into 3CX before disconnecting no longer works.

Treat the key like any other system password: anyone holding it can look your firm's clients up by phone number. If it has been shared beyond the people who need it, regenerate it and update 3CX.

Firms already using a key that Glade issued for them by hand keep working as they are. The first time you use **Connect**, the firm switches to the key shown on that screen and the older one stops being accepted.

## Edge Cases & Limitations

- What comes back from 3CX is the call's transcript and, where you have enabled it, a client record for an unrecognized caller. Call outcomes, call duration, recordings, and notes are not written back.
- **Glade records the transcript your phone system produces; it does not produce one.** A call whose transcript arrives empty is skipped and cannot be filled in afterwards — the recording stays on your own phone system and Glade has no access to it. If answered calls are being skipped, the fix is on the 3CX side: recording and transcription have to be switched on, and the call journal has to wait for the transcript before sending. Ask your phone administrator to check both.
- A call time that arrives as a plain wall-clock reading is treated as your firm's local time. A firm whose phones sit in a different timezone from the one set on its Glade account will see those calls filed against the firm's timezone rather than the phone system's.
- A client created from an unmatched call is a real client record in Glade, not a placeholder. If your firm would rather unknown callers not create records, leave client creation switched off in the 3CX configuration — transcripts from unrecognized numbers are then not recorded at all.
- Matching is exact on the last ten digits of a phone number. A client who calls from a number that is not on their record in Glade is not matched — add the number to the client's record for future calls.
- A client with several people on their case is matched on whichever record carries the calling number. The lookup returns that person, not everyone on the case.
- **Case status and office or division are no longer returned.** A call flow that branches on either needs those branches removed; they cannot be restored, and there is no replacement value for them.
- The key dates come from court notices Glade has received. A hearing that happened but whose notice has not reached Glade, or a case whose notices are not being collected, returns an empty date — which reads the same as the event not having happened.
- Dismissal reports the court's dismissal order only. A case with a motion to dismiss on the docket returns no dismissal date until the order is entered.
- Plan confirmation applies to Chapter 13. A Chapter 7 case returns no confirmation date.
- The imported-note fallback only fills the case number and case sub-type. Other case details on a client imported this way are still returned empty.

## Related Features

- [Client Records](../crm/client-records.md) — the client details the lookup returns, and the record a call transcript is filed against.
- [Communication History](../crm/communication-history.md) — the rest of a client's recorded contact with your firm.
- [Contacts](../crm/contacts.md) — how phone numbers and email addresses are recorded against a client.
- [Case Management](../back-office/case-management.md) — the case the lookup reports on.
- [PACER](pacer/README.md) — the court notices the key dates are read from.
