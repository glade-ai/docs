# Client County and Address

## Overview

An appointment type can collect where the client is — their county, their full address, or both — at booking time, and can route the booking to a calendar based on the client's county. Separately, a firm can record the counties it serves. These settings are for firms whose work depends on where the client lives: which office covers them, which court their case would be filed in, and whether the firm practices in their county at all.

## Key Behaviors

### Asking a booking client for their county

An appointment type can require the client to give their **county** when they book. This is for firms whose work depends on where the client lives — which office covers them, which court their case would be filed in, and whether the firm practices in their county at all.

- **The requirement is set per appointment type**, and it is off until your firm turns it on. A service with no use for a county asks for nothing, so nothing changes for a firm that does not enable it.
- **The client picks their county from a list rather than typing it.** The list is searchable by county name and can be narrowed to a state, so a client finds their county without needing to spell it the way the courts do. Picking from the list is what makes the answer usable downstream — a typed county has to be matched before it can be relied on, and misspellings are the usual reason that fails.
- **Requiring the county is separate from requiring the client's address.** The two settings are independent: an appointment type can ask for one, both, or neither.
- **Existing appointment types are unchanged.** Turning the requirement on affects bookings made afterwards. It does not go back and ask for a county on appointments already booked, and it does not block a client from managing a booking they made before the setting changed.

### Collecting the client's address when they book

An appointment type can ask the client for their address as part of booking. Firms running several offices use this to route a new matter to the nearest one, and to see which parts of their advertising area are actually producing consultations.

- **It is set per appointment type.** An appointment type that does not ask for an address shows no address fields at all, so a service with no use for one is unchanged.
- **Where the client enters it** — on the **Enter your information** step, alongside name, email, and phone.
- **Required means the whole address.** Street, city, state, and ZIP all have to be filled in; a city or a ZIP on its own is not enough.
- The client types their street and picks from suggested addresses, which fills in the rest. Where the suggestion service cannot complete the address, Glade falls back to a second lookup so the city, state, and ZIP still arrive rather than being left blank.
- **The client's county is worked out from the address** and shown under the fields. It is saved to the client's record along with the rest of the address, so nobody has to look it up again later. See [Client Records](../../crm/client-records.md).
- The address is saved on the client's record rather than copied onto the booking, so a booking always shows where the client lives now. Correcting an address once corrects it everywhere.
- **Booking waits until Glade knows whether an address is needed.** Confirming is held for the moment it takes to load the appointment type's settings, so a service that requires an address can never take a booking without one.
- Staff booking on a client's behalf can still record or correct an address afterwards on the client's record.

> TODO: Confirm where the "require client address" setting is switched on for an appointment type, and where the address and county appear on the firm-side bookings list.

### Routing bookings to a calendar by county

An appointment type can send its bookings to a particular calendar based on **the county the client is in**. A firm that covers several counties from different offices, or that has a different attorney responsible for each, can have a booking land on the right calendar when it is made rather than being moved by hand afterwards.

- Rules are set per appointment type, one county to one calendar. A county with no rule on that appointment type is not routed.
- **Routing only applies when it has an answer for every part of it.** The booking falls back to your firm's usual calendar selection — exactly as it worked before — when the appointment type has no county rules, when no county is recorded for the client, when the recorded county is not one Glade recognizes, or when no rule covers the client's county. A booking is never left without a calendar because routing did not resolve.
- **An appointment type with no county rules is unchanged.** Nothing about your existing booking behavior changes until your firm sets a rule up.

> TODO: Confirm where county routing rules are configured on an appointment type, and which county the rules match on — the one a client supplies at booking time or the one on their address in Glade.

### Counties your firm serves

Separately from what a booking asks the client, your firm can record **the counties it serves** — the list of counties your practice covers.

- The list is set once for the firm, not per appointment type or per team member.
- Counties are chosen from the same searchable catalog the booking form uses, so the names your firm records and the ones clients pick from are the same names.
- A firm that records nothing is treated as having no restriction recorded, which is how every firm starts.

> TODO: Confirm where the served-counties list is edited in the dashboard, and what Glade does with it once recorded — whether it filters which appointment types a client in an unserved county is offered, drives office routing, or is reporting only. The setting is stored and editable; how it is acted on is not established from the source change.

## Configuration

| Setting | Description |
|---------|-------------|
| Client county required | Whether a client booking this appointment type must give their county. Off until your firm turns it on. Independent of whether the client's address is required. |
| Require client address | Whether the client is asked for their address when booking this appointment type. Off for every existing appointment type until a firm turns it on. |
| Counties served | The counties your firm's practice covers, recorded once for the firm. Empty until your firm records them. |

## Edge Cases & Limitations

- Requiring the county on an appointment type applies to bookings made afterwards. Appointments already on the calendar have no county recorded against them, and there is no way to ask for one retroactively.
- The county requirement and the counties your firm serves are two separate settings. Recording the counties your firm serves does not by itself require a client to give theirs, and requiring a client's county does not check it against your firm's list.
- A county your firm needs that is not in the searchable catalog cannot be selected. Contact support with the county and state to have it added.
- A booking shows the client's **current** address, not the address they gave when they booked. A client who moves has their earlier bookings show the new address too — this is deliberate, since the firm works from one address per client, but it means the address on an old booking is not a record of where the client lived at the time.
- The address requirement is enforced on the booking screens, not on the record itself. A staff member correcting a booking after the fact can save it without an address.
- Turning the setting on does not go back and collect addresses for clients who already booked. Only bookings taken afterwards are asked.

## Related Features

- [Scheduling](./README.md)
- [Client Booking Flow](./client-booking-flow.md)
- [Appointment Types](./appointment-types.md)
- [Client Records](../../crm/client-records.md)
- [Reporting](../../back-office/reporting/README.md) — address and county columns on the appointments report
