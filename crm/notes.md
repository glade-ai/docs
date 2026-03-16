# Notes

## Overview

Notes allow creators and their team members to attach internal annotations to client records. Notes are visible only to the creator's team and are accessed through the "Notes" tab on the member detail view. They serve as a lightweight way to record observations, reminders, or context about a client that does not belong in the client-facing conversation.

## Key Behaviors

- Notes are scoped to a (creator, person) pair. A note belongs to a specific creator's practice and references a specific client (person).
- Each note records the `authorPersonId` (the team member who wrote it), the `creatorId`, and the `personId` (the client the note is about).
- Note content is stored as structured rich text (`slateAST` in JSON format) and a rendered `html` representation. The rich text editor supports standard formatting.
- Notes are displayed grouped by month and year, with the most recent notes first.
- The notes list is paginated with a default of 5 notes per page.
- Creating a note requires team member permissions for the creator. The system verifies that the requesting user has permission before allowing note creation.
- After a note is created, the author's name and profile photo are displayed alongside the note content and creation date.
- Notes are fetched and displayed on a per-client basis from the member detail view.

## Configuration

- **Pagination**: Notes are paginated with a configurable `perPage` parameter (default: 5).
- No additional configuration options exist. Notes do not support editing or deletion through the UI.

## Edge Cases & Limitations

- Notes cannot be edited or deleted after creation. There is no update or delete endpoint exposed for person notes.
- Notes are not searchable. There is no full-text search or filtering capability on note content.
- Notes are only accessible through the creator dashboard member detail view. Clients cannot see notes written about them.
- The `slateAST` field is typed as `any` in the codebase, meaning there is no strict schema validation on the rich text structure beyond what the frontend editor produces.

## Related Features

- [Client Records](client-records.md)
- [Contacts](contacts.md)
- [Communication History](communication-history.md)
