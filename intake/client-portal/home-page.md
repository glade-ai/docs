# Portal Home Page

## Overview

The client portal home gives the client a single view of where they stand across every case they have with your firm: a **Your next step** hero card, a path timeline of every step, their team, their balance, and upcoming meetings. This page covers what the home page shows, how path statuses are labeled, how items open from the path, and how the page keeps itself current.

## Key Behaviors

### Home page layout

- **Your next step** — a hero card at the top of the home page tells the client what to do next:
  - When there is an outstanding task, the card shows the task and a button to open it.
  - When the client has nothing outstanding but a meeting is scheduled, the card shows the booking title and date with framing such as "Your meeting is today", "Your meeting is tomorrow", or "Your meeting is coming up".
  - When the client is fully caught up with no upcoming meeting, the card shows "You're all caught up" with contextual copy describing what's happening on the firm's side (under review, firm working, upcoming, or nothing).
  - When the client has no outstanding case work but does have a comment from the firm awaiting a reply, that comment becomes the next step instead of "You're all caught up". Case work takes priority — a comment is offered only when nothing else is active.
  - Every "all caught up" variant includes an **Ask a question** link that takes the client into the most recent active case with the chat panel open so they can leave a comment for the team.
- **Path timeline** — beneath the hero card, the home page lists every step and attachment across the client's active case (document checklists, questionnaires, agreements, signatures, bookings, invoices, credit reports). Items are grouped by status: completed → under review → scheduled → active → upcoming. Active items show the assigned team members (or "No assignees yet" if none have been picked).
- **Comments awaiting a reply appear on the timeline too** — a comment or discussion the client has been asked to respond to shows as an active row with a chat icon and a **Reply** action, even though it is not a step in the workflow. Previously the home page listed only workflow steps, so a client could be shown "You're all caught up" while the firm's own follow-up list held dozens of outstanding "Respond to Comment" tasks for that same client.
- **Open buttons** — only items the client can actually act on right now show an Open button. Items that haven't been triggered yet, or that are waiting on the firm, render as upcoming without a button.
- **Voided e-signatures are hidden** — a voided e-signature request is removed from the client's path. Because a voided signature cannot be acted on, it does not appear as an item and is not counted toward its step's assignments, so the client no longer sees a dead "document voided" card or a stray prompt to finish an assignment that no longer exists. The firm's own dashboard and chat still show the voided indicator.
- **Booking states** — bookings on the path appear in three sub-states: **Active now** (no time picked yet — the client needs to schedule), **Scheduled** (time is set, with a date subtitle), or **Completed** (the meeting has passed). Imminent meetings include a "Today, …" or "Tomorrow, …" prefix on the date.
- **Your team rail** — shows up to ten team members assigned to the case; any beyond ten roll up into a "+N supporting" caption.
- **Balance card** — shows the paid/contracted ratio from the most recent case's invoices, with a **Total / Paid / Due** breakdown beneath the headline so the client can still see the full picture once an invoice is paid off. A fully-paid case shows "Total $X · Paid $X · Due $0.00" rather than collapsing to an uninformative "$0.00". When the case's invoice is on an **active payment plan**, the card also shows the installment amount and cadence (for example, "$200.00 monthly") and the next payment date, so a client paying down a balance on a plan sees that reflected. When the client has invoices but owes nothing, the card shows a green checkmark with "You're all paid up", a positive confirmation that the balance is fully paid. This is distinct from the "All paid up" message shown when there are no invoices, or all invoices have been voided — in that case the card reads "All paid up" with a full progress bar. A completed or canceled payment plan is not shown on the card.
  - **Choosing an invoice to pay** — selecting the Balance card opens a picker of the client's invoices. Invoices that have not been generated yet — those whose amount has not been assigned — do not appear in the picker and are left out of the balance totals, so the client no longer sees duplicate "$0.00" rows for invoices that are still being prepared.
- **Coming up rail** — surfaces the next scheduled meeting on a date tile.
- **Top bar** — every page includes a global top bar with the firm's branding, a hamburger menu (Meetings, Home, Library, Support chat, and a "Visit {firm}" external link), a **Need help** popover with help videos, and an account menu. The firm logo links back to the home page.
- **Loading state on first open** — when the home page first opens, it shows a brief loading placeholder while it gathers the client's steps, rather than momentarily showing "You're all caught up" before the real information appears.
- **Status badges on active path items** are easier to read against their background than they previously were.

### Status meanings

The portal resolves a wide range of internal status values into four user-facing labels:

| Label | Applies to |
|-------|-----------|
| Completed | Steps that succeeded, finished, were agreed to, were paid, or have an `agreedAt` timestamp. |
| Under review | Steps in review, under review, submitted for review, or awaiting review. |
| Active now | Steps in progress, pending, awaiting response, started, initiated, or with an approval request sent. |
| Upcoming | Steps that have not yet been triggered, or whose entity does not exist yet. |

Within each group, items appear in the original order they would be encountered in the workflow.

### Opening an item from the path

Selecting a questionnaire, document checklist, agreement, invoice, or other item from the path timeline opens it as its **own full page**, rather than as a panel layered over the home page.

- Each item page carries a **Back** button that returns the client to their portal home.
- Because each item has its own page, a client can be sent a link that opens straight to one specific item — a particular questionnaire or checklist — instead of landing on the home page and having to find it. This is useful when your team is walking a client through one outstanding thing over the phone.
- A client who arrives on an item directly from a link still lands back on their portal home when they use **Back**, rather than reaching a dead end.
- This applies to the client portal only. How your own team opens the same items from the firm dashboard is unchanged.

### Live updates

The client portal home keeps itself current without the client having to do anything. It refreshes on its own when:

- the client completes or submits a task (for example finishing a questionnaire, uploading a document, or booking a meeting);
- someone on the firm updates the case (for example marking a step complete or generating an invoice); and
- the client returns to the portal tab after being away, or reconnects after losing their connection.

Because the home updates automatically, there is no manual refresh step — the Your next step card, path timeline, and balance all reflect the latest state as soon as it changes.

## Edge Cases & Limitations

- A booking-request step that hasn't been triggered yet renders as **Upcoming** on the path timeline, not as **Active now**. The client cannot schedule until the step has actually fired and the booking has been sent.

## Related Features

- [Client Portal](./README.md)
- [Client Tasks](./client-tasks.md)
- [Multi-Case Clients](./multi-case-clients.md)
- [Documents and Signing](./documents-and-signing.md)
- [Payment Plans](../../payments/payment-plans/README.md)
