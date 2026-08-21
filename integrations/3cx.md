# 3CX Phone System Integration

## Overview

The 3CX integration lets a firm's 3CX phone system look a caller up in Glade while the phone is still ringing. When a call comes in, 3CX matches the caller's number against the firm's Glade clients and shows the staff member who answers who is calling and where their case stands — instead of leaving them to search for the client after picking up. The same lookup can drive a firm's automated call flow, so calls are routed on the caller's case details rather than on a menu the caller has to work through.

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

The integration is set up by Glade rather than from a settings screen in the app.

| Setting | Description |
|---------|-------------|
| Access credential | Glade issues your firm a long-lived credential that identifies your firm. It is entered into 3CX once, in both the CRM lookup configuration and the call-flow configuration. |
| Lookup by | Phone number or email address. Both are supported; 3CX normally sends the caller's number. |
| Office labels | The office or division names your call flow branches on. Tell Glade which labels your flow expects so divisions can be translated to them. |

To set the integration up, contact Glade support with your 3CX configuration. The credential is specific to your firm and should be treated like any other system password — anyone holding it can look your firm's clients up by phone number.

## Edge Cases & Limitations

- The integration is a lookup only. It reads client and case information into 3CX; it does not write call records, call outcomes, or notes back into Glade.
- Matching is exact on the last ten digits of a phone number. A client who calls from a number that is not on their record in Glade is not matched — add the number to the client's record for future calls.
- A client with several people on their case is matched on whichever record carries the calling number. The lookup returns that person, not everyone on the case.
- Firms moving to this from an older in-house lookup should re-check any call-flow branch that tests for a specific value. Case status, log number, and office labels are now shaped to match what those flows expected, but the match is not guaranteed for every value — test each branch against a real call before relying on it.
- A filed-and-pending case returns no case status value. A call flow that treats an empty status as a lookup failure needs to distinguish the two.
- The imported-note fallback only fills the case number, chapter, and county. Other case details on a client imported this way are still returned empty.
- Divisions in districts that have not been configured for office-label translation are returned as recorded — see above.

## Related Features

- [Client Records](../crm/client-records.md) — the client details the lookup returns.
- [Contacts](../crm/contacts.md) — how phone numbers and email addresses are recorded against a client.
- [Case Management](../back-office/case-management.md) — the case status and office the lookup reports.
