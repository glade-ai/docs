# Required Documents Check

## Overview

The pre-filing review checks the filing packet against the document slots the case's district actually requires, and reports anything missing before submission. This is a blocking check.

## Key Behaviors

### Requirements come from each district's rules

- **Required documents come from each district's own rules.** Instead of a list maintained form by form, the check reads the required-document list for the case's filing district and chapter — the same list that drives the filing packet checklist. When a district's required documents change, the review follows automatically.
- **Each missing document is reported as its own item.** A packet missing five required documents produces five blocking items, each naming the document, and each needing its own attorney sign-off. Signing off on one document does not clear the others, and withdrawing sign-off on one document re-gates only that document.
- **Findings name the document they are about.** Each missing required document is reported using the district's own label for that slot — "Payment Advices", for example — so a packet missing several documents produces one clearly-titled finding per document. Previously every one of those findings carried the same generic title, so a case missing three documents showed three identical rows and you had to open each to learn what it meant.
- **The review is the only place a missing required document stops a filing.** Submission no longer runs a separate missing-document check of its own at the final step. Once each missing document in the review is resolved or signed off, the submission goes ahead. Before, a filing could still be turned away on the last click for a document the district requires. The filing packet preview still shows how many required documents are missing and flags each missing document in the list.
- Documents a district requires **only when they apply** are not reported as missing when they are absent — they have to be valid only if they are provided.
- Documents that apply only to joint filings are required on joint cases and skipped on individual cases. If Glade cannot yet tell whether the case is joint, that document is reported as not evaluated rather than as missing, so an individual filing is never blocked over a joint-only form.
- If the district's required-document list cannot be determined at all, the review reports the check as not evaluated instead of blocking the filing.
- **A missing document may now block where it previously only warned.** Because required-document status comes from each district's rules, a document the district marks as required is treated as gating. Pay advices are the common case: in districts whose rules require them, a missing paystubs file now blocks submission rather than showing a warning.
- **The second debtor's pay advices are governed by the district's rules too.** On a joint filing, whether Debtor 2's pay advices are required now comes from the filing district's document list like every other requirement, and appears as its own named item in the pre-filing review. Previously this rule sat inside the filing engine instead of the district's document list, and a joint case whose second debtor legitimately had no pay advices — because they are unemployed, retired, or self-employed — failed at submission with an error that nothing in Glade could clear, no matter how many times the packet was reviewed and signed off. See [Who can clear a blocking finding](./clearing-findings.md) for how this item is cleared.

### Fee and means-test forms

- **Four fee and means-test forms are now hard-required when the case calls for them**, and a missing one blocks like any other required document:
  - **Form 103A** (application to pay the filing fee in installments) and **Form 103B** (application for a fee waiver) — required when the debtor has elected that fee treatment.
  - **Form 122A-2** (Chapter 7 means test calculation) and **Form 122C-2** (Chapter 13 calculation) — required for above-median cases.
  These four were previously checked only if they had already been uploaded; their absence produced no finding at all. A Chapter 7 case where the debtor elected fee installments could reach filing with no Form 103A while the review reported "All required documents attached". If your team relied on that message alone, re-check any case filed before this change that involved a fee installment election, a fee waiver, or an above-median means test.
- Each of the four is demanded only when the case's own answers call for it. Form 103A is not required on a Chapter 7 filing where the debtor paid the fee outright.

### Skeleton filings

A skeleton filing submits only the minimum set of documents a district accepts to open a case, with the remaining schedules and forms filed afterwards. The pre-filing review now takes that into account:

- When a case is submitted as a skeleton filing, the required-documents check reads the district's **skeleton packet** requirements instead of its full-packet requirements. A document the district requires only in the complete packet no longer blocks a valid skeleton submission.
- Documents a district requires only when they apply are treated the same way in skeleton mode as in a full filing — absent is not the same as missing.
- The filing packet checklist and the list of expected documents still show the district's full shape either way. Only what the review treats as *required* changes; nothing disappears from the packet view.
- **Forms that are due later stay out of a skeleton packet and its review.** When a document already on the case is one the district does not file in a skeleton packet — for example Form 121 or Form 122A-1 left over from an earlier compile — the skeleton packet no longer lists it as an extra document, and a skeleton review no longer flags it as "e-filing document not supported". Previously every court-tagged document on the case was added to the skeleton packet, so these forms appeared in it with "not supported" warnings even though the district files them later. A document the district's rules do not recognize, such as a file your team added by hand as "Other", still appears in the skeleton packet. A form is left out only when none of the district's rules put it in a skeleton packet, so a form that is part of the skeleton packet for one chapter still appears for that chapter.
- Filings that are not marked as skeleton are unchanged and continue to be checked against the district's complete required-document list.
- Each review records the mode it ran in, so a result can be read back against whether it was checked as a skeleton or a full packet.

Skeleton requirements are defined per district, alongside that district's other filing rules. Kentucky Eastern is now set up for electronic filing, with its required documents pre-selected for skeleton submissions.

- **Check work on the eFiling screen follows the filing's current mode.** Both **Run checks** and the automatic re-run, when a review is out of date, use the mode the filing is in now. A review run in the other mode counts as out of date, so switching a filing between a skeleton filing and a full filing runs the checks again. A full-packet review does not clear a skeleton filing, and a skeleton review does not clear a full filing.
- **Submitting a skeleton filing sends only the skeleton packet.** Documents the district files later are not included in that submission.
- A filing is a skeleton filing when the petition is generated with **Use skeleton petition** checked. The electronic filing packet then shows a **Skeleton filing** badge. Generating the petition again without that box checked makes the filing a full packet. The choice is kept for the browser you are working in; it is not a setting saved on the case.

## Edge Cases & Limitations

- The required documents check reports on the separate documents in the filing packet. Forms that are folded into the consolidated petition rather than filed as their own document are not reported individually.

## Related Features

- [Pre-filing Review](./README.md)
- [Required documents in the filing packet](../filing-packet/required-documents.md) — how each district's expected documents are configured and locked into the packet.
- [Packet checks](./packet-checks.md)
- [Who can clear a blocking finding](./clearing-findings.md)
