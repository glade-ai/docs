# Notice Classification

## Overview

Because the trigger is an exact match on notice type, what an automation fires on depends entirely on how the incoming notice was classified. This doc covers how notices are classified, the notice types available, what counts as a rescheduled or reset notice, and the docket text carried on each notice.

## Key Behaviors

### How notices are classified

Classification now works from the notice itself before falling back to interpretation: when a notice carries a recognisable official form number or filing title, that identifier decides the type outright, so the same document is classified the same way every time rather than being read afresh on each arrival.

Several types were added or narrowed:

- **Means test and income statements are now four distinct types** rather than one general classification — Chapter 7 Statement of Current Monthly Income (Form 122A-1), Chapter 7 Means Test Calculation (Form 122A-2), Chapter 13 Statement of Current Monthly Income (Form 122C-1), and Chapter 13 Calculation of Disposable Income (Form 122C-2). An automation can now target the specific form and chapter instead of firing on all of them.
- **Three new types** are available: Statement of Financial Affairs, Notice to Court of Intent to Argue, and Withdrawal and Substitution of Attorney.
- **Trustee Supplemental Report** is available as a type, and appears in the court notices type dropdown. It covers a trustee's supplemental report requesting dismissal — including the version citing failure to make plan payments, and one saying an order will follow. These reports were previously classified as **Motion to Dismiss**, and staff could not relabel them because the type did not exist. A supplemental report that asks to reschedule confirmation is still classified as **Confirmation Hearing**, and a certificate that only mails the report is still **Certificate of Mailing**. Existing notices classified as Motion to Dismiss are not changed; relabel them by hand where needed.
- **Adversary Complaint** is available as a type. A complaint opening an adversary proceeding against a debtor now classifies as Adversary Complaint instead of arriving with no type at all, so these notices can be filtered on the court notices list and used as an automation's match type. Only the complaint itself is classified this way — later filings in the same adversary proceeding, such as answers, summonses, and motions, are not.
- **521 Compliance** is only applied when the notice explicitly cites Section 521. Notices that merely resemble a compliance notice are no longer classified this way.
- **Investigating Asset** is now limited to trustee reports that explicitly describe an ongoing investigation into estate property. Recovered-asset and claims-bar notices, routine 341 meeting reports, no-distribution reports, and final reports are classified as what they are and no longer land here. An automation set up to watch for asset investigations fires on far fewer, more relevant notices as a result.
- **A continued 341 meeting is separated by whether the meeting was held.** Two new types — **341 Meeting Held and Continued** and **341 Meeting Not Held and Continued** — cover a meeting that took place and was then continued (usually for further documents) and a meeting that did not take place and was continued. Both previously landed on **341 Meeting Held**, so a firm could not automate a no-show continuation separately from a meeting that went ahead. A 341 that was held and concluded, a reset or rescheduled 341, a certificate of mailing, and a continued *confirmation* hearing are not taken by the new types.
- **A confirmed delinquency in Chapter 13 plan payments** has its own type, so a firm can automate on it rather than reading it out of a more general classification.
- **Rescheduled** and **Reset** are available as types of their own. A hearing that is moved, or a 341 meeting that is reset, used to be classified as an ordinary Hearing, Confirmation Hearing, or 341 Meeting Held — so a firm had no way to treat "the date has changed" differently from the original notice. An automation can now match the move itself, and both types appear in the court notices report's type filter.
- Several neighbouring definitions were narrowed at the same time so they stop taking each other's notices: certificates of service and mailing, requests for a claims deadline, first-meeting reports, and the difference between a confirmation hearing that has been *requested* to move and one that actually has.

**A notice is listed before it has been classified.** A newly arrived notice appears on the court notices list as soon as it is read, and picks up its type when classification finishes a moment later.

- A notice whose classification does not complete — a temporary outage, for example — is retried rather than being recorded as a notice with no type. A notice that ends up with no type is one Glade read and could not place, not one it never got to.
- Automations are evaluated once the type is known, so a notice that arrives before its classification is still matched against your rules. Case linking, the existing triggers and filters, and the handling of notices that arrive before their case is linked are all unchanged.

> TODO: Confirm the exact name of the Chapter 13 plan-payment delinquency type as it appears in the notice type picker — an automation's trigger is an exact match on the type, so the wording matters.

**Notices already on your cases are not reclassified.** These rules apply to notices received from now on. A notice that arrived under the old classification keeps the type it was given, and an automation matching a new type will not fire retroactively for it. If your firm needs its existing notices re-read for Rescheduled and Reset, contact Glade — this can be run for a firm on request.

### What counts as rescheduled or reset

The two new types are decided from the court's own wording on the docket — language such as *Confirmation Hearing Rescheduled* or *Meeting of Creditors Reset* — before any interpretation is applied, so the same wording classifies the same way every time.

- **The move has to have happened.** A trustee's report merely *requesting* a reschedule is not a Rescheduled notice, and a certificate of mailing about a reset 341 is not a Reset notice. Both are classified as what they are.
- **Hearing, Confirmation Hearing, and 341 Meeting Held are unchanged as types**, but they no longer absorb reschedule and reset wording. An automation matching one of those three fires on fewer notices than before — check any automation or saved report that was relying on catching moved dates that way.

### Docket text on a notice

Every court notice now carries the **docket text** and **docket number** recorded on the docket entry it came from. Both appear in the notice list, in the notice detail view, and in CSV and report exports, so your team can read the court's own wording for an entry without opening the notice or looking it up on PACER. Notices already on your cases show their docket text immediately.

## Edge Cases & Limitations

- Classification changes apply only to notices received after the change. Notices already on your cases keep the type they were originally given. Rescheduled and Reset can be applied to a firm's existing notices on request, but only those two types are re-read.
- Rescheduled and Reset depend on the court's docket wording. A district that moves a hearing without saying so in those terms produces an ordinary Hearing or 341 notice, so a firm outside the districts that use this language may see neither type.

## Related Features

- [Court Notice Automations](./README.md)
- [Triggers and Filters](./triggers-and-filters.md)
- [PACER Integration](../../integrations/pacer/README.md)
