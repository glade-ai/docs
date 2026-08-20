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
- Firms moving to this from an older in-house lookup should re-check any call-flow branch that tests for a specific value. Case status and office names are returned as Glade records them, which may not be the codes an older flow was written against, and the log number some older flows tested for is not provided at all.
- Divisions in districts that have not been configured for office-label translation are returned as recorded — see above.

## Related Features

- [Client Records](../crm/client-records.md) — the client details the lookup returns.
- [Contacts](../crm/contacts.md) — how phone numbers and email addresses are recorded against a client.
- [Case Management](../back-office/case-management.md) — the case status and office the lookup reports.
