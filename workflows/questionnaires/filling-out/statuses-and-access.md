# Statuses and Access

## Overview

A questionnaire moves through a small set of statuses as it is filled out, reviewed, and completed, and who can see or edit it depends on assignment, firm membership, and collaborator permissions. This page covers the statuses, sending a questionnaire back for changes, how a submitted questionnaire looks to the client, and access control.

## Key Behaviors

### Statuses

Questionnaires progress through statuses: **in progress**, **submitted for review** (if review workflow is enabled), **changes requested** (when a reviewer sends it back to the client), **completed**, and **skipped**.

For who reviews a submitted questionnaire, who can edit it while it is in review, and requesting changes, see [Questionnaire Review](./review-flow.md).

A completed questionnaire can be re-opened — see [Re-opening and Re-syncing](../case-data/reopening-and-resync.md).

### Sending a questionnaire back for changes

A reviewer can send a questionnaire that is **submitted for review** back for changes. The action and the dialog title are **Send back for changes**. The recipient step is **Assigned now**, and it asks **Who fixes it? They become its assignees, get the feedback task, and are the only ones who can edit it until it's resubmitted.** The client option reads **{name} (client)**, or **The client**. Confirm with **Send back to {n} person** or **Send back to {n} people**. A separate review action is **Approve & send back…**, which confirms as **Approve & send back**.

The people pre-selected in that choice depend on who actually works in the questionnaire:

- **The client is pre-selected only while they hold the questionnaire with edit access.** On a questionnaire the client fills in, they are selected as before. On one the firm fills in and the client never had — such as the Bankruptcy Schedules — the client is not selected, so the reviewer no longer has to untick them each time.
- **The team member who submitted it** is pre-selected while they are still part of the firm.
- **If neither applies**, the client is pre-selected so the questionnaire still goes to someone who can fix it.
- The reviewer can change the selection before sending. A send back made without choosing anyone goes to the same people the choice pre-selects.

### How a submitted questionnaire appears to the client

When a questionnaire uses the review workflow, a client who has submitted it sees it marked **Submitted — under review** with a clock icon, and the "Complete this task" prompt is removed — so the client can tell the questionnaire is already in and does not look like it still needs their attention. Your team's dashboard continues to show "Review required by you" for the same questionnaire.

**The review email names whoever submitted the questionnaire.** When a questionnaire goes into review, its reviewers can be emailed that "{name} has submitted the following form to your case". The name in that sentence, and the sender name on the email, are now the person who actually submitted it. Previously both always showed the client's name — even on questionnaires such as the Bankruptcy Schedules that your team fills in and submits — so reviewers were told the client had submitted a form they never touched. When a client submits their own questionnaire, the email reads as before. The email is sent only when the questionnaire's template has email notifications turned on, which is off by default.

Anyone with view or edit access who opens a questionnaire that is not currently editable for them — for example, a client opening a questionnaire they have already submitted for review, or a view-only team member opening one that is still in progress — sees the questionnaire's answers in read-only form. Previously some of these combinations showed a "We are generating your form results…" message that never cleared (most noticeably after submitting a questionnaire for review from the client's own profile); that stuck message no longer appears for anyone who has permission to view the questionnaire.

### Access Control

If you navigate to a questionnaire you are not assigned to and are not a member of the firm it belongs to, you see a "You don't have access to this questionnaire" screen. This applies to direct links shared by others — opening the link shows the access denied message rather than an error.

### Collaborators

Collaborators (additional team members) can be assigned to questionnaires with view or edit permissions.

## Configuration

- The review workflow and assignees are set on the template — see [Template Settings](../templates/template-settings.md).

## Related Features

- [Questionnaires](../README.md)
- [Filling Out Questionnaires](./README.md)
- [Submitting a Questionnaire](./submitting.md)
- [Questionnaire Review](./review-flow.md)
- [Re-opening and Re-syncing](../case-data/reopening-and-resync.md)
- [Client Portal](../../../intake/client-portal/README.md)
