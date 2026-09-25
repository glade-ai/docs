# More Than One Organizer on a Case

## Overview

A case can carry more than one income organizer — typically one for the primary debtor and a second for a joint debtor or a non-filing spouse. Every organizer on the case is now visible and usable, where previously only the first one could be reached.

## Key Behaviors

- Where a questionnaire offers **Source Data** links, each organizer appears as its own labeled entry (for example, *Income Organizer · Pay Organizer (Debtor 1)*). Opening an entry takes you to that organizer. A case with only one organizer shows a single unlabeled link, exactly as before.
- On an organizer's detail page, a badge names whose income it holds — **Primary**, **Debtor 2**, or **Non-filing spouse**. The badge only appears when the case has more than one organizer, so single-organizer cases are unchanged.
- Importing income into a questionnaire is not limited to one organizer. The import pulls from every income organizer on the case, so a joint case fills both Schedule I columns from a single import.

Before this, an attorney could not see or add income for a non-filing spouse even after a second organizer existed on the case — the interface showed only the first one it found.

### Each debtor's Schedule I total stays with that debtor

On a joint case, an income source belongs to the debtor it is recorded against, and that debtor's Schedule I total is worked out from the sources that belong to them. A source added for debtor 2 is attached to debtor 2's organizer even if it was entered from debtor 1's, so the two never mix.

Two problems on joint cases came from the same cause and are both resolved:

- **Debtor 2's income no longer lands on debtor 1's Schedule I.** A source tagged for one debtor could sit on the other's organizer, and its amount was then carried onto the wrong debtor's schedule.
- **An edit after the initial entry updates the total.** Where a source was on the wrong debtor's organizer, editing an amount recalculated the *other* debtor's organizer — which was empty — so the figure on screen never moved however many times it was corrected.

Existing cases are corrected the next time the organizer is opened or recalculated; there is nothing to run. **Re-check Schedule I on any joint case prepared earlier** — a debtor showing income that belongs to their spouse, or a total that did not respond to a correction, is the symptom.

## Edge Cases & Limitations

- The debtor badge on an organizer's detail page only appears when the case has more than one income organizer. A single-organizer case shows no badge, which is not an indication that the organizer is unlabeled.

## Related Features

- [Income Organizer](./README.md)
- [Schedule I](./schedule-i.md)
- [Business and Rental Income: Adding Business Sources](./business-and-rental-income/adding-business-sources.md) — recording which contact a business or rental belongs to
- [Questionnaires](../questionnaires/README.md)
