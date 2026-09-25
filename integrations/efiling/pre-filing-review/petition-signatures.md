# Required Signatures on the Petition

## Overview

The signature check reads the assembled petition that is actually about to be filed and confirms that everyone required to sign it has done so. It is an advisory check.

## Key Behaviors

- **Who it expects to have signed** — the debtor on every case, the second debtor on a joint case, and the attorney when the debtor is represented. If Glade cannot tell from the case whether the debtor is represented, the check does not assume they are unrepresented.
- **Where it looks** — across the whole filing bundle, not one form. That includes the petition itself, the attorney and fee forms, the declaration about the schedules, the statement of financial affairs, the statement of intention, and the verification of the creditor matrix, plus any other signature block it finds in the document.
- **What counts as a signature** — typed, electronically signed, or handwritten on a printed and scanned page all count. Firms that print, sign in ink, and re-upload are covered the same as firms that sign electronically.
- **What it reports** — **Passed**, **Failed** with the signer who is missing and the form they are missing from, or **Inconclusive** when it cannot read the document or is not confident enough to call it. An explanation in plain English appears next to the other pre-filing findings.
- **It does not gate filing.** The check is advisory for now: it warns and can be set aside, and a Failed or Inconclusive result never blocks submission. Treat it as a second pair of eyes on the packet, not as a guarantee.
- **It re-reads the petition when the petition changes, not on every review.** Because the check reads the assembled document, it runs again after the petition is regenerated, or when someone asks for the review to be run manually. On the automatic refreshes that follow unrelated edits — a change to case data, a questionnaire save — it keeps its most recent verdict, which stays listed with its explanation rather than disappearing or being recalculated against a petition that has not moved. If you have corrected signatures on the source documents and want a fresh verdict, regenerate the petition or run the review manually.

Because it reads the pages rather than checking a stored answer, the check is deliberately cautious — it reports Inconclusive rather than guessing on a court filing. An Inconclusive result means the check could not reach a verdict, not that a signature is missing.

## Edge Cases & Limitations

- The petition signature check needs the compiled petition to be available. If the petition cannot be read, the check reports Inconclusive rather than passing or failing.
- The petition signature check is advisory and cannot currently be dismissed the way the other pre-filing findings can. It reappears on each review until the signatures are in place.

## Related Features

- [Pre-filing Review](./README.md)
- [Filing Packet](../filing-packet/README.md)
