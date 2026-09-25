# Pre-filing Review

## Overview

Before a petition can be submitted, Glade runs a set of automated checks against the case and reports what needs attention. Each finding is either **blocking** — submission is gated until the item is resolved or an attorney signs off on it — or **advisory**, which flags the issue without gating submission.

## Key Behaviors

### Active checks

The following checks are active:

| Check | What it looks for | Severity |
|-------|-------------------|----------|
| Required documents in the packet | Every document the filing district requires for the case's chapter is present in the packet | Blocking |
| Statement of Intention required | The Statement of Intention (Form 108) is included on a Chapter 7 case that needs one | Blocking |
| Debtor type supported by the district | The case's debtor type is one Glade can file in that district | Blocking |
| Negative amounts on the case-upload data | None of the dollar figures sent to the court with the case can be negative | Blocking |
| Documents the district can place | Every document in the packet maps to a filing slot the district accepts | Blocking |
| Required filing fields | Every debtor field the filing needs has an answer | Blocking |
| Debtor's county recognized | The county on each debtor's address is one Glade recognizes for that state | Blocking |
| Case already has a case number | The case has not already been assigned a number by the court | Blocking |
| A filing is already in progress | No other filing is underway on the case | Blocking |
| District supports a joint petition | The filing district accepts joint petitions for the chapter being filed, on a case being filed jointly | Blocking |
| Non-filing spouse accepted by the district | The district accepts a married debtor filing individually with a non-filing spouse | Blocking |
| Presumption of abuse (Idaho) | On an Idaho Chapter 7 means-test case, the presumption of abuse is answered "no" | Blocking |
| Court office identified | The case's division resolves to an office the court's filing system recognizes | Blocking |
| An attorney is assigned to file | The case has a filing attorney, either assigned on the case or set as the firm's default | Blocking |
| Petition out of date | The compiled petition is older than the case data or questionnaire answers behind it | Advisory |
| Required signatures on the petition | Everyone required to sign the petition has signed, everywhere a signature is called for | Advisory |
| Duplicate creditors | The creditor mailing matrix lists the same creditor more than once under slightly different details | Advisory |
| A recent filing attempt on the case | The case was attempted recently enough to be worth a second look before trying again | Advisory |
| Schedule I / J figures missing | (Chapter 7) The income and expense figures the surplus comparison needs are present | Advisory |
| Court notice matched to a client | A court notice held on the case matches this client | Advisory |
| Document the district will accept electronically | Every tagged document in the packet is one the district's filing system will accept for this case as it stands | Advisory |
| Presumption of abuse answered (New Mexico) | On a New Mexico Chapter 7 case that is not exempt from the means test, the presumption of abuse is answered yes or no | Blocking |
| Joint means-test-exempt filing (Ohio Southern) | The case is not a joint Chapter 7 filing claiming a means-test exemption, which Ohio Southern does not accept | Blocking |
| Chapter supported for e-filing (New Mexico, Ohio Southern) | The chapter being filed is one Glade can e-file in that district | Blocking |
| Duplicate filing slots | No two documents in the packet are assigned to the same filing slot | Advisory |
| Incomplete PACER tags | Every tagged document in the packet carries the file the district's system needs | Advisory |

### How findings are reported

- **A check that could not reach a conclusion says so.** When a check depends on case information that is missing, its finding is worded as unresolved and names the check, rather than asserting that the case failed it. Previously an inconclusive result was written in exactly the same language as a genuine failure, so a check that simply had nothing to go on read as a defect in the case — and teams went looking for a problem that was not there. Treat an unresolved finding as "supply the missing information and run the review again", not as something to correct on the petition.
- **Every check needs the case's chapter.** Glade works it out from the case record, falling back to the chapter recorded on the case itself and then to the rest of the case's data. Previously the chapter was read from one place only, so a case where it had not been recorded there — typically a case opened without a case type set — had every check come back as not evaluated for a missing chapter, and the review produced nothing usable. If the chapter genuinely cannot be determined, the checks still report as not evaluated rather than passing.
- **"Petition out of date" reflects the petition's own inputs.** It is raised when the case data or the questionnaire answers the petition is built from have changed since it was compiled. Adding a supporting document to the filing packet no longer raises it — the petition is a merge of the selected forms and schedules, so an unrelated PDF added alongside them does not make it out of date. Previously any addition to the packet flagged the petition and prompted a recompile that changed nothing.

### Where pre-filing checks run

Every pre-filing rule lives in the pre-filing review. There is no longer a separate set of warnings computed at the moment you submit that could disagree with what the review reported.

- The review is the single place a filing is gated. A filing blocked by a rule is stopped at submission with the specific rules that failed, named — so a case that passes the review passes for the same reasons at submit time.
- The older dialog that raised its own required-field warnings on the last click has been removed, along with the duplicate rules behind it. Nothing your team relied on is no longer checked; the same conditions are enforced, in one place, and visible earlier.
- An unrecognized county is one of these. It is now reported by the review and, if you submit anyway, refused at submit time naming the county lookup as the rule that failed.

### Checks not yet enabled

Credit counseling recency was held back from the first release and has since been switched on — see [Certificate recency before filing](../../abacus-credit-counseling.md) for what it reports. The remaining checks — Social Security number completeness, fee-waiver and installment applications, and prior-discharge advisories — are still turned off and are planned for later releases. The review catches a specific set of problems; it is not a substitute for reviewing the packet.

> TODO: Confirm the exact condition under which the Statement of Intention check applies. It is a conditional requirement tied to the case's secured claims and fee election rather than one that applies to every Chapter 7 filing.

## Topics

- [Required documents](./required-documents.md) — missing required documents, fee and means-test forms, joint-only documents, and skeleton filings.
- [Required fields](./required-fields.md) — the debtor fields and court-required answers checked before filing.
- [Submission checks and duplicate filings](./submission-checks.md) — existing case numbers, filings in progress, recent attempts, and other checks that used to appear only at submission.
- [An unrecognized county](./unrecognized-county.md) — how a county Glade cannot identify is reported, with suggestions.
- [District rules](./district-rules.md) — debtor types, joint petitions, non-filing spouses, presumption of abuse, court offices, and Chapter 7-only districts.
- [An attorney is assigned to file](./filing-attorney.md) — the filing attorney check.
- [Packet checks](./packet-checks.md) — unplaceable documents, documents the district will not accept electronically, and packet integrity.
- [Required signatures on the petition](./petition-signatures.md) — the advisory signature check.
- [Duplicate creditors](./duplicate-creditors.md) — near-duplicate creditors on the mailing matrix.
- [Credit counseling checks](./credit-counseling.md) — certificate recency findings.
- [Who can clear a blocking finding](./clearing-findings.md) — sign-off permissions.
- Negative amounts on the case-upload data — see [Case upload files](../../pacer/case-upload-files.md#negative-amounts-in-the-pre-filing-review).

## Related Features

- [Electronic Court Filing (eFiling)](../README.md)
- [Why a filing is blocked](../blocked-filings.md)
- [Filing Packet](../filing-packet/README.md)
- [Chapter handling](../../pacer/chapter-handling.md)
