# PACER Integration

## Overview

Glade integrates with PACER (Public Access to Court Electronic Records) to automate bankruptcy case filing in federal courts. Firms connect their PACER credentials, and Glade handles the end-to-end filing process — uploading documents, navigating court-specific forms, paying filing fees, and reporting the assigned case number back to the firm. The filing runs asynchronously and typically completes in 7–10 minutes.

## Key Behaviors

### Connecting PACER credentials

- Firms provide their PACER account email and two-factor authentication key from the PACER integration settings.
- Credentials are stored encrypted and linked to the firm's account.
- PACER session tokens are cached to avoid repeated logins across filings.

### PACER notice address

Each firm is given its own dedicated address for receiving PACER court notices when the firm is created. Glade routes incoming court notices through this address to the firm's case activity timeline automatically — no extra setup is needed. The address is provisioned at the time the firm is set up; firms that existed before this was automatic have had their addresses backfilled.

### Supported courts

Glade currently supports automated filing in the following bankruptcy courts:

- Alabama Northern (ALNB) — Chapter 7 (individual filings only; joint petitions are not yet supported)
- Florida Middle (FLMB)
- Florida Northern (FLNB)
- Florida Southern (FLSB)
- Idaho (IDB)
- Kentucky Western (KYWB) — Chapter 7
- Louisiana Eastern (LAEB) — Chapter 7
- Maryland (MDB) — Chapter 7
- South Carolina (SCB)
- Virginia Eastern (VAEB) — Chapter 7
- Washington Eastern (WAEB) — Chapter 7
- Washington Western (WAWB) — Chapter 7 and Chapter 13

Districts that list a chapter (for example, Kentucky Western — Chapter 7) only support filings of the listed chapter. Districts without a chapter qualifier support all chapters Glade files (Chapter 7 and Chapter 13). Courts not in this list are not available for automated filing.

### Filing workflow

1. An attorney initiates a filing from the case's eFiling modal, confirming the documents and court district.
2. Glade validates the filing packet — checks that required documents (petition, creditor matrix, pay advices, counseling certificates) are present and the chapter type is compatible.
3. A submission attempt is created with status "in progress."
4. The filing runs asynchronously via browser automation:
   - Logs into PACER with the firm's credentials and 2FA.
   - Uploads core case documents (debtor info, attorney information, petition, creditor matrix, pay advices).
   - Uploads supplemental documents based on chapter type — Chapter 7: income statements, means test; Chapter 13: repayment plan, income statements. For Chapter 7 business-debt cases claiming an exemption from the means test presumption of abuse, the **Statement of Debtor's Temporary Exclusion from Presumption of Abuse (B122A-1Supp)** is available as a document type in the ECF document filename dropdown and is uploaded as part of the supplemental documents.
   - Submits credit counseling certificates and compensation disclosures.
   - Extracts the assigned case number from the court's confirmation screen.
   - Pays the filing fee via the firm's credit card on file with PACER.
5. On success, Glade records the case number and notifies the attorney via email and inbox notification with a link to the case.
6. On failure, the attorney receives a failure notification with error details and can retry from the case view.

### Filing packet document types

Each document in the filing packet must be labeled with the correct ECF document type. The document type dropdown in the filing packet lists named options for all commonly filed documents. Selecting the correct type ensures courts can identify each file — courts including FLMB and FLSB reject filings that contain unrecognized filenames.

- For **Chapter 7 business-debt cases** where the debtor is claiming exemption from the means test presumption of abuse, upload the B122A-1 Supplement and select **Statement of Debtor's Temporary Exclusion from Presumption of Abuse (B122A-1Supp)** from the document type dropdown. This is supported for all available districts. Filing this document labeled as "Other" causes a submission failure.
- When a court requires individual debtor identification documents, select **PhotoID (Debtor 1)** or **PhotoID (Debtor 2)** for each debtor's photo identification, and **DeBN (Debtor 1)** or **DeBN (Debtor 2)** for each debtor's Declaration of Electronic Notice. The Debtor 1 variant is for the primary debtor; the Debtor 2 variant is for the co-debtor in a joint case.
- For **Western District of Pennsylvania (PAWB)** Chapter 7 cases, **Local Form 1 — Declaration Re: Electronic Filing of Petition, Schedules & Statements** is available in the document type dropdown. This form is submitted through the EDSS portal alongside the SSN Statement — it is not part of the standard ECF filing packet. A Local Form 1 slot appears in the per-district document checklist for PAWB Chapter 7 workflows once the document is labeled and uploaded.
- For **Florida Southern (FLSB)** Chapter 13 cases, **Local Form 67 — Certification of Compliance** is available in the document type dropdown. The form auto-surfaces in the FLSB Chapter 13 required-document checklist, and ad-hoc uploads from the case documents picker are accepted under common filename variants (with or without spaces, hyphens, underscores, or the full form name).
- For **Maryland (MDB)** Chapter 7 cases, **Form 108 — Statement of Intention** is filed as a separate case-open document rather than folded into the consolidated petition. It has its own **Statement of Intent** slot in the district's document checklist, and common filename variants for the form are recognized automatically so the upload lands in that slot instead of falling back to **Other**.
- Additional district-specific document types are available in the dropdown so attorneys filing in these courts can label uploads correctly instead of falling back to **Other**:
  - **Ohio Southern (OHSB)** Chapter 7 — **Statement of Intent** (Statement of Intention for individuals filing under Chapter 7) and **Verification of Creditor Matrix** (OHSB filename variant) are selectable from the document type dropdown.
  - **Washington Eastern (WAEB)** Chapter 7 — **Declaration Regarding Payments (LBR 1007-1)** is selectable from the document type dropdown.
  - **New Mexico (NMB)** Chapter 7 — **Marital Status** is selectable from the document type dropdown.
  - **Louisiana Eastern (LAEB)** Chapter 7 — **Tax Returns** is selectable from the document type dropdown.
  - **Pennsylvania Western (PAWB)** Chapter 7 — `lf29.pdf` (the PAWB filename for the Verification of Creditor Matrix) is now accepted on upload in addition to the canonical name.
  - **Means Exemption (Form 122A-1Supp)** is also recognized end-to-end across the catalog, validator, and runtime allowlist, so uploads that select this option no longer fail filename validation on the way to PACER.
- For **Ohio Southern (OHSB)** Chapter 7 joint-debtor filings, **Statement 1015-2 — Joint Debtor Compliance (OHSB)** is available in the document type dropdown for the Joint Debtor Compliance Statement form (Statement 1015-2 with No Prior). Label the uploaded form with this document type so it is recognized at filing time — uploading it as **Other** prevents the OHSB filing engine from picking it up.
- For **Washington Eastern (WAEB)** Chapter 7 cases, three additional installment-and-fee-related document slots are now available in the case's document checklist when the corresponding files are attached: **Form 103A — Application for Individual to Pay Filing Fee in Installments**, **Form 103B — Application to Have the Filing Fee Waived**, and **LBR 1007-1 — Declaration Regarding Payments**. Slots only render when a file is attached, so cases that pay the filing fee in a single transaction continue to show only the standard checklist. Common filename variants for the LBR 1007-1 declaration (with or without spaces, hyphens, or the full form name) are accepted on upload.
- Glade also accepts non-canonical filename variants for **Verification of Creditor Matrix** uploads, so files named with run-together or otherwise normalized variants pass the filing packet's filename check instead of being rejected.
- Use a named document type whenever one exists in the dropdown. The generic "Other" option is for documents that do not match any named type.
- When you save documents to the filing packet and the save does not go through, the document selection window stays open and shows the specific reason it failed (for example, the exact validation message), so you can correct the problem and try again. Previously the window could close on a failed save without anything being saved, and only a generic error was shown.
- When you assign a custom filename to a document being added to PACER, Glade now preserves spaces, hyphens, parentheses, periods, plus signs, apostrophes, and accented letters in the filename. Filenames such as `Pay Advices`, `Tax Return 2024`, and `Photo ID (Debtor 1)` flow through to PACER as typed instead of being collapsed into a single run-on word. Only characters that filesystems or PACER cannot accept (such as path separators and control characters) are removed.
- Filenames that contain only special characters and would resolve to an empty name are rejected at the form before they can be saved, so you see the validation message immediately rather than encountering a runtime error during filing.
- **A document type the district does not accept is refused, not quietly dropped.** When you label a document by hand and the filing district's rules do not accept that type for the case, the save fails with an error explaining the problem. Previously the save appeared to succeed while the label was silently cleared, so the document went back to being unlabelled — and the packet was a file short at filing time with nothing on screen to say why. Check any document you labelled and later found unlabelled again; it was most likely refused by the district's rules rather than lost.
- The district check recognises every way a district can accept a document — as its own upload, folded into the case-open bundle, combined with other files, or excluded from the packet under a specific filename. A document type a district genuinely accepts is no longer refused because it happens to be accepted in one of the less common ways.
- Automatic labelling is unchanged. When Glade cannot match a document to a district's slot on its own, it still leaves the document unlabelled rather than guessing at a type, so nothing is filed under a label nobody chose.

### Filing Packet AI Review

Filing Packet AI Review is currently turned off. Filing packet uploads no longer trigger an automated AI review, the document review status panel and review badges have been removed from the PACER preview pane, and the Filing Packet AI Review configuration page is no longer in use. The feature is paused while the review experience is reworked.

### Chapter 13 plan status in the filing packet

For Chapter 13 cases in districts where Glade generates the Chapter 13 repayment plan, the filing packet preview shows the status of the plan document so you can confirm it is current before filing. The plan is reviewed in the packet preview because it is filed as a separate document, not folded into the consolidated petition.

- **Outdated plan** — When the plan attached to the packet was generated from a plan version that is no longer the current published one, the plan row shows an **Outdated** tag. Regenerate the plan so the filed copy reflects the latest figures.
- **Missing plan** — When the plan row is missing and the district supports plan generation with a published plan available, the row shows a **Generate it from the plan calculator** hint pointing you to the [Chapter 13 Plan Calculator](../workflows/questionnaires.md). Plan generation happens in the calculator; the packet preview only reports the status.

This status appears only for Chapter 13 packets in plan-generation districts. Other packets make no plan-status check.

### Filing fees

- PACER charges a filing fee per case, determined by court and chapter type.
- Glade submits payment through PACER's credit card interface during the filing process.
- Payment is retried up to 3 times if the initial attempt fails.
- The transaction number from PACER is recorded on the submission.

### Attorney compensation disclosure (Form 2030)

The attorney compensation amount disclosed on Form 2030 is read from the case questionnaire and carried into the filing.

- Glade reads the amount from whichever compensation question the case's Form 2030 actually uses. Firms are on several versions of the form, and the answer may be a currency amount, typed text (including a formatted figure such as `1,600.00`), or a choice from a list — all of these are read correctly. Previously Glade looked for the answer on a retired version of the form only, so the amount reached the court blank on every filing.
- A fee of **$0** — pro bono representation — is carried through as zero rather than treated as unanswered.
- If the question has not been answered, or the answer is not a readable amount, the compensation figure is left unset. In districts that require it, this blocks the filing until the question is answered on the questionnaire.

### Filing progress panel

A filing progress panel appears in the bottom-right corner of the screen when a PACER filing is running. It persists as you navigate to other pages — you do not need to stay on the filing tab to monitor progress.

- The panel is collapsed by default. The header shows the current step label, a progress count (e.g., "Uploading documents (3/6)"), and a spinner while the filing is in progress.
- Click the header to expand the panel and see the full step list, a **View filing** link that opens the case's status tab, and a dismiss button.
- When the filing completes, the header shows a green check and "Filing completed." When it fails, a red indicator and "Filing failed" appear.
- If you cancel a filing in progress, the header shows "Cancellation pending" until the cancellation is confirmed.
- Dismissing the panel hides it from view. The case's status tab continues to show full filing history.
- **Three failure reasons that used to show no detail now explain themselves.** A filing that stopped because the PACER login did not finish loading, because a required file was missing from the packet, or because the court site landed on a page Glade did not expect used to leave the progress detail empty and show only a generic "Case sync failed" message on the dashboard. Each of these now reports its own explanation, so your team can tell a court-site problem worth retrying from a packet problem it has to fix first. Other failure reasons were already explained and are unchanged.

### Status tracking

- Submission status values: in progress, succeeded, failed, or manual (attorney filed outside Glade).
- Each step of the filing process is logged with timestamps.
- Screenshots are captured at key steps for debugging failed submissions.
- Inbox notifications link directly to the case's status tab.
- The assigned PACER case number is shown in the workflow header. Clicking the case number copies it to your clipboard, making it easy to paste into other tools or communications.
- For a case your firm filed outside Glade and then recorded in Glade, the **Filed at** date on the PACER case number panel is the court's actual filing date, which is usually earlier than the day someone entered the case. Your own team can now read that date back after entering it — it stays visible on the panel when you reload the case or come back to it another day. Previously only Glade staff could read the value, so the panel showed the date as unset to the firm even though it had been saved, and an attorney could re-enter the same date repeatedly without it ever appearing. Each firm sees only its own cases.

### PACER login failures

When a filing fails because Glade could not log in to PACER, the case status dashboard reports **"PACER login failed."** without advising you to check your credentials.

Login failures are frequently not a credential problem — a two-factor prompt that timed out while waiting is the most common cause — so the message no longer points your team at credentials that are usually correct. Where a more specific reason is available, it appears in the case's filing log. Retry the filing first; only re-enter your PACER details if the failures continue.

### Filing deficiencies

Sometimes a case is accepted by the court but one or more required documents are rejected and must be re-filed by hand in PACER — a "filed with deficiency" outcome. Glade surfaces this state persistently across the case so it is not missed after the live filing view is closed.

- An **action-required banner** appears on the case listing the specific forms that still need to be filed manually in PACER. The banner stays visible until the deficiency is addressed, rather than appearing only while the submission is running.
- On the Case Status tab, the filing card shows a **Filed with deficiency** heading and a **View Submission** button that opens the submission details, so you can see exactly which documents were rejected.
- The status updates live — if a filing's status changes while you are viewing the case, the banner and the status card refresh without a manual reload.
- **One task per rejected document.** Glade creates a separate cure task for each document the court rejected, each titled after its own document, rather than a single task covering all of them. Your team can divide the work and see at a glance how many documents are still outstanding. See [Status Tracking](../workflows/status-tracking.md) for how these tasks are assigned.
- **Completing a task clears that document.** After you file a rejected document by hand in PACER, mark its task complete and that document is cleared from the case's deficiency. The action-required banner narrows to the documents that remain and disappears once the last one is cleared. Previously the banner stayed up even after every document had been re-filed, and clearing it required contacting Glade.

> TODO: Confirm in production that completing a cure task clears the document from the banner. The court-integration side of this behavior was still pending when the change shipped, and a failure there is reported internally rather than shown to the user — so a banner that still lists an already-filed document should be raised with Glade.

### Recording a case filed outside Glade

When a case is filed directly in PACER instead of through Glade, your team can register it against the workflow from the dashboard's case-status widget, so Glade tracks it alongside cases it filed itself.

- Enter the court-assigned case number to register the case. The registration is attributed to your firm, so the case appears in your firm's case-status views and reports next to cases filed through Glade. Previously a manually registered case was not attributed to the firm and could be missing from those reports.
- **Filed at date** — an optional date field records the date the court actually accepted the filing, which is often earlier than the day someone entered the case into Glade. After you save it, the date is shown read-only next to the case number.

### 341 meeting notices

Glade processes incoming court notices about 341 meetings (meetings of creditors) and displays the name of the trustee who will conduct the meeting.

- When a 341 meeting notice identifies the conducting trustee by name — for example, via a video or phone conference format — Glade shows that person as the trustee for the meeting.
- The conducting trustee may differ from the case trustee listed elsewhere in the notice. Glade prioritizes the person actually conducting the meeting, not other named parties such as case-party trustees.

### Notices scheduling several hearings at once

Some courts set more than one hearing in a single notice — a confirmation hearing on one date and a 341 meeting on another, in the same docket entry. Glade records **each** hearing separately, matching every date to the hearing type named beside it.

- Previously only one hearing per notice was captured, and the date and the hearing type could come from different hearings — so a notice could produce a single entry showing a 341 meeting label against the confirmation hearing's date, with the other hearing missing altogether.
- When a notice is processed again — after a rescheduling notice, for example — Glade reconciles the hearings it already recorded against the notice: missing hearings are added and entries that no longer match are removed, so an earlier mismatched entry is corrected rather than duplicated.
- Each recorded hearing flows through to the rest of Glade independently: it appears on the case, and (where court hearing sync is enabled) creates its own calendar event. See [Calendar Sync](../appointments/calendar-sync.md).

Notices processed before this correction are not revisited automatically. If your firm files in a district that routinely issues combined notices, ask Glade to reprocess your court notices for the affected date range.

### Proof of claim documents and the claims register

Glade captures the proofs of claim creditors file against your case and organizes them into a claims register at the case level, so your team can review what has been claimed without opening each court notice one at a time.

- **The claim PDF is captured.** Proof of claim notices link their document from the notice's claim number rather than a document number. Glade now recognizes both, so the claim PDF is stored with the case and appears in the Court Notices document column. Previously that column was empty for proof of claim notices and the document had to be retrieved from PACER by hand.
- **Claims are listed per case.** The claims register shows every claim filed against the case, with a summary across all claims and a detail view for each one, instead of requiring the picture to be reassembled from individual notices.
- **Claim details are extracted.** For each claim, Glade reads the creditor's name and address and the claimed amounts — total, secured, priority, and unsecured.
- **Each claim shows its current state and its history.** Glade tracks where a claim stands now separately from the record of events on that claim, so later activity updates the claim without erasing what came before. Notices that arrive out of order do not leave the current state wrong.
- **Certificates of Service are recognized from the notice subject**, so a notice that says what it is is classified without waiting on document analysis.
- **A notice that arrives before its case is identified is not lost.** When a court notice cannot be matched to a case at the time it arrives and is associated with the workflow later, Glade extracts the claim information at that point.
- Claims are visible only to the firm that owns the case.

### South Carolina (SCB) Chapter 7 filings

- Chapter 7 cases filed in the South Carolina Bankruptcy Court need a completed Debtor's Election Re: Electronic Noticing (DeBN) form for each filer. Glade reads the election directly from the uploaded DeBN PDF — there is no separate questionnaire question to answer. Upload the signed DeBN form to the document slot during document collection and Glade extracts the elected action automatically.
- For an individual case, upload the debtor 1 DeBN form. For a joint case, upload a DeBN form for each debtor — both the debtor 1 and debtor 2 elections are read and sent to PACER.
- The supported actions read from the form are **Activate**, **Deactivate**, **Update**, or **Decline**. The extracted answer is passed through to PACER so the SCB filing engine fills the matching radio on the local form.
- Auto-extraction runs on both individual and joint SCB Chapter 7 filings. Non-Chapter 7 filings do not require the DeBN extraction.
- If a required DeBN form has not been uploaded by the time a qualifying SCB Chapter 7 case is submitted, the filing is blocked with an error naming the missing election so your team can add the document before retrying. On a joint case, the election is required for both debtors — a missing form for either filer blocks the filing.
- If an uploaded DeBN form cannot be parsed — for example, no radio button is selected on the form — the filing modal shows an inline **election picker** so you can recover without leaving the filing. Pick the election the debtor signed (**Activate**, **Deactivate**, **Update**, or **Decline**) and submit again; Glade saves the choice to the case and retries the filing. On a joint case, a picker appears for each debtor whose election could not be read. Re-uploading a clean copy of the form is still an option if you prefer to fix the source document.
- Re-uploading a newer DeBN form supersedes the previously extracted answer. The most recent extraction wins, so correcting an earlier upload mistake is a matter of replacing the file in the document slot.

### Chapter 7 individual presumption-of-abuse page

When a Chapter 7 individual case explicitly indicates "no presumption" on B122A-1 line 14, Glade now fills the matching presumption fields on B122A-1 lines 40 and 42 with that same answer instead of leaving them blank. Because the lines are populated, PACER no longer renders the standalone "Presumption of Abuse" page during filing — the filing proceeds without that extra interstitial. Other income and expense fields wiped by the no-presumption answer continue to be cleared as before. The override applies only to Chapter 7 filings; cases on other chapters that carry stale prior answers from an earlier Chapter 7 session are not affected.

### Case transfers

When a bankruptcy case is transferred to a different court and assigned a new case number, PACER sends electronic notices to the new case number. Glade automatically associates those incoming notices with the original workflow, so your case activity timeline stays complete without manual re-linking. The association is based on the transfer notice in the PACER email, which identifies the originating case number.

### Case number matching across formats

Courts write the same case number in several different formats — for example `26-18233`, `26-bk-18233`, and `0:26-bk-18233` — and some districts add the assigned judge's initials on the end (for example `8:25-bk-08186-RCT`). Glade treats all of these as the same case number when it links court notices and when you search, so a difference in format no longer prevents a match.

- **Incoming court notices** link to the right case even when the notice writes the case number in a different format than the one stored on the workflow. Previously an exact-text mismatch could leave a notice unlinked, so notices for a case could pile up without ever attaching to its activity timeline.
- **Dashboard case-number search** matches a workflow regardless of which format you type. Searching for `26-18233` finds a case stored as `26-bk-18233` or `0:26-bk-18233`, and the reverse also works.

Notices that were already stranded by an earlier format mismatch are not re-linked on their own. If a case is missing court notices you expected to see, contact Glade to re-sync it.

### Case numbers when a case has more than one workflow

A single matter often carries several workflows — a retainer alongside a filing workflow, or a new workflow created when a case converts from one chapter to another. The court case number is recorded on the workflow the case was actually filed under, not on all of them.

- Every workflow in the group now **displays** the case number, taking it from whichever sibling holds one. Opening the retainer on a filed case shows the docket number instead of a blank field. Where more than one sibling carries a number, the most recently created one is shown.
- The case number is displayed, not copied. It still belongs to the workflow the case was filed under, which is what keeps incoming court notices attached to the right workflow.
- **Reports and filters that match on case number are unchanged.** They match the workflow that actually carries the number, so a report segmenting cases by whether a case number is present continues to count each matter once rather than once per workflow in the group.

### Claim notices with more than one document

Proof-of-claim notices from PACER can carry several documents — the claim form plus its attachments. All of them are captured.

- Every document on the notice is saved, and each keeps the part number the court assigned it, so a multi-part claim can be read in the order the court filed it.
- Claim documents are named from the creditor, claim number, case number, and part, so they are identifiable in the case's document list without opening each one.
- An amended claim number on the notice is recorded as the claim number. Previously an amended value that Glade could not read fell back to the case number, which made the document harder to identify.
- **Capture status and the reason for any failure are shown.** If one document on a claim cannot be retrieved, the rest are still captured and the notice reports what failed rather than appearing complete.
- A retry picks up only the documents that are still missing; documents already captured are not fetched again.
- Anything the court returns that is not a readable PDF — a sign-in page or an error page, for example — is rejected rather than saved as if it were the document. Previously these could be stored as PDFs that would not open.
- **Attaching a claim PDF by hand is supported.** When a document cannot be captured automatically, uploading it to the case keeps its connection to the PACER claim it belongs to, so it is found by the same case and claim reference as automatically captured documents rather than sitting as an unrelated file.

Claims captured before this behavior shipped are not re-processed. If an older claim is missing attachments, capture them again or attach them by hand.

### Changing the chapter at petition compile time

When a case switches between Chapter 7 and Chapter 13 mid-workflow, the petition must be re-compiled against the new chapter so the schedules and forms match. The pre-compile modal (Documents → **Compile Petition**) makes this switch visible at the moment of filing.

- If the case's district supports more than one chapter, a **Chapter** selector appears in the compile modal next to the filing district banner. Picking a different chapter updates the case data immediately, so the next compile run uses the new chapter.
- After changing the chapter, a **"Chapter changed. Recompile to refresh the petition."** note reminds you to click **Compile** so the regenerated petition reflects the new chapter. The note clears as soon as the new petition finishes compiling.
- If the district only supports a single chapter, or the case is already filed, the selector is read-only and shows the current chapter as a chip — you can see the chapter at a glance but cannot change it.

### Required fields check before filing

Before a filing can be submitted, Glade validates that all required debtor fields are present. If any are missing, the filing is blocked at both the pre-filing preview and the ECF submission modal, and the missing fields are listed by name so your team can address them before re-attempting.

- The **credit counseling completion date** is no longer part of this check. A Chapter 7 or Chapter 13 filing is no longer stopped because that date is absent from the case questionnaire — firms whose Schedules questionnaire does not ask for it can file with the certificate itself as the record of completion, for individual and joint cases alike. Whether the briefing is recent enough to satisfy § 109(h) is assessed by the pre-filing review instead of by this check, so a stale certificate is raised for an attorney to review rather than blocking the filing outright with no explanation.
- For individual Chapter 7 filings, the **marital filing status** is required. Submission is blocked if the answer is missing from the questionnaire, and the missing field is named in the eFiling error so the team can fill it before retrying. For joint Chapter 7 filings, when the questionnaire indicates the petition is filed jointly but the marital filing status answer was not provided, Glade infers "Married, filing jointly" automatically — joint Chapter 7 filings no longer fail because of an unanswered marital status question.
- Glade checks these fields in the questionnaire data — if the information has been collected but not yet saved, save the questionnaire before initiating the filing.
- Whether the case is joint or individual is read from the **Schedules** questionnaire only, not from custom client-intake forms or earlier questionnaires that may carry stale answers. Cases that were initially entered as joint and later corrected to individual (or vice versa) on the Schedules questionnaire reflect the corrected value at filing time.
  - Checks that only apply to a second debtor use the same answer. On an individual filing where nothing else on the case indicates whether it is joint or individual, those checks no longer report an unresolved second-debtor result — an individual Chapter 7 stops showing a "(Debtor 2)" line for things like a co-debtor's briefing or Social Security number.
- Missing fields are shown with labels — for example, "Marital filing status" — so you can identify exactly what needs to be filled in. An **Open questionnaire** link in the error state takes you directly to the case questionnaire.
- If a filing attempt fails because required fields are still missing at the point of submission, the eFiling modal names the specific missing fields so your team knows exactly what to complete before retrying.
- **When the check itself reports a problem with the data, that problem is shown.** Some failures are not about a blank field but about a value the check cannot work with — an address whose county cannot be identified, for example. Those now appear as the specific problem to fix, in both the pre-filing warnings dialog and the submission modal. Previously any failure of this kind read as "Required-Fields Check Unavailable — retry shortly", which looked like a Glade outage and left teams retrying a filing that would never succeed until the underlying data was corrected. A genuine outage still reports as unavailable, so the two are now distinguishable.

### Required documents check before filing

Alongside the required fields check, Glade checks the filing packet against the document slots the case's district actually requires, and reports anything missing before submission.

- **Findings name the document they are about.** Each missing required document is reported using the district's own label for that slot — "Payment Advices", for example — so a packet missing several documents produces one clearly-titled finding per document. Previously every one of those findings carried the same generic title, so a case missing three documents showed three identical rows and you had to open each to learn what it meant.
- **Four fee and means-test forms are now hard-required when the case calls for them**, and a missing one blocks like any other required document:
  - **Form 103A** (application to pay the filing fee in installments) and **Form 103B** (application for a fee waiver) — required when the debtor has elected that fee treatment.
  - **Form 122A-2** (Chapter 7 means test calculation) and **Form 122C-2** (Chapter 13 calculation) — required for above-median cases.
  These four were previously checked only if they had already been uploaded; their absence produced no finding at all. A Chapter 7 case where the debtor elected fee installments could reach filing with no Form 103A while the review reported "All required documents attached". If your team relied on that message alone, re-check any case filed before this change that involved a fee installment election, a fee waiver, or an above-median means test.
- Each of the four is demanded only when the case's own answers call for it. Form 103A is not required on a Chapter 7 filing where the debtor paid the fee outright.

### Credit counseling checks before filing

- Recency findings state the **date the briefing was completed** and the **date the certificate remains valid through**, rather than only reporting pass or fail. This makes it possible to see how much time is left on a certificate, and to audit afterwards which date the check was actually assessing.
- Findings also record **which date was used** — the date printed on the certificate, or the date the certificate reached Glade. The two can be months apart when a briefing was completed with a provider outside Glade and the certificate attached later.
- **The credit counseling certificate's own row in the packet is flagged when a check about it fails.** Previously only the petition document could show a "Needs attention" marker, so a blocking credit counseling finding left the certificate row looking fine and the problem had to be found in the review results.

### Preventing duplicate filings

Before a filing proceeds, Glade checks whether the case already has an assigned case number or an in-progress filing. Depending on the situation, you will see one of two states in the pre-filing dialog:

- **Hard block** — If a case number already exists, or if a filing is actively in progress for the case, the dialog shows only a **Go Back** button. You cannot proceed until the existing filing resolves. A red alert banner in the eFiling modal also shows the blocking reason.
- **Soft warning** — If a recent filing attempt exists but does not meet the hard-block conditions, you can review the details and continue by checking an acknowledgment checkbox and clicking **Continue Anyway**.

At the moment you click the final submit button, Glade performs a fresh check. If the status has changed to a hard-block condition while the dialog was open, the submission is blocked and you will see a toast and an updated alert banner.

### Compiling selected documents for amendments

When filing an amendment, you can select a subset of the case's documents and download them as a single merged PDF — without downloading all documents or individual files.

1. Open the Case Documents pane (press **D** while viewing the case).
2. Check the boxes next to the documents you want to include. You can select across multiple document categories.
3. The footer button changes to **Download N selected as PDF**, where N is your selection count.
4. Click it to open the compile modal. Enter a custom filename and drag to reorder documents if needed.
5. Click **Compile and Download PDF** to download the merged file.

Deselecting all documents returns the footer to the standard download options. Your selection clears automatically when you close the documents pane.

### Notifications

| Event | Email | Inbox |
|-------|-------|-------|
| Filing succeeded | Case number and client name | Link to case status tab |
| Filing failed | Error summary | Link to case for retry |

## Configuration

| Setting | Description |
|---------|-------------|
| PACER credentials | Email and 2FA key, entered in integration settings |
| Court district | Selected per filing from the case's eFiling modal |
| Test environment | Submissions can be routed to PACER's test system for QA |

## Edge Cases & Limitations

- Only bankruptcy cases (Chapters 7 and 13) are supported. Other case types (civil, criminal, appellate) are not available.
- Filing requires a complete document packet — missing required documents cause the submission to fail.
- The required documents check reports on the separate documents in the filing packet. Forms that are folded into the consolidated petition rather than filed as their own document are not reported individually.
- Courts outside the supported list cannot be filed to through Glade.
- Filing is asynchronous and takes 7–10 minutes. The attorney does not need to keep the page open.
- If the PACER session token expires mid-filing, the submission fails and can be retried.
- PACER passwords are not stored — they are passed only at filing time. The 2FA key is stored encrypted.
- If a filing partially succeeds (some documents uploaded but fee payment fails), the submission is marked as failed. The attorney may need to complete the filing manually in PACER.
- Once a case number is assigned, Glade hard-blocks any further automated filing attempts for that case. To file again (e.g., for an amended petition), contact support or file directly in PACER.
- Reconnecting after a credential change requires re-entering the 2FA key.
- The claims register covers proofs of claim received from the point the feature became available. Claims filed against a case before then are not added to the register on their own — contact Glade if a case needs its earlier claims brought in.

## Related Features

- [Electronic Court Filing (eFiling)](./efiling.md)
- [Workflows](../workflows/automation-rules.md)
- [USCIS Integration](./uscis.md)
