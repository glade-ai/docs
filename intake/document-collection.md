# Document Collection

## Overview

Document collection enables creators to request specific files from clients as part of a workflow. The feature is managed by the `noodle-documents` microservice, with `noodle-api` orchestrating events and notifications. Creators define document request templates with a checklist of required and optional files, and clients upload documents through the client portal. Uploaded files can be reviewed, approved, or rejected by the creator's team.

## Key Behaviors

- A `DocumentRequest` is a template defining the files to collect. It contains one or more `DocumentRequestFile` entries, each specifying a file name, description, ordering, required/optional status, and whether the file is "for your eyes only" (restricted visibility).
- When a document request is assigned to a client within a workflow, a `DocumentRequestUser` instance is created, linking the document request to a specific person and user workflow.
- Document request users progress through statuses: `in-progress`, `in-review`, `succeeded`, `skipped`, and `failed`.
- Each file slot in the request becomes a `DocumentRequestUserFile` for the client, tracking upload status (`incomplete`, `complete`, `action-required`), rejection messages, and file metadata.
- Clients upload documents via the portal at `/{creatorSlug}/document-requests/{documentRequestUserId}`. Each uploaded file is associated with a `DocumentRequestUserFileDocument` linking to the actual stored document.
- Files can be rejected by a reviewer with a rejection message, setting the file status to `action-required` and notifying the client. Clients can then re-upload.
- A client can submit the document request for review once all required files have been uploaded. The `canSubmitForReview` check verifies `uploadedRequiredFiles >= totalRequiredFiles`.
- The review workflow tracks whether the document request is expecting a review (status `in-review` with no rejected files) via the `isExpectingAReview` method.
- Reviewers are tracked via `DocumentRequestReviewer` entities, associating specific team members with document request review responsibilities.
- Document request completion emits events consumed by `noodle-api` to trigger downstream workflow steps, task updates, activity logging, email notifications, and socket notifications.
- Document requests support collaborator assignment, allowing multiple team members to participate in the review process.
- The `isForCreator` flag on a document request indicates whether the document request is for the creator's internal use (e.g., the attorney uploads documents) rather than the client.

## Configuration

- **Document request templates** (`DocumentRequest`) define the title, slug, followup settings, auto-assignment behavior, archival status, type, and whether it is for the creator.
- **Document request files** (`DocumentRequestFile`) define each file slot: file name, description, ordering, required flag, "for your eyes only" flag, and optional integration metadata (e.g., PACER integration slug and file name).
- **Followup cadence** can be configured per document request and per document request user instance with a cadence value and units (minutes, hours, days, weeks, or none).
- **Document request types**: `basic` for standard file uploads, `income-data` for structured income data collection. Income data files can track metadata including income source, pay frequency, start/end dates, and monthly dollar values.
- **Internal data types** on files (`income-data`, `asset-data`, `personal-data`, `prompt-data`) enable structured data extraction from uploaded documents.
- **Integration support**: Files can be associated with external integrations (e.g., PACER) via `integrationSlug` and `integrationFileName`, enabling auto-generated legal documents to be included in the checklist.
- **Email notifications** can be toggled per document request template via `emailNotificationsEnabled`.

## Edge Cases & Limitations

- Skipping a document request user sets status to `skipped` but does not remove uploaded files; unskipping returns the status to its previous state.
- The `submitForReviewModalCloseForAttorney` and `submitForReviewModalCloseForClient` flags on `DocumentRequestUser` track whether the "submit for review" modal has been dismissed, preventing repeated prompts.
- File validation status is stored as JSONB (`validationStatus`) with a status string and optional `approvedBy` field, but the schema is loosely typed.
- The compiled document (`compiledDocumentId` on `DocumentRequestUser`) links to a generated document that aggregates all uploaded files, but this is optional and may be null.
- Archiving a document request template (`isArchived`) prevents it from being used in new workflows but does not affect existing instances.

## Related Features

- [Client Portal](./client-portal.md)
- [Case Questionnaire](./case-questionnaire.md)
- [Webforms](./webforms.md)
