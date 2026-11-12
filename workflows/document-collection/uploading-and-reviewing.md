# Uploading and Reviewing Documents

## Overview

Clients upload documents against the file slots on a document request, and your team reviews them — accepting, rejecting, moving, or removing files — until the checklist is complete. This page covers the upload, rejection and replacement, submit-for-review, and re-open loop between clients and your team.

## Key Behaviors

- Clients upload documents through the portal. Each uploaded file is linked to its corresponding file slot.
- Each uploaded file is listed under its file slot by its own file name. For a short period in August 2026 every uploaded file in the Document Requests checklist displayed as **"Untitled file"** regardless of its real name; the names are stored and now display correctly again, with no re-upload needed. Folder names were never affected.
- **The delete control on an uploaded file deletes it.** Clicking the trash icon next to a file used to open the file for viewing instead, so the only way to remove a document was to open it and use **Remove** from the document view. The trash icon now removes the file directly, and the drag handle in the same cluster of controls responds again too.
- **Deleting a document from the case's Documents list takes it off its checklists too.** Whether you delete one row or several at once, the document leaves every checklist item it is filed under on the case, including the **Triage** folder. Undo puts it back everywhere it was. Previously the document disappeared from the Documents list but stayed on its checklist item or in Triage, so the checklist still counted a document your team had deleted. If the document is a paystub or profit & loss statement in an income folder, deleting it also removes its income figures, and undo restores them.
- **A client's remove follows an upload Glade AI has filed.** When a client removes a file they uploaded on a questionnaire card after Glade AI has moved it out of Triage to a checklist item, the file is removed from wherever it was filed. Previously nothing was removed, even though the remove appeared to succeed. A client still cannot remove a file your team has filed into a folder the client cannot see.
- Files can be moved from one document request to another using a dropdown that lists the available destination requests. If the source document request is currently in review, a warning message asks you to confirm before proceeding — moving files out changes the review status. If all files in an in-review request are moved out, the request status resets from in review to in progress.

### Glade AI's check of an upload

- **A check that never finishes is marked unavailable.** While Glade AI checks an uploaded document, the document shows "Glade AI is evaluating this document…" and **Re-run AI** is disabled. If no result arrives within about four hours, the document now shows "AI review unavailable" and **Re-run AI** becomes available again. Previously a check that was dropped before it finished left the document showing "evaluating" indefinitely, with no way to re-run it.
- **Files over 100 MB are not checked by Glade AI.** A very large upload is kept on the case as normal, but it gets the "Not able to validate the document using AI" result, the same one oversized images already get. Review these files by hand.
- **A document with open AI findings moves to Needs Review.** On firms with Glade AI document findings turned on, a document Glade AI approved no longer stays **Approved** when its findings check turns up something. Once the check finishes with at least one finding still open, the document moves to **Needs Review**. Previously only a blurry, expired, or wrong document moved it there, so a document with content findings could read Approved.
  - This happens once, when the findings arrive. Approve the document after reviewing it and it stays Approved, even if the findings are checked again.
  - It applies only to a document Glade AI approved. A status a person on your team set is left as it is, including an approval made while the findings were still being checked.
- **Approving or reopening a document keeps what Glade AI found.** When someone on your team marks a flagged document **Approved**, or sets it back to **Needs Review**, only the document's review status changes. The AI's verdict stays with the document, so the blurry, expired, or doesn't-match-the-request flags you approved past are still visible. Previously approving replaced the verdict with a clean one, and the flags disappeared without a trace.

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
- Documents deleted from the Documents list before the checklist fix, while still filed on a checklist, were not cleaned up. They still appear on their checklist item; remove them from the checklist directly.
- A stuck Glade AI check is only marked unavailable after about four hours, so a document can show "evaluating" for that long before **Re-run AI** becomes available.
- Documents a person approved before approvals stopped clearing the AI verdict keep the cleared verdict. Their earlier flags come back only if Glade AI checks the document again.
- Clearing a document's last blurry, expired, or wrong-document flag can still return it to Approved while other AI findings on it are open. Check the findings before relying on the Approved status.

## Related Features

- [Document Collection](./README.md)
- [Document Requests](./document-requests.md)
- [Renaming and Downloading Files](./renaming-and-downloading-files.md)
- [AI-Suggested File Names](./ai-suggested-file-names.md)
- [Client Portal](../../intake/client-portal/README.md)
