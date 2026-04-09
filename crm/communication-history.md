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
