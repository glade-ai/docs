# Review Email and Automatic Submit for Review

## Overview

Two settings on a document request template control what happens when a checklist is ready for review. A **review email** replaces Glade's generic "in review" email with a message your firm writes — to the **Client**, **Workflow assignees**, or both — optionally with the finished documents attached. **Submit for review automatically** moves a checklist your team fills in to review as soon as every required item is complete, without anyone pressing **Submit for Review**. Firms use them together, for example to send the client a final petition draft for review the moment it is filed into a "Final Draft" checklist.

## Key Behaviors

### Review email

- **Sent whenever the checklist reaches review.** It goes out whatever moved the checklist to **In Review** — a client submitting, your team submitting, or an automatic submit.
- **Replaces the generic email.** When a review email is set up, the standard "in review" email is not sent for that checklist. With no review email set up, nothing changes: the standard email goes out as before.
- **Recipients.** Choose **Client**, **Workflow assignees**, or both. Each group gets its own review link, and a team member who is also the client's address is not emailed twice.
- **Silent submissions are respected.** When your team submits a "for your team" checklist without checking **Notify client**, the client is left off the review email; any **Workflow assignees** chosen still receive it. See [Document Requests](./document-requests.md#checklists-for-your-team).
- **Placeholders.** The **Message** can use `{{clientName}}` (the client's name) and `{{documentRequest}}` (the checklist's name). A review link is added to the email automatically; you do not type a placeholder for it.
- **Branding.** The email uses your firm's branded email layout and logo.
- **Sent regardless of the template's email notifications toggle.** That toggle controls only the standard client notification; a review email your firm wrote is always sent.

### Attaching the finished documents

With **Attach the submitted documents** turned on, the checklist's finished documents are attached to the review email.

- Only completed files are attached. Files marked **for your eyes only**, encrypted files, and duplicates are left out.
- Attachments are capped at 20 MB in total. Documents that would push the email past that limit are left off; the email still sends.
- Documents are attached even when the checklist was submitted silently and the client cannot yet see it in the portal.

### Submit for review automatically

- **Off by default.** Turn it on per document request template.
- **Applies to checklists your team fills in** ("for your team" checklists). When the last required item is completed, the checklist moves to **In Review** on its own, through the same steps as a manual submit — client access, review tasks, and the review email all work as usual.
- **Triggered by your team's actions.** Uploading or attaching a file, moving or restoring a file into the checklist, accepting a file, or marking a file optional can each complete the checklist. Generating a petition draft straight into a checklist item also counts — see [Generating a Draft Petition](../questionnaires/petition/draft-petition.md#what-goes-into-the-draft-and-where-it-is-saved).
- **Only someone who could submit it by hand triggers it.** The automatic submit happens only when the person whose action completed the checklist has edit access to it. If a client completes the last required item, the checklist stays **In Progress**.
- It happens once. A checklist that is already in review, or that has been completed, is not submitted again.
- The client recipient of the review email, if one is set, is the one notified; otherwise the usual client notification applies.

## Configuration

Both settings live on the document request template:

- **Send email when submitted for review** — the note under the switch reads "This message replaces the standard review email for this checklist." The fields are **Subject** (up to 250 characters), **Message**, **Recipients** (**Client**, **Workflow assignees**, or both), and **Attach the submitted documents**. Clearing it returns the checklist to the standard in-review email.
- **Submit for review automatically** — on or off (off by default).

Both settings are kept when a workflow template is cloned.

## Edge Cases & Limitations

- Moves Glade makes on its own — for example moving checklists during a chapter conversion or workflow switch — never trigger an automatic submit, so clients are not emailed unexpectedly.
- If a stored review email is incomplete or malformed, Glade sends the standard in-review email instead.
- An automatic submit that fails does not stop the upload or other action that triggered it; the checklist simply stays **In Progress** and can be submitted by hand.

## Related Features

- [Document Requests](./document-requests.md)
- [Uploading and Reviewing Documents](./uploading-and-reviewing.md)
- [Generating a Draft Petition](../questionnaires/petition/draft-petition.md)
- [Document Collection](./README.md)
