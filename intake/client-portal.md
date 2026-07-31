# Client Portal

## Overview

The client portal is where clients interact with your firm's workflows. Clients access the portal through a link you send them and can view and complete assigned tasks including questionnaires, document uploads, invoices, bookings, and messaging.

## Key Behaviors

- Clients reach the portal through a link you share or through a workflow landing page that describes the workflow and provides an entry point.
- The portal URL is branded to your firm using your unique URL slug (e.g., `yourfirm.glade.app/...`).
- Clients start a workflow by following a link that walks them through the workflow's initial steps.
- Each workflow step can include questionnaires, document collection, payments, bookings, e-signatures, and messaging.
- Clients sign up or sign in through the portal. Each client is associated with your firm's account.
- **Signing up with an email Glade already recognizes** — when a client tries to sign up with an email that Glade already has on file (for example, from a prior sales contact, demo, intake widget, or CRM import), the portal no longer bounces them with a generic "user already exists" error:
  - If the email exists but no password has been set, Glade emails the client a one-time code and switches the form to a verification screen. Entering the code finishes the account and signs them in.
  - If the email already has a password set, the form shows an inline error and a prominent **Sign in instead** button that opens the sign-in screen with the email prefilled.
  - Refreshing the page mid-verification shows a "Session expired" panel with a button back to the sign-up screen — the in-progress sign-up is not silently lost without explanation, but it does have to be re-entered.
- When adding a joint filer or collaborator to a case workflow at initiation, you can provide an optional phone number. When present, the phone number appears in the case initiation summary and is saved with that person's contact record.
- You can configure workflow steps to automatically assign tasks to yourself or to the client, so tasks are ready as soon as a workflow starts.
- The portal includes a branded "Client login portal" accessible from your public page.

### Home page

The client portal home gives the client a single view of where they stand across every case they have with your firm.

- **Your next step** — a hero card at the top of the home page tells the client what to do next:
  - When there is an outstanding task, the card shows the task and a button to open it.
  - When the client has nothing outstanding but a meeting is scheduled, the card shows the booking title and date with framing such as "Your meeting is today", "Your meeting is tomorrow", or "Your meeting is coming up".
  - When the client is fully caught up with no upcoming meeting, the card shows "You're all caught up" with contextual copy describing what's happening on the firm's side (under review, firm working, upcoming, or nothing).
  - Every "all caught up" variant includes an **Ask a question** link that takes the client into the most recent active case with the chat panel open so they can leave a comment for the team.
- **Path timeline** — beneath the hero card, the home page lists every step and attachment across the client's active case (document checklists, questionnaires, agreements, signatures, bookings, invoices, credit reports). Items are grouped by status: completed → under review → scheduled → active → upcoming. Active items show the assigned team members (or "No assignees yet" if none have been picked).
- **Open buttons** — only items the client can actually act on right now show an Open button. Items that haven't been triggered yet, or that are waiting on the firm, render as upcoming without a button.
- **Voided e-signatures are hidden** — a voided e-signature request is removed from the client's path. Because a voided signature cannot be acted on, it does not appear as an item and is not counted toward its step's assignments, so the client no longer sees a dead "document voided" card or a stray prompt to finish an assignment that no longer exists. The firm's own dashboard and chat still show the voided indicator.
- **Booking states** — bookings on the path appear in three sub-states: **Active now** (no time picked yet — the client needs to schedule), **Scheduled** (time is set, with a date subtitle), or **Completed** (the meeting has passed). Imminent meetings include a "Today, …" or "Tomorrow, …" prefix on the date.
- **Your team rail** — shows up to ten team members assigned to the case; any beyond ten roll up into a "+N supporting" caption.
- **Balance card** — shows the paid/contracted ratio from the most recent case's invoices, with a **Total / Paid / Due** breakdown beneath the headline so the client can still see the full picture once an invoice is paid off. A fully-paid case shows "Total $X · Paid $X · Due $0.00" rather than collapsing to an uninformative "$0.00". When the case's invoice is on an **active payment plan**, the card also shows the installment amount and cadence (for example, "$200.00 monthly") and the next payment date, so a client paying down a balance on a plan sees that reflected. When the client has invoices but owes nothing, the card shows a green checkmark with "You're all paid up", a positive confirmation that the balance is fully paid. This is distinct from the "All paid up" message shown when there are no invoices, or all invoices have been voided — in that case the card reads "All paid up" with a full progress bar. A completed or canceled payment plan is not shown on the card.
  - **Choosing an invoice to pay** — selecting the Balance card opens a picker of the client's invoices. Invoices that have not been generated yet — those whose amount has not been assigned — do not appear in the picker and are left out of the balance totals, so the client no longer sees duplicate "$0.00" rows for invoices that are still being prepared.
- **Coming up rail** — surfaces the next scheduled meeting on a date tile.
- **Top bar** — every page includes a global top bar with the firm's branding, a hamburger menu (Meetings, Home, Library, Support chat, and a "Visit {firm}" external link), a **Need help** popover with help videos, and an account menu. The firm logo links back to the home page.
- **Loading state on first open** — when the home page first opens, it shows a brief loading placeholder while it gathers the client's steps, rather than momentarily showing "You're all caught up" before the real information appears.

### Multi-case clients

When a client has more than one active case with your firm, the portal adapts:

- **Sidebar** — a left-hand sidebar appears once the client has two or more active visible cases. Archived, canceled, and closed cases are excluded; cases linked into a chain (for example a refile) collapse to a single most-recent representative.
- **Search** — once the client has more than three cases, the sidebar adds a search input. Search matches both the chain representative and any linked member cases, so searching for any case in a chain finds it.
- **Auto-redirect** — for clients with two or more active cases, opening the home URL routes straight to the first case's representative. The exception is when the URL carries an activity deep link (with a specific case and comment) — the portal honors that deep link and shows the home with the targeted case opened.

### Status meanings

The portal resolves a wide range of internal status values into four user-facing labels:

| Label | Applies to |
|-------|-----------|
| Completed | Steps that succeeded, finished, were agreed to, were paid, or have an `agreedAt` timestamp. |
| Under review | Steps in review, under review, submitted for review, or awaiting review. |
| Active now | Steps in progress, pending, awaiting response, started, initiated, or with an approval request sent. |
| Upcoming | Steps that have not yet been triggered, or whose entity does not exist yet. |

Within each group, items appear in the original order they would be encountered in the workflow.

### Client timezone

The portal captures and stores a timezone for each client so that times shown to the client — appointment slots, meeting times on the home page, and reminders — appear in the client's own local time, and so that automated messages such as task follow-ups respect the client's local hours of day.

- When a client signs in or visits the portal after signup, Glade reads the timezone from their browser and saves it to their profile if no timezone has been stored yet. The client does not need to do anything for this to happen.
- The client can change the saved timezone at any time from their portal profile, using a **Timezone** dropdown. Clients who travel or who normally use Glade from a different timezone than their device's setting can use this to lock the timezone to whatever they prefer.
- The saved timezone is used both by the portal (to render meeting times in the client's local hours) and by Glade's outbound messaging (for example, the 8:00 AM–9:00 PM SMS delivery window for task follow-ups).

### Active status and tasks

The portal's "active" indicators and the Your next step card are driven by the underlying entity status, not by the task system. If a client dismisses a task whose underlying item (for example a document checklist) is still open and assigned to them, the home page continues to surface that item as their next step with the correct Open button.

- **Dismissing a task** — Every task in the home list has a trash icon that shows a **Dismiss task** label when hovered. Dismissing a task clears it from the client's list; it does not complete the underlying item. (The control was previously an unlabeled arrow that clients often mistook for "open" rather than "clear.")
- **Respond to Comment tasks** — A "Respond to Comment" task opens the reply thread for that comment directly, so the client lands where they can reply rather than on the full conversation with the comment merely highlighted.
- **Credit counseling enrollment task** — When the firm sends a credit counseling enrollment request, a task to enroll appears on the client's portal home, labeled **Get Pre-Filing Credit Counseling** before the case is filed (or **Get Post-Filing Debtor Education** afterward). Opening the task takes the client straight to the enrollment form. On joint filings, both debtors receive the task. The task clears on its own once enrollment is completed or skipped, and the client receives automated follow-up reminders to enroll while it remains outstanding. The accompanying "enrollment details needed" message now opens the enrollment card directly, instead of pointing to a button that was not shown.
- **Connect Bank Account task** — When a bank statements step is active on the client's case, a **Connect Bank Account** task appears on the portal home alongside the client's other tasks. Opening it takes the client straight to the Bank Statements Organizer, and the task clears once the client connects an account or the step is skipped. See [Bank Statements](./bank-statements.md).
- **Tasks from linked workflows** — When a client's workflow is linked to other workflows, the client tasks from those linked workflows also appear on the portal home. The client sees every task assigned to them in one place, not only the tasks on their main workflow.

### Live updates

The client portal home keeps itself current without the client having to do anything. It refreshes on its own when:

- the client completes or submits a task (for example finishing a questionnaire, uploading a document, or booking a meeting);
- someone on the firm updates the case (for example marking a step complete or generating an invoice); and
- the client returns to the portal tab after being away, or reconnects after losing their connection.

Because the home updates automatically, there is no manual refresh step — the Your next step card, path timeline, and balance all reflect the latest state as soon as it changes.

## Configuration

- You configure the portal experience through workflow templates that define the sequence of steps, triggers, and actions.
- Workflow landing pages are available for specific practice areas (e.g., bankruptcy, immigration, personal injury) and describe the workflow before a client begins.
- Products control pricing and sale state (free, not for sale, or on sale) for workflows that require payment.
- Followup reminders can be configured on questionnaire templates and document request templates with a customizable frequency (minutes, hours, days, or weeks) to remind clients of pending tasks.

## Edge Cases & Limitations

- The portal uses your firm's URL slug for routing. If you change your slug, existing links sent to clients stop working.
- Workflow initiation requires a specific step link; there is no generic "start workflow" entry point.
- Unverified users (clients who have not confirmed their account) may have limited portal functionality.
- A booking-request step that hasn't been triggered yet renders as **Upcoming** on the path timeline, not as **Active now**. The client cannot schedule until the step has actually fired and the booking has been sent.

## Related Features

- [Questionnaires](../workflows/questionnaires.md)
- [Document Collection](../workflows/document-collection.md)
