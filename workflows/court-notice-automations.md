# Court Notice Automations

## Overview

Court notice automations act automatically when classified PACER court notices arrive on a case — sending emails and creating tasks. Your firm sets up rules that match incoming notice types, and Glade fires the configured actions to the right recipients with the right context — without anyone on your team having to watch the inbox. Automations are managed under **Workflow Reports → Court Notices → Automations**.

## Key Behaviors

- Each automation is owned by a creator (your firm) and listens for PACER notices that match its rules.
- An automation has a **name**, an **enabled/disabled** toggle, a **match type** (the notice type to match — for example "Notice of Hearing"), optional **chapter** and **judge** filters, and a list of **actions**.
- When a matching notice is processed, the system loads case context, resolves who each action applies to, fills in the tokens, and runs the actions in order.
- **Sender identity**: automation emails are sent from your firm owner's email address, and the sender name shown to recipients is your firm's name. Replies go to the firm owner.
- Each fire is recorded as a run on the automation, so you can see when each automation last ran and whether it succeeded. The automation's **last run** time and **last run status** appear on the list view. A run also records an outcome for each individual action it ran.
- **Idempotency**: the same incoming court notice never triggers the same automation twice. If the same upstream event is processed again (for example after a retry), the duplicate fire is ignored. This applies per action, so a reprocessed notice does not send a second email or create a second copy of a task.
- **Failure isolation**: if one automation fails — for example because a recipient email is invalid — other automations matching the same notice still run. The same holds between actions on a single automation: if one action fails, the remaining actions still run, and the run is recorded as **partial** rather than failed.

### Actions

An automation runs a list of actions rather than a single email. Each action has its own type, its own settings, and its own enabled/disabled state, and actions run in the order they are listed. Two action types are available:

- **Send email** — sends the configured email to the resolved recipients.
- **Create task** — creates a task on the case so the work lands in someone's queue instead of only in an inbox.

Automations that existed before actions were introduced continue to work unchanged: each one now shows a single **Send email** action carrying the subject, body, and recipients it already had. There is nothing to re-create.

#### Create task

- The task's **assignees** are chosen the same way as email recipients — case-party tokens (`debtor1`, `debtor2`, `attorney`) and team members at your firm. At least one assignee is required.
- **Due in** sets the task's due date as a number of days after the notice date, calculated in your firm's timezone. Leave it blank for no due date.
- The task carries a title and description, which support the same tokens as the email subject and body.
- Assignees are notified through the normal task notifications and the task appears in their inbox, exactly as a task created any other way.
- A create-task action is **skipped** when the notice is not linked to a workflow, or when none of its assignees resolve at fire time (for example because every assignee was a team member who has since been removed). Glade never creates a task with no assignee.
- Team member assignees are checked against your firm at fire time; anyone no longer at the firm is dropped.
- Two create-task actions on one automation produce two separate tasks.

### Per-action run results

Every run records a result for each action it ran, so you can tell which part of an automation worked and which did not — for example, that the email went out but the task was not created. Run status rolls up across the actions:

| Run status | Meaning |
|------------|---------|
| Ran | Every action that was supposed to run succeeded. |
| Partial | At least one action succeeded and at least one failed. |
| Failed | Every action failed. |
| Skipped | Nothing ran — for example, no recipients or assignees resolved. |

The recipients an email was actually sent to are recorded on the run, so the history shows who was contacted at the time rather than who would be contacted today.

### Naming an individual action

An automation can carry more than one action — several emails, or an email alongside a task. Each action can be given its own **action title**, so a list of three emails reads as "Chase trustee", "Notify debtor", and "Flag for review" instead of three identical "Send email" cards you have to open one at a time to tell apart.

- The title is a label for your team only. It is not shown to recipients and does not appear in the email.
- Titles are optional. An action left untitled continues to show its action type.
- A title can be up to 200 characters. Leaving it blank, or entering only spaces, clears it.
- An action's title is separate from the title of any task the action creates — naming an action does not change the task your clients or team see.

> TODO: Confirm the label and location of the action title field in the automation editor.

### Finding an automation

The find bar on the automations list matches on whole words in any order, across the automation's name, its match type, and its actions' titles.

- Searching `trustee email` finds an automation named "Email trustee" — word order does not matter, and the words do not have to be next to each other.
- All the words you type must appear in the same place: `chase trustee` matches an action titled "Chase trustee", but not an automation named "Chase" with an unrelated action titled "Trustee".
- Titles on disabled or deleted actions are not matched.
- The result count reflects the filtered list.

Previously the find bar matched only against the whole automation name and match type, start to finish, so searching `trustee email` returned nothing for an automation named "Email trustee".

### Triggers and filters

A trigger has three parts. All must match for the automation to fire:

- **Notice type** (required) — exact match against the classified PACER notice type. For example, an automation with match type "Notice of Hearing" fires only on notices classified as "Notice of Hearing".
- **Chapter** (optional) — restricts the automation to a specific chapter (Chapter 7 or Chapter 13). When left blank, the automation matches any chapter.
- **Judge** (optional) — restricts the automation to a specific judge (matched by judge initials, case-insensitive). When left blank, the automation matches any judge.

The judge picker is populated from the judges who have actually appeared on PACER notices for your firm in the last 12 months, sorted by how often they appear so the most common judges are at the top.

### How notices are classified

Because the trigger is an exact match on notice type, what an automation fires on depends entirely on how the incoming notice was classified. Classification now works from the notice itself before falling back to interpretation: when a notice carries a recognisable official form number or filing title, that identifier decides the type outright, so the same document is classified the same way every time rather than being read afresh on each arrival.

Several types were added or narrowed:

- **Means test and income statements are now four distinct types** rather than one general classification — Chapter 7 Statement of Current Monthly Income (Form 122A-1), Chapter 7 Means Test Calculation (Form 122A-2), Chapter 13 Statement of Current Monthly Income (Form 122C-1), and Chapter 13 Calculation of Disposable Income (Form 122C-2). An automation can now target the specific form and chapter instead of firing on all of them.
- **Three new types** are available: Statement of Financial Affairs, Notice to Court of Intent to Argue, and Withdrawal and Substitution of Attorney.
- **521 Compliance** is only applied when the notice explicitly cites Section 521. Notices that merely resemble a compliance notice are no longer classified this way.
- **Investigating Asset** is now limited to trustee reports that explicitly describe an ongoing investigation into estate property. Recovered-asset and claims-bar notices, routine 341 meeting reports, no-distribution reports, and final reports are classified as what they are and no longer land here. An automation set up to watch for asset investigations fires on far fewer, more relevant notices as a result.

**Notices already on your cases are not reclassified.** These rules apply to notices received from now on. A notice that arrived under the old classification keeps the type it was given, and an automation matching a new type will not fire retroactively for it.

### Docket text on a notice

Every court notice now carries the **docket text** and **docket number** recorded on the docket entry it came from. Both appear in the notice list, in the notice detail view, and in CSV and report exports, so your team can read the court's own wording for an entry without opening the notice or looking it up on PACER. Notices already on your cases show their docket text immediately.

### Video hearing details on Florida Southern 341 notices

341 meeting notices from the Southern District of Florida publish their video hearing details in a format Glade could not previously read, so the meeting ID, passcode, and dial-in number were left blank — and any automation email using the video hearing tokens sent with those details missing. These notices are now parsed into the meeting ID, passcode, and phone number, and the tokens fill in as expected.

Notices that arrived before this was fixed still have blank video hearing details. Contact Glade to have those cases re-processed if your team relies on those tokens.

### Creating a task from an automation

As well as sending an email, an automation can create a task on the case when it fires. Who that task is assigned to can depend on the notice, using **assignment rules**.

Each rule combines up to three conditions with a list of the people to assign:

| Condition | Matches on |
|-----------|-----------|
| **Chapter** | Chapter 7 or Chapter 13, compared the same way as the automation's own chapter filter |
| **Judge** | The judge on the notice, compared by initials and case-insensitive, the same way as the automation's judge filter |
| **Trustee** | The trustee named on the notice. Trustee names are free text, so they are compared ignoring capitalization and surrounding spaces |

This lets one automation route work the way your firm actually divides it — Chapter 13 notices to the Chapter 13 paralegal, notices in front of one judge to the person who covers that judge, anything from a particular trustee to both.

**How the conditions combine:**

- Each condition is joined to the next by **and** or **or**, and the rule is read strictly left to right: chapter, then judge, then trustee. There is no precedence between **and** and **or** — "chapter **and** judge **or** trustee" means "(chapter and judge) or trustee", never "chapter and (judge or trustee)". Order your conditions with that in mind.
- A condition you leave blank drops out of the rule entirely, along with the operator that joined it. It is not treated as a match. A rule with a chapter and a trustee joined by **or**, and no judge, matches a notice that is either in that chapter or from that trustee.
- A rule with all three conditions blank always matches. Use one as a catch-all so notices that fit none of your specific rules still land with someone.

**How assignees are worked out when the automation fires:**

- Every rule is evaluated against the notice, and **one task** is created — not one per rule and not one per person.
- The assignees from every rule that matched are combined. Someone named by two matching rules is assigned to the task once.
- If no rule matches the notice, no task is created and the run is recorded as skipped.
- If rules matched but none of their assignees can be resolved — for example every one of them was a team member who has since been removed — no task is created and the run is recorded as skipped.
- An automation with two separate task actions still creates two tasks, as before.

The trustee picker is populated from the trustees who have actually appeared on PACER notices for your firm in the last 12 months, most frequent first — the same way the judge picker works.

Automations set up before assignment rules existed keep working unchanged. Their single list of assignees reads as one rule with no conditions, so the same people are assigned on every firing until you add conditions.

### Recipients

Recipients are the people who receive the email when the automation fires. Three recipient kinds are supported and can be combined on a single automation:

- **Case-party token** — automatically resolves to the email address of a person on the case. Supported tokens are `debtor1`, `debtor2`, and `attorney`.
- **Team member** — a specific Glade team member at your firm. The system verifies the team member still belongs to your firm at fire time; soft-deleted team members are skipped.
- **Literal email** — a fixed email address you type in.

If an automation has no resolvable recipients at fire time (for example because every recipient was a team member who was removed), the run is logged as skipped and no email is sent.

### Tokens in the email

The email subject and body support a set of tokens that are filled in at fire time:

- `{{caseNumber}}` — the PACER case number on the matched notice.
- `{{noticeType}}` — the classified notice type that matched the automation.
- `{{clientName}}` — the primary debtor's name on the case.
- `{{judgeInitials}}` — the judge initials on the matched notice.
- `{{firmName}}` — your firm's display name.

In addition, automations can pull case-party and hearing details so the email reads like a personalized notice:

- The **first debtor's name** and, for joint cases, the **second debtor's name**, taken from the people on the case.
- The **341 meeting of creditors date and time**, taken from the linked court calendar entry for the case, or read directly from the notice when the court calendar entry for the case has not been created yet. A 341 notice and the calendar entry it produces are handled at the same moment, so the automation often used to run a fraction of a second before the calendar entry existed — which left the meeting date and time blank on the email even though the notice itself stated them. Those details now fill in either way, and the case number is no longer the only token that reliably renders on a 341 notice.
- The **video hearing join details** (for example, the meeting link, meeting ID, and passcode) when the notice is for a remote 341 meeting. Glade reads the Zoom details out of the notice text, including formats that name the trustee's meeting room without a colon before the meeting ID — the style used in the Western District of Pennsylvania, for example. Notices written that way previously produced no video hearing details at all.

#### The dial-in number is no longer included by default

The video hearing details token fills in the **meeting ID and passcode only**. The Zoom dial-in phone number is no longer part of it.

- Firms reported staff mistaking the dial-in number for a client's or a case's phone number, because it appeared in the email as a bare `Phone:` line with nothing to identify it as a Zoom number.
- A separate **video hearing phone** token is available for firms that do want the dial-in number in their emails. Add it to the subject or body where you want it to appear.
- **Nothing to change on your existing automations.** The dial-in line stopped going out on its own — you do not need to edit a template to remove it, and templates that never mentioned a phone number are unaffected.
- 341 emails sent before this change went out with the dial-in number included. Those emails are not recalled or resent.

> TODO: Confirm the in-product name of the video hearing phone token in the automation email editor's token picker.

The same case-party and hearing details are available to **Create task** actions, so a task raised from a 341 notice can state the meeting date, time, and join details in its description.

#### Debtor names on notices that are not linked to a case

Not every incoming court notice is matched to a case in Glade. When a notice is unlinked, the debtor and client name tokens have no client record to read from, and the email previously went out addressed to nobody — a discharge congratulations message opening "Dear ," is the case firms reported.

- When the notice is linked to a case, the client's name on that case is used, exactly as before. A linked name always wins.
- When the notice is not linked, or the linked client has no name on file, Glade falls back to the debtor name in the case caption carried on the court notice itself, and strips the trailing case-number text so only the name is inserted.
- If neither source has a name, the token still renders as empty and the email still sends.

#### Hearing tokens when a notice carries more than one hearing

A single court notice can schedule more than one hearing — a confirmation hearing and a 341 meeting in the same docket entry, for example. When that happens, the hearing tokens use the **341 meeting**, so an email written for the meeting of creditors quotes the meeting date rather than whichever hearing happened to be listed first.

> TODO: Confirm the exact token spellings for the debtor names, 341 meeting date/time, and video hearing join details once they are finalized in the email editor.

Tokens are case-insensitive and tolerant of extra whitespace inside the braces. Unknown tokens render as empty strings — the email still sends, with the unknown token replaced by nothing.

## Configuration

| Setting | Description |
|---------|-------------|
| Name | Display name shown on the automations list. |
| Action title | Optional label for an individual action within the automation, up to 200 characters. Internal only — not shown to recipients. |
| Enabled | Whether the automation runs. Disabled automations are ignored. |
| Match type | Notice type to match (exact). |
| Chapter | Chapter 7, Chapter 13, or any. |
| Judge | Specific judge or any. |
| Actions | One or more actions to run when the automation fires — **Send email**, **Create task**, or several of each. Each action can be enabled or disabled on its own and the actions run in listed order. |
| Recipients | Combination of case-party tokens, team members, and literal email addresses. |
| Assignment rules | For an automation that creates a task: a list of rules, each with an optional chapter, judge, and trustee condition joined by **and**/**or**, plus the people to assign. At least one assignee per rule. |
| Subject and body | Email content with optional tokens for case number, notice type, client name, judge initials, firm name, debtor names, the 341 meeting date and time, and video hearing join details. The video hearing details token carries the meeting ID and passcode; the dial-in number has its own separate, opt-in token. |
| Task assignees | For a **Create task** action: case-party tokens and team members. At least one is required; literal email addresses are not available here. |
| Task due in | For a **Create task** action: the number of days after the notice date that the task is due, in your firm's timezone. Optional. |

Edits are tracked: each save records who made the change and when, alongside who originally created the automation.

## Edge Cases & Limitations

- The match type is exact. Notices with a slightly different classification do not match — set up additional automations for related notice types if needed. This matters where a single type has been split into several: an automation that watched for means test and current-monthly-income notices needs one automation per form to keep the same coverage.
- Classification changes apply only to notices received after the change. Notices already on your cases keep the type they were originally given.
- Only the supported tokens listed above are recognized. Unknown tokens render as empty strings.
- Hearing tokens are filled from the linked court calendar entry or from the notice itself. If neither states a 341 meeting time, or the notice carries no video hearing details, those tokens render as empty strings.
- The video hearing details token no longer includes the Zoom dial-in number. A firm that needs the dial-in number in its 341 emails has to add the separate phone token to each template that should carry it.
- The case-caption fallback for debtor names only supplies a name. It does not link the notice to a case, so the other case-context tokens on an unlinked notice stay empty.
- If a recipient is a soft-deleted team member, that recipient is skipped at fire time. The automation still fires for any remaining recipients.
- Run history (every individual fire of an automation) is not yet surfaced in the UI. The automation list shows the most recent run time and status only.
- Failed runs are not retried automatically. The failure shows as the automation's last run status, and the run's per-action results show which action failed.
- Emails sent before the 341 meeting details fix went out with the meeting date, time, and join details blank. Those emails are not resent — if clients were sent a 341 notice missing its meeting details, follow up manually.
- Tasks created by an automation appear in the inbox and in the newer task views. They may not yet appear in the older dashboard task lists, which show only a fixed set of task kinds.
- A **Create task** action needs the notice to be linked to a workflow. Court notices that never matched a workflow — the majority of notices for many firms — cannot raise a task, so an automation whose only action is Create task will show runs as skipped on those notices. Pair it with a **Send email** action if someone should still be told.
- Conditional logic inside a single automation is limited to assignment rules on a task action — they decide *who* a task goes to, not whether the automation fires or what the email says. The automation's own trigger has no branching; use separate automations for separate scenarios.
- Assignment-rule conditions cover chapter, judge, and trustee only. There is no condition on other notice details.
- Assignment-rule conditions are evaluated strictly left to right with no operator precedence. A rule that mixes **and** and **or** may not mean what it reads like at a glance — check the grouping described above.
- A rule whose conditions are all blank matches every notice. Leaving a rule empty by accident assigns its people to every firing.
- Action titles are not recorded on a run's history. A run identifies which action fired, but if you rename an action later, past runs reflect the current title rather than the one in place when they ran.
- The find bar searches automation names, match types, and action titles. It does not search email subject or body text, recipients, or judge filters.

## Related Features

- [Automation Rules](./automation-rules.md) — general workflow automations driven by client actions.
- [PACER Integration](../integrations/pacer.md) — the source of court notices that drive these automations.
