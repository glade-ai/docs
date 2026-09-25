# Proofs of Claim and the Claims Register

## Overview

Glade captures the proofs of claim creditors file against your case and organizes them into a claims register at the case level, so your team can review what has been claimed without opening each court notice one at a time.

## Key Behaviors

### Proof of claim documents and the claims register

- **The claim PDF is captured.** Proof of claim notices link their document from the notice's claim number rather than a document number. Glade now recognizes both, so the claim PDF is stored with the case and appears in the Court Notices document column. Previously that column was empty for proof of claim notices and the document had to be retrieved from PACER by hand.
- **Claims are listed per case.** The claims register shows every claim filed against the case, with a summary across all claims and a detail view for each one, instead of requiring the picture to be reassembled from individual notices.
- **Claim details are extracted.** For each claim, Glade reads the creditor's name and address and the claimed amounts — total, secured, priority, and unsecured.
- **Each claim shows its current state and its history.** Glade tracks where a claim stands now separately from the record of events on that claim, so later activity updates the claim without erasing what came before. Notices that arrive out of order do not leave the current state wrong.
- **Certificates of Service are recognized from the notice subject**, so a notice that says what it is is classified without waiting on document analysis.
- **A notice that arrives before its case is identified is not lost.** When a court notice cannot be matched to a case at the time it arrives and is associated with the workflow later, Glade extracts the claim information at that point.
- Claims are visible only to the firm that owns the case.

### Claim notices with more than one document

Proof-of-claim notices from PACER can carry several documents — the claim form plus its attachments. All of them are captured.

- Every document on the notice is saved, and each keeps the part number the court assigned it, so a multi-part claim can be read in the order the court filed it.
- Claim documents are named from the creditor, claim number, case number, and part, so they are identifiable in the case's document list without opening each one.
- An amended claim number on the notice is recorded as the claim number. Previously an amended value that Glade could not read fell back to the case number, which made the document harder to identify.
- **Capture status and the reason for any failure are shown.** If one document on a claim cannot be retrieved, the rest are still captured and the notice reports what failed rather than appearing complete.
- A retry picks up only the documents that are still missing; documents already captured are not fetched again.
- Anything the court returns that is not a readable PDF — a sign-in page or an error page, for example — is rejected rather than saved as if it were the document. Previously these could be stored as PDFs that would not open.
- **Attaching a claim PDF by hand is supported.** When a document cannot be captured automatically, uploading it to the case keeps its connection to the PACER claim it belongs to, so it is found by the same case and claim reference as automatically captured documents rather than sitting as an unrelated file.

## Edge Cases & Limitations

- The claims register covers proofs of claim received from the point the feature became available. Claims filed against a case before then are not added to the register on their own — contact Glade if a case needs its earlier claims brought in.
- Claims captured before the multi-document behavior shipped are not re-processed. If an older claim is missing attachments, capture them again or attach them by hand.

## Related Features

- [Court Notices](./README.md)
- [Case number matching](./case-number-matching.md)
