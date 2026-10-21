# Packet Checks

## Overview

Several pre-filing review checks look at the documents in the filing packet themselves: whether each maps to a slot the district accepts, whether the district will take it electronically for this case, whether the packet is put together correctly, and whether the compiled petition contains Form 121. These catch defects that used to surface only as a failed submission or a rejection after filing.

## Key Behaviors

### Documents the district cannot place

Every document in the filing packet has to map to a slot the district's filing system accepts. Where one does not, the review reports it as a blocking item naming the document, so your team can replace or remove it before submitting.

- Previously this failed at submission with an internal error and no indication of which file was at fault, so there was nothing to act on and nothing to retry that would behave differently.
- **Each unplaceable document is its own item**, so a packet with three of them names all three rather than stopping at the first.
- The same file listed twice produces one item, not two.
- If Glade cannot work out whether the packet's documents can be placed at all, the check reports as unresolved rather than passing.
- **District of Puerto Rico cases are covered.** Since Puerto Rico was brought online as a filing district, this check could not recognize it and reported as unresolved on every case filed there — so an unplaceable document was never named before submission and instead failed at the court. Puerto Rico cases are now checked like any other district. If a Puerto Rico filing failed at the court with nothing in the review to explain it, run the review again; a packet problem will now be named.

### A document the district will not accept electronically

Separate from whether a document can be *placed* on a filing slot, a district decides which documents it will take electronically at all — and that answer depends on the case as well as the district. A district may not accept a particular form electronically in any circumstances, or may accept it only for a case of a certain shape.

- Each tagged document in the packet that the district will not accept for this case raises its own advisory finding naming that document, so a packet with several names all of them.
- **This is what a firm previously learned from a rejection after filing.** A document the court's system would not take came back as a post-submission rejection with nothing on the case to point at; the finding moves that to before you submit.
- **It is advisory, so the review will let you file past it** — but the court's system will not. Filing over one of these findings means the submission fails at the court rather than at the review. Treat it as a rejection you have been shown early, not as an optional warning.
- Only documents actually in the packet are checked. An expected slot with nothing in it raises nothing here.
- Where Glade cannot determine whether the district accepts a document, no finding is raised for it.

This is a different check from [Documents the district cannot place](#documents-the-district-cannot-place), which is blocking and asks whether a document maps to a filing slot at all. A document can map to a slot perfectly well and still be one the district will not take electronically.

### Packet integrity

Two advisory findings look at how the packet itself is put together, so defects that used to surface as a failed submission are visible while the packet is still being reviewed.

- **Two documents on the same filing slot.** Each document in the packet goes to a specific slot in the district's filing system, and a slot takes one document. Where two have been assigned to the same slot — two credit counseling certificates on the credit counseling slot is the case firms hit — the finding **names both documents** so you can tell which one to move or remove. Left in place, this fails at submission, and a filing can hard-fail repeatedly against every engine tried.
- **A tagged document missing its file.** A document tagged for a filing slot has to carry the file the district's system will send. Where that link is missing, the finding names the document. These are older records; a tag created from now on cannot end up in this state.

Both start as advisory, so neither gates a filing today — they are there to be read and cleared. **Expect findings on cases that have been sitting unfiled**: a platform-wide check found several hundred workflows with more than one document on a single slot, most of them not yet filed. Working through those findings before filing is the point of the check.

### Form 121 inside the petition

The Statement About Your Social Security Numbers (Form 121) contains the debtor's full Social Security number and is not filed on the public docket as part of the petition. The review reads the compiled petition itself and blocks the filing if Form 121 appears anywhere inside it.

- Applies to every Chapter 7 and Chapter 13 case, in every district.
- The finding gives the **page numbers** where the form appears, so your team can find it and remove it from the petition before filing. It never repeats any Social Security number digits.
- The voluntary petition (Form 101), which shows only the last four digits of the number, is not mistaken for Form 121.
- The check runs on the initial review, when the review is run manually, and again whenever the petition is regenerated — so a petition with the form shows a failed finding the first time the case is reviewed.
- **If the check cannot read every page of the petition, it reports as inconclusive and does not block submission.** An inconclusive result means the petition was not fully checked, not that it is clean.
- This was added after a district's petition setup stopped leaving Form 121 out of the compiled petition, and petitions reached the public docket with the form inside. Nothing read the petition itself before filing until now.

This check looks only inside the compiled petition. It does not affect Form 121 filed as its own separate document where the district expects one. See [Filing packet required documents](../filing-packet/required-documents.md).

## Edge Cases & Limitations

- The Form 121 check does not gate submission when it is inconclusive. If it reports inconclusive, check the petition for Form 121 by hand before filing.

- The check on whether a district will accept a document electronically is advisory, so a filing can proceed past it. The court's system will still refuse the document — filing over the finding converts an early warning into a rejection after submission.
- A district's answer about a document can depend on the shape of the case, so the same document can raise a finding on one case and none on another in the same district.
- The packet integrity checks are advisory, so a packet with two documents on one filing slot can still be submitted — and will still fail at submission. Clear the finding rather than filing past it.
- The duplicate-slot and incomplete-tag checks are not repaired automatically and no bulk clean-up has been run. Cases that have been waiting to file will surface findings for defects that have been sitting on them for some time.

## Related Features

- [Pre-filing Review](./README.md)
- [Filing packet document types](../filing-packet/document-types.md)
- [Required documents check](./required-documents.md)
- [PDF and image conversion](../filing-packet/file-conversion.md)
