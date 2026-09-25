# Portal Access and Client Accounts

## Overview

Clients reach your firm's client portal through a link you share or a workflow landing page, then sign up or sign in to an account associated with your firm. This page covers which version of the portal clients see, how they get in, how sign-up, sign-in, and password reset behave, and how the portal records each client's timezone.

## Key Behaviors

### Which portal your clients see

Glade has a redesigned client portal — the version with the **Your next step** hero card, path timeline, and balance card described in [Portal Home Page](./home-page.md). It is now used by **every bankruptcy firm**, rather than by a hand-maintained list of firms.

- Any firm set up as a bankruptcy practice gets the redesigned portal automatically, including firms onboarded from now on. Previously each firm had to be added by hand, so newly onboarded firms stayed on the older portal until someone remembered to add them.
- Firms outside that practice area continue on the previous portal, and individual firms can still be switched over on request.
- Which portal a client sees follows the **firm whose portal they are visiting**, not the client's own account. A client who works with more than one firm sees each firm's own portal.

### Reaching the portal and starting a workflow

- Clients reach the portal through a link you share or through a workflow landing page that describes the workflow and provides an entry point.
- The portal URL is branded to your firm using your unique URL slug (e.g., `yourfirm.glade.app/...`).
- Clients start a workflow by following a link that walks them through the workflow's initial steps.
- Each workflow step can include questionnaires, document collection, payments, bookings, e-signatures, and messaging.
- When adding a joint filer or collaborator to a case workflow at initiation, you can provide an optional phone number. When present, the phone number appears in the case initiation summary and is saved with that person's contact record.
- You can configure workflow steps to automatically assign tasks to yourself or to the client, so tasks are ready as soon as a workflow starts.
- The portal includes a branded "Client login portal" accessible from your public page.

### Signing up and signing in

- Clients sign up or sign in through the portal. Each client is associated with your firm's account.
- **Signing up with an email Glade already recognizes** — when a client tries to sign up with an email that Glade already has on file (for example, from a prior sales contact, demo, intake widget, or CRM import), the portal no longer bounces them with a generic "user already exists" error:
  - If the email exists but no password has been set, Glade emails the client a one-time code and switches the form to a verification screen. Entering the code finishes the account and signs them in.
  - If the email already has a password set, the form shows an inline error and a prominent **Sign in instead** button that opens the sign-in screen with the email prefilled.
  - Refreshing the page mid-verification shows a "Session expired" panel with a button back to the sign-up screen — the in-progress sign-up is not silently lost without explanation, but it does have to be re-entered.

### Password reset emails

**Password reset emails reach everyone.** A client who asks to reset their password is sent the reset email, whoever they are and whatever they have unsubscribed from previously.

- Anyone who had ever unsubscribed from a Glade email — a booking reminder, a digest, a follow-up — was silently blocked from receiving password reset mail from then on. Nothing indicated this: the portal accepted the request and showed its "check your inbox" screen, and the email was discarded before it was delivered. The only symptom was a client insisting they never received it.
- Password reset is treated as account mail rather than something a person can unsubscribe from, so it is no longer filtered against unsubscribe preferences. Every other kind of Glade email keeps its unsubscribe link and honours the client's choice exactly as before.
- This applies to anyone who signs in to Glade, including your own team members, not only clients in the portal. A client or colleague who reported a reset email never arriving can try again — no change to their subscription preferences is needed first.

### Client timezone

The portal captures and stores a timezone for each client so that times shown to the client — appointment slots, meeting times on the home page, and reminders — appear in the client's own local time, and so that automated messages such as task follow-ups respect the client's local hours of day.

- When a client signs in or visits the portal after signup, Glade reads the timezone from their browser and saves it to their profile if no timezone has been stored yet. The client does not need to do anything for this to happen.
- The client can change the saved timezone at any time from their portal profile, using a **Timezone** dropdown. Clients who travel or who normally use Glade from a different timezone than their device's setting can use this to lock the timezone to whatever they prefer.
- The saved timezone is used both by the portal (to render meeting times in the client's local hours) and by Glade's outbound messaging (for example, the 8:00 AM–9:00 PM SMS delivery window for task follow-ups).

## Configuration

- The redesigned portal is applied automatically to bankruptcy firms; there is no per-firm setting to turn on. Firms in other practice areas that want it can request it from Glade.
- Workflow landing pages are available for specific practice areas (e.g., bankruptcy, immigration, personal injury) and describe the workflow before a client begins.

## Edge Cases & Limitations

- The portal uses your firm's URL slug for routing. If you change your slug, existing links sent to clients stop working.
- Workflow initiation requires a specific step link; there is no generic "start workflow" entry point.
- Unverified users (clients who have not confirmed their account) may have limited portal functionality.

## Related Features

- [Client Portal](./README.md)
- [Portal Home Page](./home-page.md)
- [Multi-Case Clients](./multi-case-clients.md)
