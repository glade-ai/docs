# Glade AI Filing from the Triage Folder

## Overview

A case's **Triage** folder holds documents waiting to be filed: every upload a client makes from a questionnaire question, plus anything staff drop in for Glade AI to sort. For firms where it's turned on, Glade AI files these documents. Once it has read a document in the Triage folder, it chooses the item on the case's checklist where the document belongs and moves it there. If it can't decide, it leaves the document in Triage for staff and notes why. This page covers which documents are filed and where they go, what staff and clients see, and how a person's own filing interacts with Glade AI's.

## Key Behaviors

### How a document is filed

- Filing starts after Glade AI has read a document in the Triage folder. It doesn't read the file again. It works from what it already found (the type of document, its suggested name, and whether it matched what was asked for) and from the names and descriptions of the items on the case's checklists.
- For a questionnaire upload, Glade AI also knows which question the file was uploaded for and which list entry it belongs to. A document dropped straight into the folder is filed on its contents alone.
- Any item on the case's checklists can be chosen, except:
  - items in the Triage checklist itself;
  - checklists that are for your team only;
  - pay organizer checklists;
  - checklists that have been skipped.
- **Glade AI only files a document when it's confident.** A low-confidence pick, a document that matches no item, or a file that bundles several documents together stays in Triage.
- **The reason goes on the document.** When a document is left in Triage, the reason is added to the end of its Glade AI review note ("Glade AI routing: left in Triage…"). For a low-confidence pick, the note names the item Glade AI thought most likely. Staff can read it in the review panel and file the document by hand.
- Filing doesn't message the client and doesn't send the usual "file uploaded" notifications.
- The file keeps its link to the question it was uploaded for after it is moved. Data read from it still fills that question's list entry, including when Glade AI is run again from the item it was filed in.

### Review status in Triage and after filing

- **Documents in Triage stay at Needs Review until they are filed.** The Triage folder doesn't say what document it expects, so a document waiting there isn't approved just for being there.
- **A filed document is checked against the item it is filed in.** For example, a pay stub uploaded on a vehicle question and filed into the paychecks item is checked as a paycheck and approved. It isn't checked as the vehicle registration the question asked for, so it doesn't stay stuck at Needs Review.
- When the questionnaire's own check already found the document was what the question asked for, and the item it's filed into is named for the same document, that result is reused rather than checked again. "Bank statement" and "Bank statements (last 3 months)" are an example. A document dropped straight into the folder, or one that didn't match its question, is always checked again against the item it is filed into.
- A file still waiting in Triage is checked against its question, as before.

### A person's filing always wins

- If someone on your team moves a document out of Triage before Glade AI files it, Glade AI leaves it where the person put it.
- If someone later moves a document Glade AI filed, the person's choice stands, and Glade records that the AI's filing was undone.

> TODO: Confirm whether staff can ask Glade AI to file a document again from the dashboard (a "Route again" action), and where that control appears.

### Staff dropping documents into Triage

- Staff can add documents to a case's Triage folder for Glade AI to file. This is offered only where AI filing is turned on for the firm.
- If the case doesn't have a Triage folder yet, Glade creates one the first time a document is dropped in. Staff drops and questionnaire uploads share the same folder, whichever comes first.
- A workflow that isn't attached to a case can't use the Triage folder.

> TODO: Confirm the name and location of the staff action for adding a document to Triage (the source changes refer to "Add to Triage").

### Triage activity

Glade keeps an activity log for each case's Triage folder, newest first. It records when a document is uploaded (and whether it came from a questionnaire question or was dropped straight into the folder), filed by Glade AI, left in Triage because it couldn't be filed, moved by a person, or deleted.

> TODO: Confirm where the Triage activity log is shown to staff.

### What the client sees

- The upload card under a questionnaire question says where each file is now:
  - **With your legal team** while it sits in the Triage folder;
  - **Filed in** the checklist and item it was moved to, once it has been filed by Glade AI or by a person.
- A file moved into an item only your team can see is shown as filed, without the checklist or item name.
- When a document is moved, an open upload card updates straight away without a page reload. The staff Documents tab is also told about the move.

> TODO: Confirm the staff Documents tab now refreshes on its own when a document is moved by Glade AI or by another team member.

## Configuration

| Setting | Where | Effect |
|---|---|---|
| AI filing from the Triage folder | Turned on per firm by Glade | When on, Glade AI files documents out of the Triage folder, and staff can drop documents into Triage for it to file. When off (the default), documents stay in Triage until staff file them by hand. |

> TODO: Confirm how a firm asks to have AI filing turned on.

## Edge Cases & Limitations

- Glade AI can file a document in the wrong item. Move it by hand. The move is kept, and Glade records it.
- A file that combines several documents is never split. It stays in Triage for staff.
- Documents that were filed and left at Needs Review before filed documents were checked against their own item stay that way until Glade AI is run on them again. They are then checked against the item they sit in.
- The reason note is only added when Glade AI first tries to file the document, so a later retry can't undo a reviewer's approval.
- Staff can't drop documents into Triage while AI filing is off for the firm. On its own, a document in the folder would never be filed.

## Related Features

- [Document Uploads on Questions](../questionnaires/templates/document-upload-questions.md)
- [Uploading and Reviewing Documents](./uploading-and-reviewing.md)
- [Document Requests](./document-requests.md)
- [The Documents Tab](./documents-tab.md)
- [Automatic Data Extraction](./data-extraction.md)
