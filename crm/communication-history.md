# Communication History

## Overview

Communication history tracks messaging between your firm and clients. Each conversation is a messaging thread accessible from the **Conversation** tab on a client's detail view. The system supports real-time chat, threaded replies, AI-assisted responses, and case-specific conversations.

## Key Behaviors

- Each conversation links your firm to a specific client through a thread of messages.
- Conversations have four statuses:
  - **Pending** — new conversation, no action required yet
  - **Response Required** — your team needs to respond
  - **Customer Response Required** — waiting on the client
  - **Completed** — conversation is resolved
- Messages support threaded replies, so side conversations can happen within a main thread.
- Messages can include rich text formatting, media attachments, product references, and tags.
- AI-generated and system messages are excluded from unread counts, so your unread indicator only reflects real client or team messages.
- AI responses can be turned on or off per conversation by any team member with the appropriate permissions.
- Unread detection only counts messages you haven't seen from other team members. In threaded conversations, only threads you're participating in generate unread indicators.
- Conversations are categorized by type: paid, scheduled, case-related, subscriber, lead, or anonymous.
- The conversation list shows a preview of the last message, timestamp, unread count, status, and associated products.

### Internal notes in case conversations

Case conversations — the discussions attached to a client's active workflow — support two types of messages: regular comments (visible to the client) and internal notes (visible to your team only).

- Internal notes are never shown to the client and never trigger client email notifications.
- Replies to an internal note are also internal. They remain team-only and do not appear in the client-facing discussion, regardless of who sends the reply.
- Only team members can reply to an internal note. Clients cannot post replies in an internal note thread.
- Tagged team members on an internal note or its replies receive the standard internal note email notification — but the client is never included.

#### Editing an internal note

An internal note can be edited after it is posted. While you are editing:

- Pressing **Enter** starts a new line, so you can write a multi-paragraph note without it being posted early. Previously Enter submitted the edit immediately — paralegals adding a second paragraph to an existing note had it saved mid-thought and had to re-open it to continue.
- Saving is always deliberate: use the **Save** button when the note reads the way you want.
- Mentioning a teammate with `@` works as it always has. While the mention list is open, Enter picks the highlighted person rather than adding a line break.

Writing a new note is unchanged — Enter has always added a line there.

### Case discussions stay with their own case

A reply you post in a case discussion is always filed against the case open in front of you.

- Opening a reply from a notification or a shared link and then moving to a different case used to be able to leave the earlier thread open underneath. A reply written at that point could be filed under one case while appearing in another's discussion. A small number of messages across the platform were affected, and at least one client saw another client's case details in their portal as a result. Those messages have been corrected.
- **A thread that cannot be opened now says so.** If a thread belongs to a different case, or fails to load, the discussion shows an error and the reply box stays disabled until you close the thread. Previously it looked like a thread with no messages yet, so it was easy to reply into.
- The reply box is briefly unavailable while a thread loads. This is deliberate — it stops a reply written in that moment from being filed as a new top-level comment instead of a reply.
- A direct link to a comment opens only if that comment belongs to a case you have access to.

None of this changes how you write or read a discussion on the case you are working on.

## Configuration

- **AI toggle**: Enable or disable AI responses on a per-conversation basis. Requires team member permissions.
- **Conversation status**: Managed automatically based on message activity and response patterns.

## Edge Cases & Limitations

- Anonymous conversations are those where the client has not yet verified their account.
- Lead conversations are those where the client has fulfilled all associated purchases and subscriptions.
- When a client is archived, their conversations with your firm are also archived.
- Case-specific conversations (internal team discussions about a case) are separate from client-facing conversations.

## Related Features

- [Client Records](client-records.md)
- [Contacts](contacts.md)
- [Notes](notes.md)
