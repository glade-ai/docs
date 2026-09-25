# Workflow Switch

## Overview

A workflow switch moves a case from one workflow to another within the same service — most often a Chapter 7 that needs to become a Chapter 13. Rather than starting the client again from scratch, Glade opens the case on the new workflow, carries the client's work across, links the two together, and archives the case being left behind. Firm staff run a switch from the case itself; clients are not involved and are not notified.

## Key Behaviors

### What a case can switch to

- The choices offered are the **other workflows in the same service** as the case's current one. A firm that offers Chapter 7 and Chapter 13 under one bankruptcy service can move a case between them.
- Only enabled workflows are offered. A workflow outside the service is not selectable, so a case cannot be moved somewhere the firm has not set up as an alternative for it.
- Switching to the workflow the case is already on is refused.

### What the client keeps

**Most of the case does not move — it is shared.** The two cases are linked as one matter, so the schedules, creditors, property, means test answers, and everything else recorded against the matter are readable from the new case straight away. Nothing is copied and nothing is re-entered.

What belongs to the case rather than the matter is carried across:

- **Document checklists and the client's uploaded files**, with their review and validation status intact. A document a reviewer already accepted arrives accepted, not waiting to be looked at again.
- **The Income Organizer's records.**
- **The credit report**, which is adopted rather than pulled again — no second hard inquiry on the client's credit file, no second charge, and no purchase prompt for a report the case already holds.
- **Invoices and retainers.**

### How document checklists arrive

The new case may already ask for some of the same documents, so checklists are combined rather than stacked:

- **Where the new case has no equivalent checklist**, the whole checklist moves across as it stands.
- **Where the new case already has one**, the client's files are moved onto it, matched **requirement by requirement on the requirement's name** — so a file uploaded against "Paystubs" lands on the new case's "Paystubs" rather than wherever the position happened to fall. Moved files sort after anything the new checklist already held, so a reviewer's place in the list is not disturbed.
- **A moved file completes the requirement it lands on** and is no longer counted against the one it came from, the same as moving a file by hand.
- Moved files appear in the new case's **Documents** tab, not only inside the checklist.
- **Joint filings keep their two debtors apart.** A case with a checklist for each debtor arrives with both, each holding its own documents.
- **A checklist is not duplicated when its step eventually runs.** The switch opens the new case's checklists immediately so the client's documents have somewhere to land; when the workflow step that would normally create that checklist reaches its turn, it takes over the one already there rather than opening an empty second copy beside it.
- The checklist on the archived case is left as it was — a record of what was asked for there.

### What has to be answered

A workflow asks its own set-up questions, and the outgoing case cannot always answer them.

- Questions the outgoing case can answer are **carried over automatically**, including where the two workflows word the same option differently — a "Chapter 7 joint" selection is matched to the target's "Chapter 13 joint".
- Anything that cannot be carried is **listed before you confirm**, and you answer it as part of the switch.
- A question whose wording leaves more than one possible match is treated as unanswered and put to you rather than guessed at.

### Watching a switch run

A switch is several steps, and each one is recorded as it happens.

- **A progress view shows each step and its outcome** while the switch runs. You can leave the page and come back to it.
- **If a step fails, the switch carries on and records the failure** rather than stopping halfway with no account of what happened. By the time the individual steps run the case has already moved, so an abandoned switch would leave the case moved and unexplained.
- **The outcome is written to the new case as an internal note**, always — including a clean switch with nothing to report. That note also appears in the case's activity history, so a switch is visible from either place. An absent note means the switch never ran, rather than being ambiguous.
- Switching shows in the activity history under its own label rather than as a general status change.

### What does not happen

- **Steps on the new case do not fire.** The client is not emailed about a retainer they have not signed, no credit report is pulled, and nothing is sent. The case reaches those steps in the ordinary way as the client works through it.
- **The client is not told.** Internal notes are staff-only, and Glade does not message the client that their case has moved. Tell them yourself if they should know.
- **The archived case is not deleted.** It stays as a record, linked to the new case.

### Billing

Invoices on the new case are raised from **that** workflow's invoice templates. A switched case is no longer billed against the workflow it just left.

## Configuration

Nothing is configured for a switch itself. What a case can switch to follows from how your firm's service is set up:

| Depends on | Effect |
|------------|--------|
| Workflows grouped under one service | Determines which workflows a case can be moved between. |
| Whether a workflow is enabled | A disabled workflow is not offered as a destination. |
| The target workflow's invoice templates | Decide what the case is billed for after the switch. |

## Edge Cases & Limitations

- A case can only move to a workflow in its own service. Moving a case to a workflow your firm keeps under a different service is not supported — contact Glade if a firm needs two workflows treated as alternatives for each other.
- The client is not notified. Anyone who needs to know the case has moved has to be told outside Glade.
- A switch that fails part-way leaves the case on the new workflow with the failures recorded in the note. Read the note before deciding what to repair; running the switch again is safe and reports that there is nothing left to move.
- Documents already moved are not moved a second time by a repeat run.
- The archived case keeps its own checklists showing what was asked for there, so the same requirement can appear on both cases. Only the new case's copy holds the client's files.
- A checklist requirement whose name differs between the two workflows is carried across as a requirement of its own rather than merged, so a renamed requirement can arrive alongside the new case's version of it.
- A case that has already been switched, then switched back, accumulates a linked chain of archived cases. The client sees only the current one.

## Related Features

- [Document Collection](document-collection/README.md) — the checklists and files a switch carries across.
- [Income Organizer](income-organizer/README.md) — the income records carried with the case.
- [Status Tracking](status-tracking/README.md) — where the switch appears in a case's activity history.
- [Credit Reports](../intake/credit-reports/README.md) — the report the new case adopts rather than re-pulling.
