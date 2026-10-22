# Statuses and Access

## Overview

A questionnaire moves through a small set of statuses as it is filled out, reviewed, and completed, and who can see or edit it depends on assignment, firm membership, and collaborator permissions. This page covers the statuses, how a submitted questionnaire looks to the client, and access control.

## Key Behaviors

### Statuses

Questionnaires progress through statuses: **in progress**, **submitted for review** (if review workflow is enabled), **completed**, and **skipped**.

A completed questionnaire can be re-opened — see [Re-opening and Re-syncing](../case-data/reopening-and-resync.md).

### How a submitted questionnaire appears to the client

When a questionnaire uses the review workflow, a client who has submitted it sees it marked **Submitted — under review** with a clock icon, and the "Complete this task" prompt is removed — so the client can tell the questionnaire is already in and does not look like it still needs their attention. Your team's dashboard continues to show "Review required by you" for the same questionnaire.

Anyone with view or edit access who opens a questionnaire that is not currently editable for them — for example, a client opening a questionnaire they have already submitted for review, or a view-only team member opening one that is still in progress — sees the questionnaire's answers in read-only form. Previously some of these combinations showed a "We are generating your form results…" message that never cleared (most noticeably after submitting a questionnaire for review from the client's own profile); that stuck message no longer appears for anyone who has permission to view the questionnaire.

### Questionnaires that have moved to the new client portal

Glade is moving client questionnaires to a new questionnaire engine one template at a time. Once a client's questionnaire has moved, the client continues it in your firm's new client portal rather than in the older Glade app.

- **A client who opens the questionnaire is sent to the portal.** Opening it from the client's own profile or from their inbox in the older app takes them to the portal in the same tab.
- **Inside a side panel**, the questionnaire isn't redirected. The panel shows an **Open questionnaire** button instead.
- **Your team, working from the firm dashboard,** is offered **Open in Glade** for the same questionnaire.
- **Re-opening a submitted questionnaire** that moves it to the new engine — for example with **Edit Responses** — also takes the client to the portal.
- **If the questionnaire moves while the client has it open**, saving is refused and the message tells them it now opens in your firm's new client portal and to reload to continue there. Your team sees the same refusal with a prompt to open it in Glade.

> TODO: Confirm which questionnaire templates have moved so far and how firms are told when theirs moves.

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
- [Re-opening and Re-syncing](../case-data/reopening-and-resync.md)
- [Client Portal](../../../intake/client-portal/README.md)
