# Adding Documents to the Packet

## Overview

Documents reach the filing packet from inside the eFiling modal, from the case's normal document area, or from your team's own uploads under **Case Documents**. This page covers how each route places a document in a packet slot, and what happens when adding a document fails.

## Key Behaviors

### Adding documents from the eFiling modal

- **A document added to the packet as "Other" must be given a name.** When you add a document under the generic **Other** type, the packet needs a filename for it. Leaving that name blank and clicking **Add to packet** shows the validation message on the field straight away. Previously the first click did nothing at all — no error, no document added, no indication of what was wrong — and the message appeared only after you had clicked into the name field and back out, which read as the button being broken.
- When you save documents to the filing packet and the save does not go through, the document selection window stays open and shows the specific reason it failed (for example, the exact validation message), so you can correct the problem and try again. Previously the window could close on a failed save without anything being saved, and only a generic error was shown.

### Recognized documents uploaded outside the filing modal

Some court documents — for example, documents pulled from PACER — belong in a specific slot of the electronic filing packet. When you add such a document through the case's normal document area instead of from inside the eFiling modal, Glade now recognizes documents whose file name matches a known filing document and automatically places them in the correct packet slot.

- Recognition is based on the document's file name. A document whose name matches a known filing document is slotted automatically; a document with an unrecognized name is added to the case as usual and can be slotted manually.
- Previously, a recognized document uploaded outside the modal was left unslotted and excluded from the filing packet. Now a PACER document dropped into the case this way is included in the Electronic Filing Packet without re-uploading it through the modal.

### Putting an uploaded case document into a packet slot

A document your team uploaded under **Case Documents** can be placed into a filing packet slot, and it holds that slot in place of the version Glade generated for it. Use this where the copy that has to be filed is one your team prepared or had signed — a local form, a bifurcated disclosure, a signed page — rather than the generated one.

- **The uploaded file takes over the slot.** The most recently placed document is what is filed, so a signed upload supersedes the generated PDF without your team having to remove anything first.
- **Assigning it sticks.** For a period, placing a Case Documents upload into an e-filing slot appeared to work and then silently came back unassigned, with no way to make it hold. If your team gave up trying to file a local form they had uploaded, it can be placed now.
- Nothing about how other documents reach the packet changes, and a generated document left in its slot is filed as before.

## Related Features

- [Filing Packet](./README.md)
- [Filing packet document types](./document-types.md)
- [PDF and image conversion](./file-conversion.md)
