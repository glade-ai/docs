# Email Tokens

## Overview

The email subject and body of a court notice automation support a set of tokens that are filled in at fire time — case details, debtor names, and 341 meeting and video hearing details — so the email reads like a personalized notice. The same tokens are available in the title and description of **Create task** actions.

## Key Behaviors

The email subject and body support a set of tokens that are filled in at fire time:

- `{{caseNumber}}` — the PACER case number on the matched notice.
- `{{noticeType}}` — the classified notice type that matched the automation.
- `{{clientName}}` — the primary debtor's name on the case.
- `{{judgeInitials}}` — the judge initials on the matched notice.
- `{{firmName}}` — your firm's display name.

In addition, automations can pull case-party and hearing details so the email reads like a personalized notice:

- The **first debtor's name** and, for joint cases, the **second debtor's name**, taken from the people on the case.
- The **341 meeting of creditors date and time**, taken from the linked court calendar entry for the case, or read directly from the notice when the court calendar entry for the case has not been created yet. A 341 notice and the calendar entry it produces are handled at the same moment, so the automation often used to run a fraction of a second before the calendar entry existed — which left the meeting date and time blank on the email even though the notice itself stated them. Those details now fill in either way, and the case number is no longer the only token that reliably renders on a 341 notice.
- The **video hearing join details** (for example, the meeting link, meeting ID, and passcode) when the notice is for a remote 341 meeting. Glade reads the Zoom details out of the notice text, including formats that name the trustee's meeting room without a colon before the meeting ID. Notices written that way previously produced no video hearing details at all.

The same case-party and hearing details are available to **Create task** actions, so a task raised from a 341 notice can state the meeting date, time, and join details in its description.

Tokens are case-insensitive and tolerant of extra whitespace inside the braces. Unknown tokens render as empty strings — the email still sends, with the unknown token replaced by nothing.

### The dial-in number is no longer included by default

The video hearing details token fills in the **meeting ID and passcode only**. The Zoom dial-in phone number is no longer part of it.

- Firms reported staff mistaking the dial-in number for a client's or a case's phone number, because it appeared in the email as a bare `Phone:` line with nothing to identify it as a Zoom number.
- A separate **video hearing phone** token is available for firms that do want the dial-in number in their emails. Add it to the subject or body where you want it to appear.
- **Nothing to change on your existing automations.** The dial-in line stopped going out on its own — you do not need to edit a template to remove it, and templates that never mentioned a phone number are unaffected.
- 341 emails sent before this change went out with the dial-in number included. Those emails are not recalled or resent.

> TODO: Confirm the in-product name of the video hearing phone token in the automation email editor's token picker.

### Video hearing details on Florida Southern 341 notices

341 meeting notices from the Southern District of Florida publish their video hearing details in a format Glade could not previously read, so the meeting ID, passcode, and dial-in number were left blank — and any automation email using the video hearing tokens sent with those details missing. These notices are now parsed into the meeting ID, passcode, and phone number, and the tokens fill in as expected.

Notices that arrived before this was fixed still have blank video hearing details. Contact Glade to have those cases re-processed if your team relies on those tokens.

### Debtor names on notices that are not linked to a case

Not every incoming court notice is matched to a case in Glade. When a notice is unlinked, the debtor and client name tokens have no client record to read from, and the email previously went out addressed to nobody — a discharge congratulations message opening "Dear ," is the case firms reported.

- When the notice is linked to a case, the client's name on that case is used, exactly as before. A linked name always wins.
- When the notice is not linked, or the linked client has no name on file, Glade falls back to the debtor name in the case caption carried on the court notice itself, and strips the trailing case-number text so only the name is inserted.
- If neither source has a name, the token still renders as empty and the email still sends.

### Hearing tokens when a notice carries more than one hearing

A single court notice can schedule more than one hearing — a confirmation hearing and a 341 meeting in the same docket entry, for example. When that happens, the hearing tokens use the **341 meeting**, so an email written for the meeting of creditors quotes the meeting date rather than whichever hearing happened to be listed first.

> TODO: Confirm the exact token spellings for the debtor names, 341 meeting date/time, and video hearing join details once they are finalized in the email editor.

## Configuration

| Setting | Description |
|---------|-------------|
| Subject and body | Email content with optional tokens for case number, notice type, client name, judge initials, firm name, debtor names, the 341 meeting date and time, and video hearing join details. The video hearing details token carries the meeting ID and passcode; the dial-in number has its own separate, opt-in token. |

## Edge Cases & Limitations

- Only the supported tokens listed above are recognized. Unknown tokens render as empty strings.
- Hearing tokens are filled from the linked court calendar entry or from the notice itself. If neither states a 341 meeting time, or the notice carries no video hearing details, those tokens render as empty strings.
- The video hearing details token no longer includes the Zoom dial-in number. A firm that needs the dial-in number in its 341 emails has to add the separate phone token to each template that should carry it.
- The case-caption fallback for debtor names only supplies a name. It does not link the notice to a case, so the other case-context tokens on an unlinked notice stay empty.
- Emails sent before the 341 meeting details fix went out with the meeting date, time, and join details blank. Those emails are not resent — if clients were sent a 341 notice missing its meeting details, follow up manually.

## Related Features

- [Court Notice Automations](./README.md)
- [Email Actions](./email-actions.md)
- [Create Task Actions](./create-task-actions.md)
