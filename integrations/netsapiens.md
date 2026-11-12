# NetSapiens (NoodleVoice) Call Transcripts

## Overview

Firms whose phone service runs on the NetSapiens platform — including NoodleVoice, which resells it — can have finished calls with clients saved to Glade as transcripts. The phone system already produces an AI transcript and summary of each call. Once your firm is connected, Glade picks up each finished call from a client's number and files its transcript on that client's record, so the conversation is part of the client's file and not only in the phone system.

## Key Behaviors

- **Only calls with clients are kept.** When a call ends, Glade checks the calling number against your firm's clients. If the number matches a client, the transcript is saved on that client. If it doesn't, the call is discarded straight away and nothing about it is stored. These are privileged attorney-client calls, so Glade does not keep calls it can't place.
- **Calls where nobody spoke are skipped**, such as missed calls.
- **The transcript is saved once the phone system finishes it.** This usually takes about a minute after the call ends. The saved transcript includes speaker names, the phone system's summary, and the call's topics.
- **The same call is recorded only once.** If the phone system sends a finished call again, it doesn't create a second transcript.
- **Matching is scoped to your firm.** A number that belongs to another firm's client is treated as unknown.
- **Call details stay out of Glade's logs and error reports.**

## Configuration

Glade staff connect a firm. There is no setting in the app yet. Your firm provides a read-only key for its phone account, and Glade gives your phone carrier a private web address to send finished-call notices to. Contact Glade support to set it up.

Open the client and choose **Transcripts**. A saved NetSapiens call is listed there with that client's other call transcripts, including calls saved from 3CX. The list is not split by phone system, and it does not label which system a transcript came from. The transcript is filed on the client, not on a case.

## Edge Cases & Limitations

- **Calls from a number that isn't on a client's record are not saved**, and can't be recovered later. Add the client's number to their record so future calls match.
- **No alert while a client is calling.** Glade saves the transcript after the call ends. It doesn't notify staff while the phone is ringing.
- **A transcript that never finishes is not saved.** If the phone system still hasn't finished a transcript after about two hours, Glade stops waiting and records an error for Glade to investigate.
- **If the phone account's key is revoked, transcripts stop arriving** until the firm is reconnected.
- **A client deleted while their call is processing** gets no transcript.
- Only firms Glade has connected are affected. Other firms and phone integrations work as before.

## Related Features

- [3CX Phone System Integration](./3cx.md) — caller lookup and call transcripts for firms on 3CX.
- [Client Records](../crm/client-records.md) — the record a transcript is filed against.
- [Communication History](../crm/communication-history.md) — the rest of a client's recorded contact with your firm.
- [Contacts](../crm/contacts.md) — how phone numbers are recorded against a client.
