# District Rules Checked Before Filing

## Overview

Some filings are valid in one district and not in another. The pre-filing review checks the case against district requirements that previously cleared the review and only failed once a submission was underway — debtor types, joint petitions, non-filing spouses, presumption-of-abuse answers, court offices, and which chapters a district can be e-filed in.

## Key Behaviors

### Debtor type supported by the district

Glade files cases for individual debtors. A case recorded as a corporation or a partnership is reported at review time as a debtor type the district cannot take, naming both the debtor type and the district, instead of failing at submission with a message that pointed at nothing you could fix.

- A debtor type Glade does not recognise at all is not treated as unsupported — the check reports itself as unresolved rather than blocking a case over an entry it cannot read.
- This is a check on what Glade can file today, not on the court's own rules. Districts that begin accepting other debtor types will be enabled individually.

### Joint petitions in districts that do not accept them

Some districts do not accept joint petitions. A joint case in one of those districts was previously submitted anyway and failed after the fact, with the rejection arriving by email rather than in Glade.

- A joint filing in a district that does not support joint petitions is now a blocking pre-filing finding, and names the district it applies to.
- An individual filing raises nothing — the check does not apply.
- If Glade cannot yet tell whether the case is joint, or cannot resolve the district's rules, the check reports as unresolved rather than passing, so a joint case is never let through on an assumption.

**Some districts accept joint petitions in one chapter but not another.** Whether a district takes a joint filing can depend on the chapter, so the check reads the district's rule for the chapter the case is actually being filed under rather than a single yes-or-no answer for the district.

- **Pennsylvania Western** and **North Carolina Eastern** accept joint Chapter 7 petitions but not joint Chapter 13 petitions. A joint Chapter 13 case in either district is blocked at pre-filing review, where it previously passed the review and then failed at submission with a message that pointed at nothing on the case.
- Districts with no chapter-specific rule are unchanged and continue to be treated the same way in every chapter.

### District rules that used to fail at submission

Three further district requirements are now pre-filing findings rather than failures that surfaced only when a submission was already underway. Each previously cleared the review, so a firm reached **Sync to PACER** and the submission died with a generic error.

- **New Mexico and a non-filing spouse.** New Mexico does not accept a married debtor filing individually with a non-filing spouse. The finding says the case cannot be e-filed in New Mexico and to contact support. It does not suggest converting the case to a joint filing — a genuine non-filing spouse is not a data-entry mistake, and switching to joint would be the wrong correction.
- **Idaho and the presumption of abuse.** Idaho requires the presumption of abuse to be answered "no" on a Chapter 7 case that completes the means test. A case answering otherwise is blocked at review.
- **A division that does not resolve to a court office.** The court's filing system identifies the office handling the case from the case's division. Where the division is missing or does not map to an office, the filing is blocked at review, naming the problem, instead of failing during submission. Idaho and **Florida Northern** are the districts where this arises in practice; set the case's division to clear it.

**The court office check now covers every district that needs one.** It was first switched on for Idaho and Florida Northern, and applies to all of the districts whose filing system requires a court office: Florida Middle, Florida Northern, Florida Southern, Idaho, Louisiana Eastern, New Mexico, Ohio Southern, Pennsylvania Western, South Carolina, Virginia Eastern, and Washington Western. In each of those, a case whose division does not resolve to an office is now stopped at review rather than at submission.

Three further district requirements are checked at review for the same reason — each one previously cleared the review and then failed once a submission was already underway:

- **New Mexico and the presumption of abuse.** On a New Mexico Chapter 7 case that is not exempt from the means test, the presumption of abuse has to be answered yes or no. A case that leaves it unanswered is blocked at review.
- **Ohio Southern and a joint means-test-exempt filing.** Ohio Southern does not accept a joint Chapter 7 filing that claims an exemption from the means test. Such a case is blocked at review, naming the district.
- **New Mexico and Ohio Southern take Chapter 7 only.** A Chapter 13 case in either district cannot be filed electronically through Glade. The finding says so and tells your team to file the Chapter 13 with the court directly. Both districts still support Chapter 13 as a case type in Glade — the limitation is on electronic filing, not on running the case.

## Edge Cases & Limitations

- The joint-petition rule is checked against the district resolved for the case. On a case whose filing district has not been set up, it reports as unresolved rather than passing, and the district block is what needs clearing first.
- Whether a district accepts a joint petition is now answered per chapter. A district's general joint-petition setting still applies wherever no chapter-specific rule has been recorded for it, so a district that blocks joint filings in only one chapter needs that rule recorded before the review can tell the difference — contact support if a district's joint-filing behavior does not match its local rules.
- The New Mexico non-filing-spouse rule blocks the filing and cannot be cleared on the case. Contact support for a case in that position rather than converting it to a joint filing.
- The New Mexico and Ohio Southern Chapter 7-only rule blocks electronic filing and cannot be cleared on the case. File the Chapter 13 with the court directly.

## Related Features

- [Pre-filing Review](./README.md)
- [Supported courts](../../pacer/supported-courts.md)
- [Required fields check](./required-fields.md)
- [Chapter handling](../../pacer/chapter-handling.md)
