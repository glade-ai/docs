# Uploading and Reviewing Documents

## Overview

Clients upload documents against the file slots on a document request, and your team reviews them — accepting, rejecting, moving, or removing files — until the checklist is complete. This page covers the upload, rejection and replacement, submit-for-review, and re-open loop between clients and your team.

## Key Behaviors

- Clients upload documents through the portal. Each uploaded file is linked to its corresponding file slot.
- Each uploaded file is listed under its file slot by its own file name. For a short period in August 2026 every uploaded file in the Document Requests checklist displayed as **"Untitled file"** regardless of its real name; the names are stored and now display correctly again, with no re-upload needed. Folder names were never affected.
- **The delete control on an uploaded file deletes it.** Clicking the trash icon next to a file used to open the file for viewing instead, so the only way to remove a document was to open it and use **Remove** from the document view. The trash icon now removes the file directly, and the drag handle in the same cluster of controls responds again too.
- Files can be moved from one document request to another using a dropdown that lists the available destination requests. If the source document request is currently in review, a warning message asks you to confirm before proceeding — moving files out changes the review status. If all files in an in-review request are moved out, the request status resets from in review to in progress.

### Submitting for review

- When all required documents are uploaded, the client can submit for review. Before submission, the system verifies that all required files are fully uploaded — if any required file is still incomplete, submission is blocked and the client sees an error message.
- When a document request is in review and no files have been rejected, it is awaiting reviewer action.

### Rejecting files and replacements

- Files can be rejected by a reviewer with a rejection message, which sets the file status to "action required" and notifies the client. Clients can then re-upload a replacement. After a re-upload, the new file is correctly recognized as ready for review.
- The rejection notice on a file clears once a replacement is accepted. A file only shows the rejection message while it is actually marked "action required" — accepting a replacement removes the notice instead of leaving the earlier rejection displayed on an accepted file. Previously the notice stuck around after acceptance, which made resolved requests look like they still needed the client's attention.
- **Accepting a replacement also unblocks the checklist.** A file that was rejected and then had a replacement accepted counts as ready in the same way as any other accepted file. Once every required file is accepted, the client's **Submit for Review** button and your team's **Mark as Completed** button are both available as normal. Previously the earlier rejection kept counting against the checklist after the replacement had been accepted, so neither side could close the request — the client saw no way to submit and the firm saw no way to complete it, with nothing on screen explaining what was still outstanding.
- **A client can submit as soon as they upload the replacement.** Uploading a new file against a rejected request clears that item for submission — the client does not have to wait for your team to accept the replacement first. Previously the rejected item kept blocking submission until a reviewer had accepted the new upload, so a client who had already done what was asked was left looking at a checklist that appeared ready with a **Submit for Review** button that would not go through. A rejected item with no replacement uploaded still blocks submission, as it should.

### Adding a document after a checklist is complete

A client can re-open their own completed checklist to add a document that turns up afterwards — a newer bank statement, a replacement ID, something your team asked for in a follow-up. Previously they had to message the firm and wait for a staff member to re-open it for them.

- **Re-open document request** is available to the client on any completed checklist of theirs. It was previously offered only on checklists your team owns, which a client rarely sees.
- Uploading into a completed checklist re-opens it, and the file's actions menu says so: on a completed checklist the option reads **Reopen & upload more documents** rather than **Upload more**, so the client knows before they act that the checklist is going back to your team.
- The completion message a client sees on a finished checklist now points them at that menu, instead of offering only a link to the chat.
- Re-opening returns the checklist to **in progress**. The client uploads, submits for review as normal, and it comes back to your team for review like any other submission.
- **Submit for Review works immediately after a re-open.** The button used to stay stuck in a loading state for the rest of the visit once a checklist had been re-opened or completed, which broke the last step of exactly this loop — the client could re-open and upload but never submit.

## Edge Cases & Limitations

- A rejected item with no replacement uploaded still blocks submission.

## Related Features

- [Document Collection](./README.md)
- [Document Requests](./document-requests.md)
- [Renaming and Downloading Files](./renaming-and-downloading-files.md)
- [AI-Suggested File Names](./ai-suggested-file-names.md)
- [Client Portal](../../intake/client-portal/README.md)
