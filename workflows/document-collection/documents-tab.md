# The Documents Tab

## Overview

The Documents tab collects everything gathered on a case in one place, organized into the same sub-groups as the Document Checklist. It is available from the side panel, the full-screen view, the modal, and the document pane, and all of them show the same organization.

## Key Behaviors

- **Sub-groups follow where a file actually sits**, so the Documents tab and the Document Checklist agree on which checklist item a document belongs to. Files that had been moved between checklist items previously stayed grouped under the item they were originally uploaded to, so a document could appear in the wrong place — or look missing — on the Documents tab while the checklist showed it correctly.
- **Moving a file renames it to match its new home.** When a file is moved to a different checklist item, its name updates along with its location. Documents your team added manually keep the name they were given and are not renamed by a move.
- **Requested files that have not been uploaded yet still appear**, as empty placeholder rows, so the tab shows the full picture of what has been asked for rather than only what has arrived.
- **Each file appears once.** A file referenced by more than one part of a case — including a case where a step can be reached by more than one path — is listed a single time instead of being duplicated.
- **The item count matches what you can see.** The "N items" label on a group counts the rows actually shown, including placeholders for files not yet uploaded.
- **Downloading a group as a zip produces the same folder structure** you see on screen.
- **Completed e-signature requests file their documents here.** A signed document and its signing certificate land in a **Signed Documents** group once the request completes, so they sit with the rest of the case's documents rather than only inside the e-signature task — see [E-Signatures](../e-signatures.md). These files are not added to the compiled petition.

## Edge Cases & Limitations

- Files moved between checklist items **before** the Documents tab grouping fix may still display the name they carried in their old location, even though they are now grouped correctly. Renaming the file from the detail pane corrects it.

> TODO: Confirm whether the one-off repair of historical document names has been run in production. If it has, the limitation above can be removed.

## Related Features

- [Document Collection](./README.md)
- [Document Requests](./document-requests.md)
- [Renaming and Downloading Files](./renaming-and-downloading-files.md)
- [E-Signatures](../e-signatures.md)
