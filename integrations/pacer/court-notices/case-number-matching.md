# Case Number Matching

## Overview

Glade links each incoming court notice to a case by its case number, and uses the same matching when you search by case number. This page covers the case-number formats Glade treats as equivalent, transferred cases, and what happens when one case number could belong to two different clients.

## Key Behaviors

### Case number matching across formats

Courts write the same case number in several different formats — for example `26-18233`, `26-bk-18233`, and `0:26-bk-18233` — and some districts add the assigned judge's initials on the end (for example `8:25-bk-08186-RCT`). Glade treats all of these as the same case number when it links court notices and when you search, so a difference in format no longer prevents a match.

A **four-digit year** is recognized as well. Some court portals write the year in full, as `2026-12345` rather than `26-12345`. Both forms are now read as the same case, so a number copied from one of those portals links and searches the same way as a number written the usual way.

- **Incoming court notices** link to the right case even when the notice writes the case number in a different format than the one stored on the workflow. Previously an exact-text mismatch could leave a notice unlinked, so notices for a case could pile up without ever attaching to its activity timeline.
- **Dashboard case-number search** matches a workflow regardless of which format you type. Searching for `26-18233` finds a case stored as `26-bk-18233` or `0:26-bk-18233`, and the reverse also works.
- **Court Notices search** now works the same way. Searching the Court Notices list by case number finds the case whichever format you type and whichever format the notice was stored in — the form printed on the notice in your hand, the form your workflow records, or the form a court portal gives you. Previously this search compared the text as typed, so whether it found anything came down to whether you happened to type the same form Glade had stored. Typing `26-bk-19440` for a case recorded as `26-19440` returned nothing at all. Searching by anything other than a case number — a client name, a subject phrase, part of a number — behaves exactly as it did.
- **A notice whose case number omits the district** is read correctly. Some courts write the number as `26-bk-19440`, with no district prefix in front of it. Notices written that way previously failed to process at all rather than arriving with an unusual case number, so they never reached the case. Notices that write the number in full keep their district prefix, as before.

Notices that were already stranded by an earlier format mismatch are not re-linked on their own. If a case is missing court notices you expected to see, contact Glade to re-sync it. Search is a separate matter: it reads whatever is already stored, so every notice your firm already has is findable by case number immediately, with nothing to re-process.

Case-number matching decides how a notice is **searched for and linked**. It is not why a notice is missing from a case: the most common reason for that is simply that no case number has been recorded on the workflow, leaving nothing to match against. Record the court's case number on the workflow if your firm's notices are not attaching.

### Case transfers

When a bankruptcy case is transferred to a different court and assigned a new case number, PACER sends electronic notices to the new case number. Glade automatically associates those incoming notices with the original workflow, so your case activity timeline stays complete without manual re-linking. The association is based on the transfer notice in the PACER email, which identifies the originating case number.

### When one case number belongs to two different clients

Two of your firm's cases filed in **different districts** can be written with the same year and sequence — one `2:26-bk-21382`, the other `9:26-bk-21382`. Strip the district off and both read as `26-21382`, so on its own that number does not say which client a notice belongs to.

Glade uses the rest of what the notice carries to decide, and declines to link the notice when nothing settles it.

- **The district decides where it can.** Most notices carry the district in their own case number, and most workflows record it too, so the two cases are told apart on the strongest signal available.
- **The debtor name is the backstop.** Where the district is not available on both sides, the name in the notice's case caption is compared against the client on the case.
- **When nothing on the notice settles it, the notice is left unlinked.** It stays visible in the Court Notices list and can be attached to the right case by hand. Previously the notice attached to whichever of the two cases came back first, which was effectively arbitrary and could change between notices with no apparent cause — the same case number would send some notices to one client and some to the other. A firm reading those notices was advising a client off another client's docket.
- **One client with several workflows is not a conflict.** A case that converts from one chapter to another carries its case number to the new workflow, so a single client legitimately holds two workflows under one number. Notices link normally in that situation; only a case number spanning two *different* debtors is treated as ambiguous.
- **Correcting one client's case number no longer disturbs the other's notices.** Where a number is shared, changing it on one workflow claims and releases only that workflow's own notices, and leaves the other client's notices where they are.

An unlinked notice is recoverable — a confidently wrong link is not, which is why Glade declines rather than guessing. The trade is that a small number of notices that would previously have been linked (to the right case or the wrong one, unpredictably) now sit unlinked until someone attaches them.

**Notices linked before this correction are not re-examined on their own.** If your firm files in more than one district, ask Glade to review your existing court-notice links — a report can be run over the affected case numbers and the mis-linked notices moved to the right client. Where the two clients' names on a case differ only by a title or suffix on the person's record (for example `J.D.` or `Mediator` recorded as part of the name), tidying the client record lets the notices link on their own.

## Edge Cases & Limitations

- A court notice whose case number belongs to two different clients in different districts is left unlinked when nothing on the notice identifies which client it is for. It has to be attached to the case by hand — Glade does not pick one.
- Court notices already linked before the ambiguous-case-number correction shipped are not re-checked automatically, so an existing wrong link stays wrong until Glade repairs it. See [When one case number belongs to two different clients](#when-one-case-number-belongs-to-two-different-clients).
- Court notice search matches on case number only when what you type reads as a case number. Anything else is matched as ordinary text, so a partial number finds only notices whose stored text contains it.

## Related Features

- [Court Notices](./README.md)
- [Case numbers](../case-numbers.md)
- [Proofs of claim and the claims register](./claims.md)
