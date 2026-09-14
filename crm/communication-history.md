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

(Notes on a client's profile — the **Internal Notes** tab on the client record — are a separate feature with their own rules. See [Notes](notes.md).)

#### Who can edit or delete an internal note

- The person who wrote an internal note can always edit or delete it.
- **A firm administrator can also edit or delete an internal note written by anyone else at the firm.** This covers the two situations firms actually run into: tidying a note left behind by someone who has since left the firm, and clearing a note filed on the wrong case. Previously only the author could touch a note, so a note from a departed colleague could not be corrected or removed by anybody.
- **This applies to internal notes only.** A client-facing comment can still only be edited or deleted by the person who wrote it. An administrator cannot rewrite or remove a colleague's message to a client — rewriting something the client has already read is a different act from tidying an internal record, and it is deliberately not permitted.
- Administrator access is scoped to the firm that owns the case. It gives no access to another firm's notes.
- The Edit and Delete controls appear only where you can actually use them, so what is offered matches what is allowed.

### Stopping an AI reply while it is being written

An AI reply can be stopped part-way through, and stopping it now stops the work behind it rather than only the text on screen.

- The reply halts as soon as you stop it. The assistant does not go on to take further action on the case — it will not book an appointment, raise an invoice, or send a message after you have stopped it.
- **Nothing arrives after you stop.** Previously the assistant kept running in the background: it could continue carrying out actions and then post its finished reply into the conversation moments later, so a message you had cancelled turned up anyway. Because the assistant can act on the case and not only write, a stop that did not stop was the more serious half of this.
- The portion of the reply already written stays in the conversation, matching what was on screen at the moment you stopped, so a useful partial answer is not thrown away.
- **One limit.** An action the assistant had already begun when you stopped it may still finish. Stopping reliably prevents anything *further*, but a step already under way cannot be pulled back. Check the case if you stopped a reply mid-action.
- A reply that stops on its own because it has taken too long behaves the same way, and is not treated as an error.

> TODO: Confirm which surfaces offer the stop control and how it is labeled, and whether a client chatting from the portal can stop a reply as well as a team member.

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
- A firm administrator's ability to edit and delete other people's messages covers internal notes only. There is no way for anyone other than the author to change a client-facing comment.
- A note whose author has left the firm can now be edited or deleted, but only by an administrator. Other team members still cannot.
- Stopping an AI reply cannot undo an action the assistant had already started. If a duplicate booking or invoice appears after a stop, that action was already in progress and needs to be removed by hand.

## Related Features

- [Client Records](client-records.md)
- [Contacts](contacts.md)
- [Notes](notes.md)
