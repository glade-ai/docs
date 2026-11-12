# Write Actions

## Overview

Alongside the read tools, a set of actions can change data. These cover the support requests the assistant could previously only describe rather than carry out.

| Area | What the assistant can do |
|------|--------------------------|
| **Bookings** | Schedule a new consultation for a client — pick the service, the price, and the time — as well as cancel one, or reschedule it to a new time and optionally a different team member. |
| **Clients and contacts** | Correct a client's, spouse's, or contact's name, email address, or phone number. |
| **Team** | Invite a team member, and correct a team member's role — including the case where a member has no role recorded and the firm cannot add anyone new until it is fixed. |
| **Invoices and payments** | Void an invoice, refund a payment in full or in part, and remove processing fees from an invoice. |
| **Cases** | Resend a client's portal invitation, re-run a workflow step that did not fire, and re-run AI extraction on a document that was read incorrectly. |
| **Questionnaire answers** | Add a new row to a list on a questionnaire — a creditor, an asset, a lease — as well as correcting answers already recorded. An empty schedule can be populated rather than only edited. |
| **Custom reports** | Create, edit, duplicate, and delete a saved custom report. |

## Key Behaviors

- **Write actions are off unless your firm has them switched on.** Where they are not enabled, the assistant answers as it does today — it explains what to change and leaves the change to you.
- **Your own permissions still apply.** Inviting a team member or changing a role requires the same team-management permission the app requires; without it the action is refused. Every action is scoped to your firm, and an action aimed at another firm's record is refused as not found.
- **Sensitive client fields are deliberately out of reach.** Date of birth, Social Security number, and address cannot be changed through the assistant — only name, email, and phone.
- **A portal invitation always goes to the case's own client.** The recipient is taken from the case rather than supplied in the request, so an invitation cannot be redirected to someone else.
- **Money actions are confirmed before they run.** The assistant confirms a void or a refund with you first, and each one is recorded in an audit trail identifying who asked for it.
- **Asking twice does not book twice.** If the assistant repeats a request to schedule the same client for the same service at the same time — which it may do if a reply is slow to arrive — it returns the booking already made rather than creating a second one and notifying the client twice.
- **A new questionnaire row has to say something.** A row with every cell left blank is refused rather than added, so an accidental request cannot leave an empty creditor sitting on a schedule.
- **Adding a row can create a real record on the case.** On a list that feeds the case's own records — creditors and property, for example — a row added through the assistant creates the corresponding case record immediately, exactly as it would if someone typed it into the form. Rows added this way are recorded as entered by hand, and appear in the case's activity history.
- **A questionnaire edit only updates the case data tied to what changed.** Correcting an answer or adding a row through the assistant passes along only the fields that edit touched. Other information already on the case is left as it is — previously an edit could re-send every answer on the questionnaire and overwrite newer values on the case, such as blanking the court division.
- **A saved questionnaire edit is reported as saved, even if the case update after it fails.** If the answer saves but carrying the change over to the case's records does not complete, the assistant is told the edit went through and that the case update did not. It is not told the whole edit failed, so it does not try again and add a duplicate row. The case update is not retried automatically; check the case in the Glade app and correct the affected value there if needed.

## Configuration

> TODO: Confirm which write actions are available to firms today and how a firm has them enabled. The actions are being switched on in batches, so a firm may have some and not others.

## Edge Cases & Limitations

- **Correcting a client's email no longer reports a failure after it saved.** Changing a client's email address through the assistant could come back as an upstream server error even though the change had already been applied — so the assistant would report a failure, try again, and leave your team unsure which state the record was in. The change now reports success. An email address already in use by someone else is still refused, and it is refused before anything is saved.
- **Write actions are limited to the list above**, and only where your firm has them enabled. For anything else, the assistant will tell you the change needs to be made in the Glade app.
- **Booking a client who has never booked before needs the price named.** The assistant can only reach a service's price through a client's existing booking, so scheduling a brand-new client may need you to say which price applies. Asking the assistant to list your services does not currently return their prices.
- **Scheduling through the assistant does not require a case.** A booking can be made from the client, the service, and the time alone.
- **Creating a report does not run it.** The assistant saves a custom report to your firm's dashboard with the columns and filters you described; open it in Glade to read the rows or export them.
- **An edit that changes nothing does not confirm earlier case updates.** Repeating an edit whose answers are already saved goes through, but it does not tell you whether an earlier, failed case update has since been fixed.

## Related Features

- [MCP Tools Reference](README.md)
- [MCP Overview](../overview.md)
- [Case Data](../../workflows/questionnaires/case-data/README.md)
