# Electronic Court Filing (eFiling)

## Overview

Glade integrates with electronic court filing systems to let you submit cases directly from the platform. Your team submits filings through the case's eFiling modal, and Glade tracks the submission's progress in real time, sends inbox notifications when status changes occur, and links those notifications back to the relevant case view.

## Key Behaviors

- Initiating a filing submission from a case opens the eFiling submission modal, where you confirm and submit the filing.
- If the case's Schedule I (monthly income) exceeds Schedule J (monthly expenses), a **surplus warning** appears in the eFiling modal before you submit. This signals that the debtor's income exceeds their reported expenses, which may be relevant to the case outcome. You can review and address the discrepancy or proceed with the filing.
- Filing progress steps appear in the case immediately after submission — you do not need to refresh the page or wait for a background sync. Steps update as each stage of the filing lifecycle completes.
- If a filing fails partway through, the progress panel shows which step failed and the case returns to a retryable state. Retrying the filing starts a new submission attempt and replaces the previous attempt's progress.
- When a filing fails with an error that cannot be retried, a **Contact Support** button appears alongside the error message. Clicking it sends a pre-filled message to your Glade support conversation describing the district, error, and filing attempt. The support chat opens automatically so you can follow up with the Glade team immediately. The button changes to a "Support has been notified" state after the message is sent, and resets if you start a new filing attempt.
- **A document added to the packet as "Other" must be given a name.** When you add a document under the generic **Other** type, the packet needs a filename for it. Leaving that name blank and clicking **Add to packet** shows the validation message on the field straight away. Previously the first click did nothing at all — no error, no document added, no indication of what was wrong — and the message appeared only after you had clicked into the name field and back out, which read as the button being broken.
- Historical filing events are replayed when you navigate to a case, so the progress panel always reflects the full sequence of events even if you weren't viewing the case when they occurred.
- **Inbox notifications**: When a filing event occurs (such as a status update from the court), you receive a notification in the Glade inbox. Clicking the notification takes you directly to the Case Status tab for that case so you can review the current filing status without navigating manually.
- Direct links to a case opened via an inbox notification automatically open the Case Status tab.

### Why a filing is blocked

When a filing cannot be submitted, the eFiling modal explains the specific reason instead of showing a generic error, so your team knows what to address before trying again. Common reasons include missing required case information, missing required documents, a filing district that has not been set up for the case, and permission restrictions. The same explanation appears in the modal's alert and in the accompanying notification.

When the required-fields check reports a problem with the case's data rather than a missing field — an address whose county cannot be identified, for example — the specific problem is named in the pre-filing warnings dialog and in the submission modal, so your team can correct the data. Previously these were reported as the check being temporarily unavailable, which read as a Glade outage and invited retries that could not succeed. See [Required fields check before filing](./pacer.md).

When a filing is blocked because the case's filing district has not been set up, a **Fix this** action appears inline. Completing the district setup from that prompt clears the block, so you can continue the submission without leaving the filing flow.

A filing can also be held up because Glade cannot finish its check of the case's required fields, which shows as the required-fields check being unavailable rather than as a specific item to fix. This is not something your team can resolve on the case — contact support with the case and the county, as it usually means Glade needs to recognize a county spelling. Cases in **McKean County, Pennsylvania** were affected until August 2026 and file normally now.

When a filing is blocked by Glade's pre-filing review, the modal names the specific items that need attention — for example, "Form 122A-1 is not in the filing packet" — so your team can go straight to what is missing. Previously this case showed an unhelpful internal label with no indication of which forms were at fault. If a filing is blocked by more than 20 items at once, the first 20 are listed followed by a count of how many more remain. In the rare case where the review blocks a filing but reports no specifics, the modal asks you to resolve the flagged review items and try again.

### Pre-filing review

Before a petition can be submitted, Glade runs a set of automated checks against the case and reports what needs attention. Each finding is either **blocking** — submission is gated until the item is resolved or an attorney signs off on it — or **advisory**, which flags the issue without gating submission.

Five checks are active:

| Check | What it looks for | Severity |
|-------|-------------------|----------|
| Required documents in the packet | Every document the filing district requires for the case's chapter is present in the packet | Blocking |
| Statement of Intention required | The Statement of Intention (Form 108) is included on a Chapter 7 case that needs one | Blocking |
| Petition out of date | The compiled petition is older than the case data or questionnaire answers behind it | Advisory |
| Required signatures on the petition | Everyone required to sign the petition has signed, everywhere a signature is called for | Advisory |
| Duplicate creditors | The creditor mailing matrix lists the same creditor more than once under slightly different details | Advisory |

- **Required documents come from each district's own rules.** Instead of a list maintained form by form, the check reads the required-document list for the case's filing district and chapter — the same list that drives the filing packet checklist. When a district's required documents change, the review follows automatically.
- **Each missing document is reported as its own item.** A packet missing five required documents produces five blocking items, each naming the document, and each needing its own attorney sign-off. Signing off on one document does not clear the others, and withdrawing sign-off on one document re-gates only that document.
- Documents a district requires **only when they apply** are not reported as missing when they are absent — they have to be valid only if they are provided.
- Documents that apply only to joint filings are required on joint cases and skipped on individual cases. If Glade cannot yet tell whether the case is joint, that document is reported as not evaluated rather than as missing, so an individual filing is never blocked over a joint-only form.
- If the district's required-document list cannot be determined at all, the review reports the check as not evaluated instead of blocking the filing.
- **A check that could not reach a conclusion says so.** When a check depends on case information that is missing, its finding is worded as unresolved and names the check, rather than asserting that the case failed it. Previously an inconclusive result was written in exactly the same language as a genuine failure, so a check that simply had nothing to go on read as a defect in the case — and teams went looking for a problem that was not there. Treat an unresolved finding as "supply the missing information and run the review again", not as something to correct on the petition.
- **Every check needs the case's chapter.** Glade works it out from the case record, falling back to the chapter recorded on the case itself and then to the rest of the case's data. Previously the chapter was read from one place only, so a case where it had not been recorded there — typically a case opened without a case type set — had every check come back as not evaluated for a missing chapter, and the review produced nothing usable. If the chapter genuinely cannot be determined, the checks still report as not evaluated rather than passing.
- **A missing document may now block where it previously only warned.** Because required-document status comes from each district's rules, a document the district marks as required is treated as gating. Pay advices are the common case: in districts whose rules require them, a missing paystubs file now blocks submission rather than showing a warning.
- **The second debtor's pay advices are governed by the district's rules too.** On a joint filing, whether Debtor 2's pay advices are required now comes from the filing district's document list like every other requirement, and appears as its own named item in the pre-filing review. **South Carolina** Chapter 7 and Chapter 13 now carry a Debtor 2 pay advices slot, and **Pennsylvania Western** and **Wyoming** treat theirs as genuinely required rather than optional. Previously this rule sat inside the filing engine instead of the district's document list, and a joint case whose second debtor legitimately had no pay advices — because they are unemployed, retired, or self-employed — failed at submission with an error that nothing in Glade could clear, no matter how many times the packet was reviewed and signed off.
- **"Petition out of date" reflects the petition's own inputs.** It is raised when the case data or the questionnaire answers the petition is built from have changed since it was compiled. Adding a supporting document to the filing packet no longer raises it — the petition is a merge of the selected forms and schedules, so an unrelated PDF added alongside them does not make it out of date. Previously any addition to the packet flagged the petition and prompted a recompile that changed nothing.

#### Who can clear a blocking finding

Signing off on a blocking finding so a filing can proceed is limited to firm owners, firm Admins, and Glade Admins. Other team members working the case see the review and everything it found, and can work through the items, but cannot set a blocker aside to let the filing through. A decision to file over a known problem stays with someone accountable for it.

A **debtor with no pay advices to file** is the case where this matters most in practice. Setting that requirement aside is reserved to Glade — contact support on a joint case whose second debtor has no pay advices, and the item can be cleared so the filing proceeds. Your firm's own attorneys cannot waive it themselves.

#### Required signatures on the petition

The signature check reads the assembled petition that is actually about to be filed and confirms that everyone required to sign it has done so.

- **Who it expects to have signed** — the debtor on every case, the second debtor on a joint case, and the attorney when the debtor is represented. If Glade cannot tell from the case whether the debtor is represented, the check does not assume they are unrepresented.
- **Where it looks** — across the whole filing bundle, not one form. That includes the petition itself, the attorney and fee forms, the declaration about the schedules, the statement of financial affairs, the statement of intention, and the verification of the creditor matrix, plus any other signature block it finds in the document.
- **What counts as a signature** — typed, electronically signed, or handwritten on a printed and scanned page all count. Firms that print, sign in ink, and re-upload are covered the same as firms that sign electronically.
- **What it reports** — **Passed**, **Failed** with the signer who is missing and the form they are missing from, or **Inconclusive** when it cannot read the document or is not confident enough to call it. An explanation in plain English appears next to the other pre-filing findings.
- **It does not gate filing.** The check is advisory for now: it warns and can be set aside, and a Failed or Inconclusive result never blocks submission. Treat it as a second pair of eyes on the packet, not as a guarantee.
- **It re-reads the petition when the petition changes, not on every review.** Because the check reads the assembled document, it runs again after the petition is regenerated, or when someone asks for the review to be run manually. On the automatic refreshes that follow unrelated edits — a change to case data, a questionnaire save — it keeps its most recent verdict, which stays listed with its explanation rather than disappearing or being recalculated against a petition that has not moved. If you have corrected signatures on the source documents and want a fresh verdict, regenerate the petition or run the review manually.

Because it reads the pages rather than checking a stored answer, the check is deliberately cautious — it reports Inconclusive rather than guessing on a court filing. An Inconclusive result means the check could not reach a verdict, not that a signature is missing.

#### Duplicate creditors

This check reads the creditor mailing matrix the case is about to file and flags creditors that look like the same party listed twice. It catches the kinds of near-duplicate that exact matching cannot:

- Typos and abbreviations in a creditor's name.
- The same address written with a nine-digit ZIP on one entry and a five-digit ZIP on another.
- A creditor named two different ways that mean the same company — for example a bank's trading name alongside its full legal name.
- The same creditor listed at two different addresses, raised so someone can decide which address is correct.

**It never merges anything.** The check reports what it found and leaves the decision to the attorney. Dropping a creditor that turns out to be genuinely separate is a notice problem, so no entry is removed from the matrix on the strength of this check.

- It is **advisory** — it does not gate submission, and it can be dismissed like the other advisory findings.
- Creditors that share a mailing address without sharing a name — several creditors using the same lockbox or P.O. box, for example — are not reported as duplicates. That is a normal arrangement, not a mistake.
- The check reads matrices in the layouts different districts use, including the multi-column layout used by North Carolina and Maryland.
- It runs as part of the case's first pre-filing review and on any review you run by hand. Rebuild the matrix and run the review again after correcting the creditor list.

Straightforward duplicates — the same creditor at the same address, differing only in ZIP format, capitalization, or punctuation — are already collapsed when the matrix is built and never reach this check. See [Questionnaires](../workflows/questionnaires.md) for how the matrix is assembled.

Credit counseling recency was held back from the first release and has since been switched on — see [Certificate recency before filing](./abacus-credit-counseling.md) for what it reports. The remaining checks — Social Security number completeness, fee-waiver and installment applications, and prior-discharge advisories — are still turned off and are planned for later releases. The review catches a specific set of problems; it is not a substitute for reviewing the packet.

> TODO: Confirm the exact condition under which the Statement of Intention check applies. It is a conditional requirement tied to the case's secured claims and fee election rather than one that applies to every Chapter 7 filing.

#### Skeleton filings

A skeleton filing submits only the minimum set of documents a district accepts to open a case, with the remaining schedules and forms filed afterwards. The pre-filing review now takes that into account:

- When a case is submitted as a skeleton filing, the required-documents check reads the district's **skeleton packet** requirements instead of its full-packet requirements. A document the district requires only in the complete packet no longer blocks a valid skeleton submission.
- Documents a district requires only when they apply are treated the same way in skeleton mode as in a full filing — absent is not the same as missing.
- The filing packet checklist and the list of expected documents still show the district's full shape either way. Only what the review treats as *required* changes; nothing disappears from the packet view.
- Filings that are not marked as skeleton are unchanged and continue to be checked against the district's complete required-document list.
- Each review records the mode it ran in, so a result can be read back against whether it was checked as a skeleton or a full packet.

Skeleton requirements are defined per district, alongside that district's other filing rules. Kentucky Eastern is now set up for electronic filing, with its required documents pre-selected for skeleton submissions.

> TODO: Confirm where a filing is marked as a skeleton filing — whether it is a choice in the eFiling modal at submission time or a setting on the case.

### Recognized documents uploaded outside the filing modal

Some court documents — for example, documents pulled from PACER — belong in a specific slot of the electronic filing packet. When you add such a document through the case's normal document area instead of from inside the eFiling modal, Glade now recognizes documents whose file name matches a known filing document and automatically places them in the correct packet slot.

- Recognition is based on the document's file name. A document whose name matches a known filing document is slotted automatically; a document with an unrecognized name is added to the case as usual and can be slotted manually.
- Previously, a recognized document uploaded outside the modal was left unslotted and excluded from the filing packet. Now a PACER document dropped into the case this way is included in the Electronic Filing Packet without re-uploading it through the modal.

### PDF flattening in filing packets

Court electronic filing systems (CM/ECF) reject PDFs that contain editable layers such as fillable form fields, annotations, or sticky notes. Client-uploaded documents — cover sheets, local forms, photo IDs, mortgage statements — frequently arrive as non-flat PDFs and would otherwise cause the court to reject the packet.

- When Glade compiles an eFiling packet, every PDF source in the packet is automatically **flattened** before the documents are merged. Form fields, comments, and annotations are baked into the page so the final packet meets CM/ECF requirements without manual intervention.
- Flattening is transparent — your team does not need to enable a setting or pre-process files. Uploads continue to behave the same way as before; the filing packet that goes to the court is what changes.
- If flattening fails on a particular file for any reason, Glade falls back to including the original file in the packet rather than blocking the filing. The filing proceeds and the failure is reported internally for follow-up.
- Glade-generated petition PDFs can also be flattened on output when the workflow that produced them requests it, so signature blocks and form fields render as a static page rather than as fillable form widgets.

### Required documents in the filing packet

Some documents are required by a district's rules and must not be dropped from the petition before filing. When you prepare a petition, any document the district marks as required is pre-checked and **locked** in the document list — it shows a **Required for filing** note and cannot be unchecked or removed, and range-selection skips over it. This prevents a required document from being left out by accident. For example, Florida Middle District Chapter 7 petitions require the Creditor Matrix and the Verification of Creditor Matrix, so both are locked into the packet. Other pre-checked documents that the district does not mark as required stay freely toggleable, so you can include or exclude them as needed.

Which documents a district expects, and whether each is filed inside the petition or as its own file, is configured per district and chapter by Glade. **Eastern District of Kentucky** Chapter 7 cases now include **Form 103A** — the application to pay the filing fee in installments — as its own document in the packet. It appears only when the case elects to pay the fee in installments, and not when a fee waiver is requested instead. Previously the form had no slot in the packet for that district, so filers electing installments could not include it. If your district is missing a form your court requires, contact support to have it configured.

Some districts fold a form into the petition itself rather than expecting it as its own file — North Carolina Eastern Chapter 7, for example, builds Form 122A-1 and Form 2030 into the petition. Those forms have no separate slot in the packet, and Glade no longer reports them as missing documents. A compliant filing in one of these districts is no longer held up over a form that is already inside the petition. A form the district does expect as its own file is still flagged when it is genuinely absent, including a form that is both built into the petition and filed separately.

**Florida Middle District Chapter 13** filings are a correction to this. The Certificate of Credit Counseling and Form 121 (Statement About Your Social Security Numbers) are filed as their own separate documents in this district rather than being folded into the petition. They had been configured the wrong way round, so each now has its own slot in the packet and is expected as a separate file.

### Image uploads in filing packets

Client-uploaded documents sometimes arrive as photos — for example, a phone picture of a signed Certificate of Credit Counseling saved as a JPEG or PNG. Court filing systems reject these when they reach the court as image data under a PDF name.

- When Glade compiles a filing packet, image files (JPEG and PNG) are automatically converted to a single-page PDF before the packet goes to the court, so a photographed document files successfully without your team re-scanning or re-saving it.
- Conversion is transparent — there is no setting to enable, and uploads continue to behave the same way. Only JPEG and PNG images are converted; other file types pass through unchanged.
- If conversion fails for a particular image, Glade falls back to including the original file rather than blocking the filing, and reports the failure internally for follow-up.

## Configuration

> TODO: Document any per-workflow or per-firm eFiling configuration options, such as enabling PACER submissions on a workflow template.

## Edge Cases & Limitations

- If you navigate away from a case mid-filing, the filing continues in the background. When you return, historical events are replayed so the progress panel is up to date.
- Cancelling a filing dismisses the progress panel and shows the filing in a cancelled state. The case can be re-filed if needed.
- The required-fields check depends on Glade recognizing the debtor's county as written on the case. An unrecognized county spelling makes the check unavailable and blocks the filing, and cannot be worked around by re-entering the county — it needs a fix from Glade.
- The Contact Support button is only available for non-retryable errors. Errors that can be retried show the normal retry option instead. If a support conversation is not available for your account, the button does not appear and the error message is displayed as static text.
- The petition signature check needs the compiled petition to be available. If the petition cannot be read, the check reports Inconclusive rather than passing or failing.
- The petition signature check is advisory and cannot currently be dismissed the way the other pre-filing findings can. It reappears on each review until the signatures are in place.
- The duplicate-creditor check needs the case's creditor matrix to have been generated. Where there is no matrix to read, it reports as unresolved rather than passing, and no creditors are examined.
- The duplicate-creditor check reports judgment calls for a person to settle. It does not correct the creditor list, and a finding it raises is not by itself evidence that two creditors are the same party.

## Related Features

- [Workflows](../workflows/automation-rules.md) — workflows can include eFiling steps as part of an automated case sequence.
- [Status Tracking](../workflows/status-tracking.md) — the Case Status tab where eFiling notifications deep-link.

