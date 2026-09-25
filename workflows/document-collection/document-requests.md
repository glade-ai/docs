# Document Requests

## Overview

A document request defines the checklist of files your team wants to collect from a client as part of a workflow. Each request is built from file slots, is assigned to a specific client and workflow, and moves through a set of statuses as the client uploads and your team reviews. This page covers how requests and their checklists are set up, assigned, tracked, and shared.

## Key Behaviors

- A document request defines the files to collect. Each file slot specifies a file name, description, ordering, whether the file is required or optional, and whether the file is restricted to your team only ("for your eyes only").
- When a document request is assigned to a client within a workflow, it creates an individual assignment linking the request to that specific client and their workflow.
- Document request assignments progress through statuses: **in progress**, **in review**, **succeeded**, **skipped**, and **failed**.
- Each file slot tracks its upload status: **incomplete**, **complete**, or **action required**.
- **Each requested file is labeled Required or Optional on the checklist**, matching how the slot was set up on the request. For a period in August 2026 every file on the checklist displayed as **Optional** — including files your team had marked required — so neither staff nor clients could tell which documents actually had to be provided. The labels are correct again, and no re-upload or re-configuration is needed; the requests themselves were never changed.
- Reviewers from your team are assigned to document requests to handle the review process.
- When a document request is completed, it triggers downstream workflow steps, task updates, activity logging, email notifications, and real-time notifications.
- Document requests support collaborator assignment, allowing multiple team members to participate in review.
- Paging through a long list of checklists returns each one exactly once — rows are no longer repeated or skipped between pages.

### Checklists for your team

- A document request can be marked as "for your team" (e.g., the attorney uploads documents) rather than for the client.
- **Submitting a "for your team" checklist is silent by default.** When your team submits a firm-owned checklist for review, the client is not emailed and no client review task is created — useful while a petition is still being drafted or while training staff on a live case. A **Notify client** checkbox appears on the submit prompts (both the rename step and the ready-to-submit confirmation); check it when the draft is genuinely ready for the client to look at, and the client is notified and given access to review the checklist as before. Submitting silently also withdraws client review access if an earlier submission had granted it, so reopening and resubmitting silently never leaves the checklist open in the portal. Checklists assigned to clients are unaffected — submitting those notifies your team as it always has.

### Who can see which checklists and documents

- **Collaborators on a case can see the checklists they were given access to.** Anyone working the case from outside your firm — a client's collaborator, a co-filer, another party on the workflow — sees exactly the document requests they hold view access to, and nothing else. Your own team continues to see every checklist on the workflow. Previously only members of the firm that created the workflow could load the list at all, so a collaborator opening a file's details hit a permissions error even on documents they were entitled to see. Someone with no access now sees an empty list rather than an error, and the count shown alongside a list reflects only what that person can actually see.
- **Clients can open the documents held on their own case.** A file listed in a client's case documents opens in the preview for them, including files your firm produced rather than the client — court documents pulled from PACER, the generated petition, and other staff-uploaded files attached to the matter. Previously a client who opened one of these was refused with a permissions message and could not read a document filed on their own case, even though it was listed for them. Files marked **for your eyes only** are unaffected and stay firm-only, and a client still sees only the cases they are a party to.

## Configuration

- **Document request templates** define the title, followup settings, auto-assignment behavior, archival status, type, and whether it is for your team.
- **File slots** define each requested file: name, description, ordering, required flag, "for your eyes only" flag, and optional integration metadata (e.g., PACER integration for auto-generated legal documents).
- **Followup reminders** can be configured per document request and per individual client assignment, with a customizable frequency (minutes, hours, days, weeks, or none).
- **Document request types**: "basic" for standard file uploads, "income data" for structured income data collection. See [Income Documents](./income-documents.md).
- **Integration support**: File slots can be associated with external integrations (e.g., PACER) to include auto-generated legal documents in the checklist.
- **Email notifications** can be toggled on or off per document request template.

## Edge Cases & Limitations

- Skipping a document request assignment sets its status to "skipped" but does not remove uploaded files. Unskipping returns it to its previous state.
- A compiled document that aggregates all uploaded files can be generated, but this is optional and may not always be present.
- The **Download all as a single PDF** option in a document request's overflow menu is only available when at least one file has been uploaded to that slot. The option does not appear for slots with no files yet.
- Archiving a document request template prevents it from being used in new workflows but does not affect existing assignments.

## Related Features

- [Document Collection](./README.md)
- [Uploading and Reviewing Documents](./uploading-and-reviewing.md)
- [The Documents Tab](./documents-tab.md)
- [Client Portal](../../intake/client-portal/README.md)
