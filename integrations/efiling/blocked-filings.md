# Why a Filing Is Blocked

## Overview

When a filing cannot be submitted, the eFiling modal explains the specific reason instead of showing a generic error, so your team knows what to address before trying again.

## Key Behaviors

- When a filing cannot be submitted, the eFiling modal explains the specific reason instead of showing a generic error, so your team knows what to address before trying again. Common reasons include missing required case information, missing required documents, a filing district that has not been set up for the case, and permission restrictions. The same explanation appears in the modal's alert and in the accompanying notification.
- When the required-fields check reports a problem with the case's data rather than a missing field — an address whose county cannot be identified, for example — the specific problem is named in the pre-filing review and in the submission modal, so your team can correct the data. Previously these were reported as the check being temporarily unavailable, which read as a Glade outage and invited retries that could not succeed. See [Required fields check before filing](./pre-filing-review/required-fields.md).
- When a filing is blocked because the case's filing district has not been set up, a **Fix this** action appears inline. Completing the district setup from that prompt clears the block, so you can continue the submission without leaving the filing flow.
- A filing can also be held up because Glade cannot finish its check of the case's required fields, which shows as the required-fields check being unavailable rather than as a specific item to fix. This is not something your team can resolve on the case — contact support with the case, as it usually means Glade needs to correct something behind the scenes.
- When a filing is blocked by Glade's pre-filing review, the modal names the specific items that need attention — for example, "Form 122A-1 is not in the filing packet" — so your team can go straight to what is missing. Previously this case showed an unhelpful internal label with no indication of which forms were at fault. If a filing is blocked by more than 20 items at once, the first 20 are listed followed by a count of how many more remain. In the rare case where the review blocks a filing but reports no specifics, the modal asks you to resolve the flagged review items and try again.

## Edge Cases & Limitations

- The court's required answers and the joint-petition rule are checked against the district resolved for the case. On a case whose filing district has not been set up, those checks report as unresolved rather than passing, and the district block is what needs clearing first.

## Related Features

- [Electronic Court Filing (eFiling)](./README.md)
- [Pre-filing review](./pre-filing-review/README.md)
- [Required fields check](./pre-filing-review/required-fields.md)
- [An unrecognized county](./pre-filing-review/unrecognized-county.md)
