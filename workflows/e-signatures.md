# E-Signatures

## Overview

E-signature requests let a firm send a document for a client — or a member of the firm — to sign electronically as part of a case. A request is prepared by placing signature fields on the document, sent to its signers, and completed once everyone has signed. The signed document and a signing certificate are attached to the case when the request completes.

> TODO: Document how an e-signature request is created and how signers are chosen. This page covers the request lifecycle, what each party sees at each stage, and what you can do with a request after it has gone out.

## Key Behaviors

### Request lifecycle

A request moves through these stages:

1. **Being prepared** — the request exists but its signature fields have not been placed yet. The client sees a message that the request is being prepared and there is nothing for them to do.
2. **Fields placed** — firm staff have finished marking where each signer signs. From this point the document is available to signers.
3. **Out for signature** — signers can open the document and sign. The firm sees how many signers are outstanding.
4. **Completed** — every signer has signed, and the signed document is attached to the case.

### What the client sees

- Once signature fields have been placed, opening the request loads the document to sign. Previously the client's view stayed on "Your signature request is being prepared" indefinitely and never loaded the document, even though the firm had finished preparing it — so nothing could be signed and there was no indication anything was wrong. This affected firm staff signing on the client's behalf as well.
- Before fields are placed, the client still sees the preparing message. That is the only stage where it appears.

### What the firm sees

- While signatures are outstanding, the firm's view shows how many signers remain.
- When every signer has finished but the signed document is still being assembled, the firm's view says the document is being generated. Previously this state read **"Awaiting signatures from 0 signers"**, which suggested the request was stuck when it was simply finishing.
- The field-placement prompt clears once fields have been placed, so a request that is ready for signers no longer invites staff to place fields again.

### Completed requests

- When a request completes, both the signed document and the signing certificate — the audit record of who signed and when — are attached to the case.
- A court form whose own title contains the word "certificate" (for example, a Certificate of Compliance) is treated as a signed document, not as the signing certificate. Previously such a form was mistaken for the audit record, which stopped the request from completing: every signer had signed, but the request stayed at the awaiting-signatures stage indefinitely.
- If attaching the documents fails, the request is still recorded as completed rather than being left in an earlier stage. The completion is not lost because of an attachment problem.

### Voiding, correcting, and re-sending a request

A request that has already gone out can be pulled back, corrected, and sent again without rebuilding it from scratch. Three actions work together:

- **Void** withdraws the request. Signers can no longer act on it, and it is removed from the client's path in the portal. The signature fields your team placed on the document are kept.
- **Replace file** swaps in a corrected version of the document — a fixed typo, an updated figure, a page that was missing. The request stays voided while you do this.
- **Resend** puts the request back into preparation, so you can check the field placements against the current document and send it out again.

Because the placements survive, correcting a document that has already been sent no longer means re-marking every signature and date box by hand. Voiding used to discard the prepared document along with the request, so any correction — however small — meant starting the preparation over.

- Void, replace, and resend apply to the same request rather than creating a new one, so the case keeps a single record of what was sent and when.
- A request that has been resent stays resent. A late status update arriving from the signing service for the version you voided does not flip the request back to voided after you have already sent it again.
- Voiding from inside the signing service's own editor rather than from Glade is not the same action, and does not preserve the field placements. Use the void action in Glade.

> TODO: Confirm where the void, replace file, and resend actions appear in the app, and which roles can use them.

## Configuration

E-signature requests have no settings of their own. They are sent manually or as part of a workflow:

- The **Send e-signature request** action in an automation rule sends a document for signature — see [Automation Rules](./automation-rules.md).
- **E-signature request sent** and **E-signature completed** are available as workflow triggers, and a workflow step can wait on an e-signature request before continuing — see [Triggers](./triggers.md).

## Edge Cases & Limitations

- A request whose signature fields have never been placed cannot be signed. If a client reports that a document is still "being prepared", check whether field placement was completed.
- Requests that were stuck in the preparing stage before this behavior shipped are not repaired automatically. Opening one now makes the document available; a request that appears stuck after that should be raised with Glade.
- A voided request is removed from the client's path and cannot be acted on — see [Client Portal](../intake/client-portal.md). It can be corrected and resent from Glade; see [Voiding, correcting, and re-sending a request](#voiding-correcting-and-re-sending-a-request).
- Signature field placements are preserved only when a request is voided from Glade. A request voided in the signing service's own editor cannot have its placements recovered, and has to be prepared again.
- Requests voided before this behavior shipped are not repaired retroactively — their field placements are already gone.

## Related Features

- [Automation Rules](./automation-rules.md)
- [Triggers](./triggers.md)
- [Custom Terms](./custom-terms.md)
- [Client Portal](../intake/client-portal.md)
