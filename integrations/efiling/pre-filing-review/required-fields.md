# Required Fields Check

## Overview

Before a filing can be submitted, Glade validates that all required debtor fields are present, including the answers the court itself asks for when a case is opened. If any are missing, the filing is blocked at both the pre-filing preview and the ECF submission modal, and the missing fields are listed by name so your team can address them before re-attempting.

## Key Behaviors

### Required debtor fields

- Glade checks these fields in the questionnaire data — if the information has been collected but not yet saved, save the questionnaire before initiating the filing.
- Missing fields are shown with labels — for example, "Marital filing status" — so you can identify exactly what needs to be filled in. An **Open questionnaire** link in the error state takes you directly to the case questionnaire.
- If a filing attempt fails because required fields are still missing at the point of submission, the eFiling modal names the specific missing fields so your team knows exactly what to complete before retrying.
- **The same checks now also run as part of the pre-filing review.** Missing required fields appear there as a blocking item alongside the rest of the review's findings, rather than only in the dialog at submission.
- The **credit counseling completion date** is no longer part of this check. A Chapter 7 or Chapter 13 filing is no longer stopped because that date is absent from the case questionnaire — firms whose Schedules questionnaire does not ask for it can file with the certificate itself as the record of completion, for individual and joint cases alike. Whether the briefing is recent enough to satisfy § 109(h) is assessed by the pre-filing review instead of by this check, so a stale certificate is raised for an attorney to review rather than blocking the filing outright with no explanation. See [Credit counseling checks](./credit-counseling.md).
- For individual Chapter 7 filings, the **marital filing status** is required. Submission is blocked if the answer is missing from the questionnaire, and the missing field is named in the eFiling error so the team can fill it before retrying. For joint Chapter 7 filings, when the questionnaire indicates the petition is filed jointly but the marital filing status answer was not provided, Glade infers "Married, filing jointly" automatically — joint Chapter 7 filings no longer fail because of an unanswered marital status question.
- Whether the case is joint or individual is read from the **Schedules** questionnaire only, not from custom client-intake forms or earlier questionnaires that may carry stale answers. Cases that were initially entered as joint and later corrected to individual (or vice versa) on the Schedules questionnaire reflect the corrected value at filing time.
  - Checks that only apply to a second debtor use the same answer. On an individual filing where nothing else on the case indicates whether it is joint or individual, those checks no longer report an unresolved second-debtor result — an individual Chapter 7 stops showing a "(Debtor 2)" line for things like a co-debtor's briefing or Social Security number.

### Problems with the data, and outages

- **When the check itself reports a problem with the data, that problem is shown.** Some failures are not about a blank field but about a value the check cannot work with. Those appear as the specific problem to fix, in both the pre-filing warnings dialog and the submission modal. Previously any failure of this kind read as "Required-Fields Check Unavailable — retry shortly", which looked like a Glade outage and left teams retrying a filing that would never succeed until the underlying data was corrected. A genuine outage still reports as unavailable, so the two are now distinguishable.
- **An unrecognized county no longer stops this check, or the submission.** An address whose county Glade cannot identify used to end the check with an error modal at both the pre-filing preview and the point of submission. It is now raised by the pre-filing review as its own blocking item against the debtor it belongs to, with a suggested county where one can be offered — so the case is gated in the same place as everything else that needs attention, and with something to act on. See [An unrecognized county](./unrecognized-county.md). The check still reports every other missing or unusable field as it did before.

### The court's own required answers are checked before you file

Opening a case with the court asks for a set of answers beyond the petition itself — the nature of the debtor's debts, the fee treatment elected, prior filings, the estimated number of creditors, estimated assets and liabilities, the county, marital filing status, and the means-test presumption. A missing or contradictory answer used to stop the filing **during** submission, appearing as a "Required-Fields Check Failed" message partway through, with the case left to retry.

- These are now checked as part of the pre-filing review, so a missing answer is named in the review panel **before** anyone starts a submission.
- Each answer is reported as its own blocking item naming what is missing, rather than one combined failure.
- Which answers are required depends on the filing district — courts do not all ask for the same things — so the review reflects what the case's own court expects.
- The consistency of the joint-filing answers is checked as well: a case that says it is filed jointly in one place and individually in another is reported rather than being sent to the court to be rejected.
- Submission still runs its own check at the moment you file, so nothing gets through on a stale review. The difference is that the problem is visible earlier and described in the same place as every other finding.

### Two answers no longer hold a submission back

Two of these answers were also enforced at the moment of submission, which stopped filings the court would have accepted:

- **Marital filing status** no longer blocks a Chapter 7 individual filing at submission when it has been left unanswered.
- **Whether the case is filed jointly** no longer has to be answered Yes or No to submit.

**An unanswered joint-filing question files the case as an individual filing.** Nothing is assumed from a blank answer, so a case meant to be filed jointly and left unanswered goes to the court as an individual petition. Confirm that answer before submitting a joint case — this is the one situation where the removed check was doing useful work.

The pre-filing review still reports the answers the case's own district requires, and it remains the place to clear them.

> TODO: The marital filing status bullet under "Required debtor fields" (submission blocked when missing on an individual Chapter 7) and "Two answers no longer hold a submission back" (not enforced at submission) come from separate source docs and disagree. Confirm current behavior and remove the outdated statement.

## Edge Cases & Limitations

- An unanswered joint-filing question no longer stops a submission, and is treated as an individual filing. A joint case that has never had the question answered is therefore submitted as an individual petition rather than being held back — check the answer before filing a joint case.
- Marital filing status is no longer enforced at submission on a Chapter 7 individual filing. Where the case's district requires it, the pre-filing review is the only place it is reported.
- The court's required answers are checked against the district resolved for the case. On a case whose filing district has not been set up, those checks report as unresolved rather than passing, and the district block is what needs clearing first.

## Related Features

- [Pre-filing Review](./README.md)
- [Submission checks and duplicate filings](./submission-checks.md)
- [An unrecognized county](./unrecognized-county.md)
- [Why a filing is blocked](../blocked-filings.md)
- [Attorney compensation disclosure (Form 2030)](../../pacer/attorney-compensation-disclosure.md)
