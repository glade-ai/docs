# Document Collection

## Overview

Document collection enables your team to request specific files from clients as part of a workflow. You define document request templates with a checklist of required and optional files, and clients upload documents through the client portal. Uploaded files can be reviewed, approved, or rejected by your team.

## Key Behaviors

- A document request defines the files to collect. Each file slot specifies a file name, description, ordering, whether the file is required or optional, and whether the file is restricted to your team only ("for your eyes only").
- When a document request is assigned to a client within a workflow, it creates an individual assignment linking the request to that specific client and their workflow.
- Document request assignments progress through statuses: **in progress**, **in review**, **succeeded**, **skipped**, and **failed**.
- Each file slot tracks its upload status: **incomplete**, **complete**, or **action required**.
- Clients upload documents through the portal. Each uploaded file is linked to its corresponding file slot.
- Files can be rejected by a reviewer with a rejection message, which sets the file status to "action required" and notifies the client. Clients can then re-upload a replacement. After a re-upload, the new file is correctly recognized as ready for review.
- Files can be moved from one document request to another using a dropdown that lists the available destination requests. If the source document request is currently in review, a warning message asks you to confirm before proceeding — moving files out changes the review status. If all files in an in-review request are moved out, the request status resets from in review to in progress.
- When all required documents are uploaded, the client can submit for review. Before submission, the system verifies that all required files are fully uploaded — if any required file is still incomplete, submission is blocked and the client sees an error message.
- When a document request is in review and no files have been rejected, it is awaiting reviewer action.
- Reviewers from your team are assigned to document requests to handle the review process.
- When a document request is completed, it triggers downstream workflow steps, task updates, activity logging, email notifications, and real-time notifications.
- Document requests support collaborator assignment, allowing multiple team members to participate in review.
- A document request can be marked as "for your team" (e.g., the attorney uploads documents) rather than for the client.

## Configuration

- **Document request templates** define the title, followup settings, auto-assignment behavior, archival status, type, and whether it is for your team.
- **File slots** define each requested file: name, description, ordering, required flag, "for your eyes only" flag, and optional integration metadata (e.g., PACER integration for auto-generated legal documents).
- **Followup reminders** can be configured per document request and per individual client assignment, with a customizable frequency (minutes, hours, days, weeks, or none).
- **Document request types**: "basic" for standard file uploads, "income data" for structured income data collection. Income data files can track metadata including income source, pay frequency, start/end dates, and monthly dollar values.
- **Income organizer AI processing**: When a paystub or income document is uploaded, AI automatically extracts the income data. While processing is underway, a loading indicator appears on the row. The uploaded file name is clickable even during processing — you can view the original document without waiting for AI to finish. Once AI completes, the loading indicator clears and extracted data appears. An **Edit** button is available on all income rows once processing is complete, whether the data was entered manually or extracted by AI. The Edit button is only hidden while AI is actively processing a row.
- **Income calculation mode** (employment income): When a client uploads multiple paystubs for employment income, your team can choose how Glade calculates the monthly income figures used in documents like Schedule I:
  - **All paystubs** (default): sums all selected paystubs and averages them across the unique months represented.
  - **Single paystub YTD**: uses the year-to-date totals from one paystub divided by the number of months elapsed in the year. This is useful when only one recent paystub is available or when YTD figures are more accurate than averaging multiple pay periods.
  To switch modes, click the **Calculation** button next to an employer row in the income document view. When using YTD mode, you select which paystub provides the YTD figures, and choose whether to auto-detect months elapsed from the paystub date or set the number manually. A preview of the resulting Schedule I contributions is shown before you apply changes.
  - **Apply YTD to means test**: When YTD mode is active for an employer, you can also apply the same YTD figures to the means test calculation instead of using the standard 6-month window. Toggle this option on within the YTD settings for that employer. When enabled, Glade uses the YTD gross pay divided by months elapsed to populate the means test income line for that employer. Other employers not set to YTD mode continue to use the standard calculation.
- **Structured data types** on file slots (income data, asset data, personal data, prompt data) enable structured data extraction from uploaded documents.
- **Integration support**: File slots can be associated with external integrations (e.g., PACER) to include auto-generated legal documents in the checklist.
- **Email notifications** can be toggled on or off per document request template.

## Edge Cases & Limitations

- Skipping a document request assignment sets its status to "skipped" but does not remove uploaded files. Unskipping returns it to its previous state.
- A compiled document that aggregates all uploaded files can be generated, but this is optional and may not always be present.
- The **Download all as a single PDF** option in a document request's overflow menu is only available when at least one file has been uploaded to that slot. The option does not appear for slots with no files yet.
- Archiving a document request template prevents it from being used in new workflows but does not affect existing assignments.

## Related Features

- [Client Portal](../intake/client-portal.md)
- [Questionnaires](./questionnaires.md)
