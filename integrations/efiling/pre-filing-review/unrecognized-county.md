# An Unrecognized County

## Overview

The court's filing system identifies the debtor's county by a standard code, and Glade has to translate the county written on the case into that code. When the county on a debtor's address is not one Glade recognizes for that state, the pre-filing review reports it as a blocking item against that debtor, naming the county as it was entered.

## Key Behaviors

- When the county on a debtor's address is not one Glade recognizes for that state, the pre-filing review reports it as a blocking item against that debtor, naming the county as it was entered. It is now handled like any other review item rather than stopping the required-fields check or the submission with an unexplained error, so the problem is described in one place alongside everything else the review found.
- Occasionally Glade cannot translate the county — a county name that exists in more than one state, or an address whose ZIP code points at a neighboring state, are the usual causes.
- This is reported as a **blocking pre-filing finding that names the county and state it could not identify**, so your team can see immediately what the obstruction is and which address to check.
- Previously the same situation produced a dead-end error partway through the required-fields check, with no route to a fix and no indication of which value was at fault.

### Suggestions

Where Glade can tell what the county was meant to be, the finding says so:

- **A county that exists in another state** is named with that state — up to three of them. The usual cause is the wrong state on the address rather than a mistyped county.
- **A county spelled one character away from a real county in the same state** is offered as a "did you mean" suggestion.
- **Where there is no confident answer** — nothing close, or two candidates equally close — the finding says the county could not be matched and asks you to contact support, rather than guessing at one.

Suggestions are there to read. Glade never substitutes a suggested county on its own, because filing under the wrong county is worse than being asked to check. Correct the address on the case and run the review again.

### Fixing it

- Start by checking the debtor's address, since the wrong state on an otherwise correct county is the most common cause. Where the address is right and the county is genuinely one Glade does not yet recognize, contact support — the list of counties is maintained by Glade and the addition is quick.
- Submission itself still refuses to proceed on an unrecognized county. The check makes the reason visible early rather than changing whether the filing can go ahead. If you submit anyway, the submission is refused naming the county lookup as the rule that failed.

Cases in **McKean County, Pennsylvania** were affected by an unrecognized spelling until August 2026 and file normally now.

## Edge Cases & Limitations

- An unrecognized county is reported by the pre-filing review as a blocking item on the debtor it belongs to, with a suggestion where Glade can offer one. Correcting the address clears it. A county that is spelled correctly and still not recognized needs Glade to add it — contact support with the case and the county.

## Related Features

- [Pre-filing Review](./README.md)
- [Required fields check](./required-fields.md)
- [Why a filing is blocked](../blocked-filings.md)
