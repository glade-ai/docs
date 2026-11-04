# Questionnaire Review

## Overview

When a questionnaire uses the review workflow, submitting it does not complete it straight away — it goes to **submitted for review**, and a reviewer at the firm checks it before it is completed. This page covers who reviews a questionnaire, who can edit it while it is in review, the tasks and case activity the review creates, requesting changes from the client, and how approving a questionnaire completes it.

## Key Behaviors

### Who reviews a questionnaire

- **A firm user submitting for review can choose the reviewers** — between 1 and 25 members of the firm. Clients and other non-firm users cannot choose reviewers.
- **Without a choice, the case's workflow owners review it.**
- Each submission for review replaces the reviewer list with the one chosen for that submission.

### Editing while a questionnaire is in review

- **Only the reviewers can edit a questionnaire in review.** For everyone else — other firm staff, assignees, and the client — the questionnaire behaves as if it were completed and shows its answers read-only. Previously any firm staff member or assignee could keep editing a questionnaire after it was submitted for review.
- **Nobody can edit a questionnaire once changes have been requested on it.**
- Glade's own automatic updates to a questionnaire are not affected by these rules.
- The same rules apply to edits made through an AI assistant connected to Glade: an assistant cannot change answers on a questionnaire that is in review or has changes requested.

### Submitting for review

When a questionnaire is submitted for review:

- The questionnaire's open tasks are completed, and each reviewer is given a **Review Questionnaire** task.
- A **submitted for review** entry is added to the case activity, naming who submitted it. When the client submitted it, it counts as client activity.
- **Every Forms & Schedules file is built at this point**, so reviewers can check the generated documents rather than waiting for completion. If the petition was just generated, those files are reused instead of being built twice.

### Requesting changes

A reviewer can send a questionnaire in review back to the client:

- The status changes to **changes requested**, open tasks are completed, and the client is given an **Address Questionnaire Feedback** task.
- A **changes requested** entry is added to the case activity, naming the reviewer.
- The client resubmits the questionnaire for review, which starts the review again and records a new submitted-for-review entry.

Only firm users can request changes, and only on a questionnaire that is currently in review.

> TODO: Confirm where the **Request changes** and **Resubmit** buttons appear and when they became available, and how the client addresses feedback while the questionnaire cannot be edited.

### Approving and completing

- **A reviewer completing a questionnaire that is in review counts as approving it.** An **approved by** entry naming the reviewer is added to the case activity just before the completion entry, and the usual completion steps follow — workflow steps advance, emails go out, and case data is updated. See [Submitting a Questionnaire](./submitting.md#completion).
- **Files are rebuilt only if answers changed during review.** When no answer was edited after the questionnaire was submitted for review, the files built at submission are kept. When an answer was edited, or Glade cannot tell, the files are built again.
- Only a reviewer can complete a questionnaire from review. A questionnaire with changes requested cannot be completed until it has been resubmitted and reviewed.

## Configuration

- The review workflow is turned on per template — see [Template Settings](../templates/template-settings.md).
- Reviewers are chosen when submitting for review; otherwise the case's workflow owners are used.

## Edge Cases & Limitations

- If two reviewers act on the same questionnaire at the same moment, only the first decision is applied; the second is refused.
- When no reviewers were chosen and the case's workflow owners change during review, edit access follows the change immediately, but **Review Questionnaire** tasks already created stay with the previous owners.
- A questionnaire in review does not receive case data updates — see [Case Data Sync](../case-data/case-data-sync.md).

## Related Features

- [Statuses and Access](./statuses-and-access.md)
- [Submitting a Questionnaire](./submitting.md)
- [Filling Out Questionnaires](./README.md)
- [Tasks](../../status-tracking/tasks.md)
- [Template Settings](../templates/template-settings.md)
