# 3CX Phone System Integration

## Overview

The 3CX integration lets a firm's 3CX phone system look a caller up in Glade while the phone is still ringing. When a call comes in, 3CX matches the caller's number against the firm's Glade clients and shows the staff member who answers who is calling and where their case stands — instead of leaving them to search for the client after picking up. The same lookup can drive a firm's automated call flow, so calls are routed on the caller's case details rather than on a menu the caller has to work through. Once a call is finished, 3CX can also send its transcript back so the conversation is recorded on the client's file.

## Key Behaviors

- **Callers are matched on phone number or email address.** A phone number matches on its last ten digits, so a number stored with a country code, dashes, or brackets still matches the number 3CX reports.
- **A match returns the client's contact details** — their name, email address, and phone numbers — along with a link that opens that client directly in Glade.
- **A match also returns where the case stands**, so a call flow can act on it without a second lookup:
  - the case number,
  - the case status,
  - the case sub-type,
  - whether the meeting of creditors has been held,
  - the office or division handling the case.
- **The lookup is scoped to your firm.** A phone number or email belonging to another firm's client returns nothing. There is no way to reach another firm's records through the integration.
- **No match returns an empty result rather than an error**, so an unrecognized number — a wrong number, or a caller who is not yet a client — does not interrupt the call flow.
- Case details are returned where they are available. A caller who is a client but has no case open yet is still matched on their contact details.

### Values a call flow can branch on

Three of the values the lookup returns are shaped for call flows rather than for reading on screen, so a flow can test them directly.

- **Case status** reports one of three things: the caller is a client with no case open yet, the caller has a case that is not yet filed and pending, or the case is filed and pending. A filed-and-pending case returns no status value at all, which is what lets a flow treat "nothing to report" as the ordinary path.
- **Log number** returns the caller's client identifier in Glade. Firms moving from an older in-house lookup that branched on a log number have a value to test again — this was previously not provided at all.
- **Office or division** is returned as the office label your call flow expects wherever Glade has been set up with your firm's labels for a district. Tennessee districts return Nashville, Northern, or Southern, and Georgia districts return Atlanta.

Firms that carried a call flow over from an older lookup should re-test any branch on these three values. They are deliberately shaped to match what those older flows expected, so a branch that had to be rewritten when the integration was first set up may now be able to go back to its original form.

### Recording a finished call in Glade

As well as looking a caller up while the phone is ringing, 3CX can send a finished call's transcript back to Glade, so the conversation is on the client's record instead of only in the phone system.

- **A transcript is filed against the client it belongs to**, matched on the calling number the same way the lookup matches it, and appears on that client's transcripts alongside their other recorded calls.
- **A caller the lookup did not recognize can be created as a client.** Where the number matches nobody at your firm, 3CX can ask Glade to create a client record from the call so the transcript has somewhere to live rather than being discarded. The new client is recorded as having come from 3CX and is **not** sent a welcome email.
- **Only answered calls with a transcript are recorded.** A missed or unanswered call, and an answered call whose transcription came through empty, is skipped rather than filed as a blank entry.
- **The same call is only recorded once.** If the phone system sends a call again — after a retry, for example — it is recognized as the call already on file and does not produce a second entry.
- The caller is always matched on the last ten digits of the calling number. A call carrying an identifier from another system is matched on the number instead, and a call from a number Glade cannot place is refused rather than filed against a guess.

Recording calls is set up in your firm's 3CX configuration, separately from the caller lookup — the lookup keeps working on its own if you do not turn call recording on. Your 3CX administrator needs the configuration details from Glade support to enable it.

> TODO: Confirm where a client's call transcripts are read in the app, and whether a client created from an unmatched call is distinguishable in the client list beyond its 3CX lead source.

### Case details for clients imported from another system

A firm that moved to Glade from another practice-management system may have clients whose case number, chapter, and county were never recorded as case fields — they live in a note that came across with the import.

- When those fields are empty on the client's record, the lookup reads them from the imported note instead, so the caller's case number and chapter still reach the phone system and office routing still has something to work from.
- Fields recorded properly on the case always take precedence. The note is only consulted where a field would otherwise come back empty.
- The note is only a fallback for these details. It does not create a case in Glade, so the caller still shows as a client without an open case elsewhere in the app.

### Court divisions in call routing

Where a firm routes calls by office, the court division on the case is translated into the office label the firm's call flow expects.

- Where Glade has been set up with a firm's office labels for a district, the case's division is translated to the matching label.
- Divisions in districts that have not been configured this way are returned as they are recorded on the case and are not translated. A call flow that branches on a specific office name needs to account for that.

## Configuration

Your firm sets the integration up itself, from **Account → Integrations**, where **3CX** appears alongside the other integrations.

| Setting | Description |
|---------|-------------|
| Access credential | The key that identifies your firm to the lookup. Your firm generates it from Account → Integrations and enters it into 3CX once, in both the CRM lookup configuration and the call-flow configuration. |
| Lookup by | Phone number or email address. Both are supported; 3CX normally sends the caller's number. |
| Office labels | The office or division names your call flow branches on. Tell Glade support which labels your flow expects so divisions can be translated to them. |
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
- A client created from an unmatched call is a real client record in Glade, not a placeholder. If your firm would rather unknown callers not create records, leave client creation switched off in the 3CX configuration — transcripts from unrecognized numbers are then not recorded at all.
- Matching is exact on the last ten digits of a phone number. A client who calls from a number that is not on their record in Glade is not matched — add the number to the client's record for future calls.
- A client with several people on their case is matched on whichever record carries the calling number. The lookup returns that person, not everyone on the case.
- Firms moving to this from an older in-house lookup should re-check any call-flow branch that tests for a specific value. Case status, log number, and office labels are now shaped to match what those flows expected, but the match is not guaranteed for every value — test each branch against a real call before relying on it.
- A filed-and-pending case returns no case status value. A call flow that treats an empty status as a lookup failure needs to distinguish the two.
- The imported-note fallback only fills the case number, chapter, and county. Other case details on a client imported this way are still returned empty.
- Divisions in districts that have not been configured for office-label translation are returned as recorded — see above.

## Related Features

- [Client Records](../crm/client-records.md) — the client details the lookup returns, and the record a call transcript is filed against.
- [Communication History](../crm/communication-history.md) — the rest of a client's recorded contact with your firm.
- [Contacts](../crm/contacts.md) — how phone numbers and email addresses are recorded against a client.
- [Case Management](../back-office/case-management.md) — the case status and office the lookup reports.
