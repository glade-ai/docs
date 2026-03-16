# Communication History

## Overview

Communication history tracks the messaging interactions between creators and their clients through the conversation system. Each conversation represents a messaging thread between a creator and a client, accessible from the member detail view's "Conversation" tab. The system supports real-time chat, threaded replies, AI-assisted responses, and workflow-specific conversations.

## Key Behaviors

- A conversation is a named entity identified by a unique `sid`, linking a creator to a customer person through messages rooted at a `rootMessage`.
- Conversations track status with four states: `PENDING`, `RESPONSE_REQUIRED` (creator needs to respond), `CUSTOMER_RESPONSE_REQUIRED`, and `COMPLETED`.
- Each conversation records `lastActivityTime`, `creatorLastViewedDate`, and `customerLastViewedDate` to support unread message tracking.
- Messages within a conversation support threading via `parentId` and `rootMessageId`. Top-level messages have `parentId` equal to `rootMessageId`.
- Messages have types including `Chat`, `ChatRoot`, `Comment`, `WorkflowComment`, `WorkflowInternalNote`, `FreeBroadcast`, `PaidBroadcast`, `CommunityPost`, and `NoodleBroadcast`.
- Messages store content as both structured `slateAST` (rich text JSON) and rendered `html`/`text` representations. They can include media attachments, product references, and tags.
- AI-generated messages are identified by a non-null `aiRequestId` or `isSystemMessage` flag. These are excluded from unread message counts.
- Conversations can be flagged as `isAiEnabled` to allow AI to participate. Creators with appropriate permissions can toggle this per conversation.
- Unread message detection checks messages created after a `lastViewedTimestamp`, filters out AI-generated and system messages, and only includes messages from Glade team members that the current user has not sent. For threaded messages, only threads the current user participates in generate unread indicators.
- Conversations have boolean flags indicating their nature: `isPaid`, `isScheduled`, `isWorkflow`, `isSubscriber`, `isLead`, `isAnonymous`.
- Purchased products and subscriptions are tracked per conversation through join tables (`conversation_person_products` and `conversation_person_subscriptions`).
- The conversation list in the member detail view displays items with the last message preview, timestamp, unread count, conversation status, and associated product types.

## Configuration

- **AI toggle**: Creators can enable or disable AI responses per conversation, provided they have team member permissions for the creator.
- **Conversation status**: Automatically managed by the system based on message activity and response patterns.

## Edge Cases & Limitations

- Permission checks for conversation access follow a multi-step process: (1) customer match, (2) creator match, (3) participant match, (4) special AI testing creator bypass, (5) team member check, (6) Glade-specific cross-creator team member check.
- The `customerPersonId` field on conversations is nullable for backward compatibility. Legacy conversations used a many-to-many `conversation_participants` join table instead.
- Anonymous conversations are identified when the non-creator participant is an unverified person.
- Lead conversations are those where all associated person products and subscriptions are fulfilled (no outstanding deliverables).
- When a client is archived, their conversations with that creator are soft-deleted.
- Workflow conversations are a separate entity (`WorkflowConversation`) from regular conversations, used for internal discussion on workflow items.

## Related Features

- [Client Records](client-records.md)
- [Contacts](contacts.md)
- [Notes](notes.md)
