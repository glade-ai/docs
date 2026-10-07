# Document Uploads on Questions

## Overview

A questionnaire question can ask the client to upload a document alongside their answer. For example, "Upload your latest mortgage statement" can sit under the mortgage question. Template authors turn this on per question. Clients upload from a card under the question. The files land in a **Triage** folder on the case's document checklist, and AI reads them like any other upload.

## Key Behaviors

### Setting up an upload on a question

- In the template editor, **Ask for a document upload** can be turned on for any ordinary question. It isn't a separate question type, so the question still has its own answer.
- Each upload has a document name, a description, a required/optional choice, and an optional "show when" condition that controls when the upload is asked for.
- A **list** can have an upload too. It is asked once per entry, for example once per property or once per vehicle.
- Tables and page breaks can't have an upload. Changing a question into a table or page break removes its upload setting.
- There is no document type to choose. Every upload goes through Glade's normal AI classification.
- The setting is carried along when a template is published, cloned, imported or exported.

### Uploading as a client

- The client adds a file from the upload card under the question. Every open copy of the questionnaire updates straight away once the file arrives.
- All questionnaire uploads on a case go into one **Triage** folder on the case's document checklist. Glade creates it the first time it's needed. It sends no "you've been added to a checklist" email and no "file uploaded" email, and it creates no tasks.
- Each file remembers which question it answers, and which list entry for a question inside a list. Staff can move the file into another request and the question still finds it.
- A client can delete a questionnaire upload, and undo the delete, even after staff have moved it into another request. The exception is a for-your-eyes-only folder or a staff-only checklist.
- Deleting or restoring a questionnaire upload from the case's Documents list removes or restores it wherever it's filed, and the question's upload status updates to match.

> TODO: Confirm where the upload card appears. The source changes say the older questionnaire view has no upload card, so clients there can't upload from the question.

### AI review and data extraction

- AI checks a questionnaire upload against the question's document name and description, not against the folder name ("Triage").
- When the question sits inside a list entry, data extracted from the document fills in **that entry**. For example, a mortgage statement uploaded under one property fills that property. This happens only when the document's data fits the list (a vehicle document on a vehicles list) and passes the list's filter. Otherwise the data goes where it normally would. Manual edits on the entry stay protected.

### Required uploads and validation

- A required upload that is showing but has no file creates a **Document upload required** finding. In a list, each entry is checked separately.
- Changing an answer that the "show when" condition depends on rechecks the upload.
- The finding is **advisory, not blocking**. It shows in the pre-submit review but doesn't stop the client from submitting.
- **Documents that already filled in an answer count.** If AI already used a document's data to fill a question's answer, for example a mortgage statement collected through a document request, that document counts as the question's upload and the client isn't asked again. Clients see only the documents they have access to.
- Upload status carries over when a questionnaire is upgraded to a new template version, reverted, or restored from a snapshot, so a file that was uploaded doesn't show as missing afterwards.

## Configuration

| Setting | Where | Effect |
|---|---|---|
| Ask for a document upload | Question settings in the template editor | Adds an upload card under the question (or under each entry of a list). |
| Document name | Upload setting (up to 255 characters) | Shown to the client. AI also uses it to check the file. |
| Description | Upload setting (up to 4,000 characters) | Instructions for the client. AI also uses them to check the file. |
| Required | Upload setting | Creates a Document upload required finding while no file has been uploaded. |
| Show when | Upload setting (optional) | Asks for the upload only when the condition is met. |

Nothing changes on existing templates until an author turns on an upload for a question.

## Edge Cases & Limitations

- A missing required upload never blocks submission. It's only flagged.
- There is one Triage folder per case. It can't be deleted from the checklist. If the whole Triage checklist is deleted, the next upload creates a new one.
- When cases are merged or requests are moved between cases, a Triage checklist only merges into the other case's Triage checklist, never into a normal checklist.
- Restoring a deleted Triage folder while the case already has a new one brings the old folder back as an ordinary folder.
- If a template upgrade removes the question a file was uploaded for, the file stays on the case but no longer counts toward any question.

## Related Features

- [Building Templates](./README.md)
- [Fields, Lists, and Tables](./fields-and-tables.md)
- [Conditional Visibility](./conditional-visibility.md)
- [Working with Lists](../filling-out/working-with-lists.md)
- [Submitting](../filling-out/submitting.md)
- [Document Collection](../../document-collection/README.md)
- [Automatic Data Extraction](../../document-collection/data-extraction.md)
