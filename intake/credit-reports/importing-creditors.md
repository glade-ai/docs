# Importing Creditors from a Report

## Overview

When a credit report comes back, Glade brings its accounts onto the case as creditors so they reach the client questionnaire, the Master Creditor List, and Schedules D, E, and F. This page covers how imported names are formatted, how collection accounts carry their original creditor, how owned real estate is identified, how older reports are imported into case data, and what happens on joint cases and on reports that arrive with no creditors.

## Key Behaviors

### Imported creditor names

Credit bureaus report creditor and account names in all capitals. Glade converts them to normal reading case as the report is imported, so they read cleanly in the client questionnaire and on Schedules D, E, and F without anyone re-typing them by hand.

- Bank initialisms and legal entity suffixes stay capitalized. `CREDIT ONE BANK NA` imports as `Credit One Bank NA`, `EXETER FINANCE LLC` as `Exeter Finance LLC`, and `MACYS/CBNA` as `Macys/CBNA` — rather than as `Na`, `Llc`, and `Cbna`. Since these names are filed with the court, getting the suffixes right is the difference between a name that can be filed as-is and one that still needs correcting.
- Only names that arrive entirely in capitals are reformatted. A name that already carries mixed case — because someone at your firm corrected it, or because the bureau sent it that way — is left exactly as it is.
- **Reports pulled before this formatting existed are covered too.** Glade keeps a copy of each report as it was received, and reads from that copy whenever it brings creditors onto a case. Older reports held their names in all capitals, so a case could end up with `CAPITAL ONE` on one Schedule F row and `Capital One` on another for the same creditor, depending on when each row arrived. Reading formatting is now applied at the moment the stored report is read, so anything newly brought across from an older report arrives in reading case as well. There is no need to re-pull a report for this.
- **Names already written onto a case are not rewritten.** This governs what arrives from the report from now on. Where a case already carries an all-capitals creditor, correct it on the case — bringing the report across again will not change what is already there.

### Collection accounts and the original creditor

A collection account is reported under the collection agency's name, which tells you who to notice but not what the debt was for. Matching those accounts against a client's paper bills previously meant cross-referencing them by hand.

- Glade now records the **original creditor** on each collection account alongside the collection agency. The agency stays the account name, and the original creditor is carried onto Schedule F.
- Where the report provides the original creditor as its own field, Glade reads it directly. Where the bureau states it only as a remark on the account (for example, `ORIGINAL CREDITOR: PROGRESSIVE, ASSIGNED ON 10/22`), Glade reads it out of that remark. Both are recognized, including reports where the same debt appears as two agency rows from different bureaus and only one of them spells out the original creditor.
- Remarks are only read on collection accounts, so descriptive text on an ordinary account is not mistaken for a creditor name.
- The original creditor is treated like any other imported value — your team can correct it, and a correction takes precedence over what the report said.
- Some reports list collection accounts in a section separate from the client's other accounts. Those accounts were previously not imported at all; they now come through with the rest.

### Imported real-estate addresses

When Glade imports addresses from a credit report into the case as real-estate assets, it imports only addresses the client actually owns. Glade uses the credit report's owner-match indicator on each address to make this determination, so prior addresses where the client lived but did not own the property are no longer imported as real-estate assets even if they have transaction history.

### Creditors reach the case on the first successful pull

On a joint case, creditors from the credit report now reach the case record as soon as the first debtor's report comes back, instead of waiting for every debtor.

- Previously the import ran only once *all* debtors had a response. When a co-debtor never approved their own pull, the main debtor's accounts stayed inside the stored report and never reached the Master Creditor List — so attorneys saw creditors missing, or creditor addresses blank, until something else on the case happened to fill them in.
- Each successful pull now imports its own creditors immediately.
- When the co-debtor's report arrives later, its creditors are added alongside the first debtor's. The creditors already on the case keep their identity, their addresses, and any corrections your team made to them — they are not renumbered, duplicated, or replaced.
- Reports that already completed keep using the existing import, so nothing needs re-running on a case that is already correct.

### Importing a report into case data

A completed credit report can be imported into the case record so its tradelines become creditors on the case. This is how a report that was pulled before the case record held creditors gets its accounts onto the schedules.

- **Creditors already on the case are kept.** Creditors your team entered, and creditors that came from the client's questionnaire, survive the import. Only the report's own tradelines are added.
- Tradelines that match a creditor already imported from the report update that creditor rather than creating a second copy, so running the import twice does not double the creditor list.
- The import is offered on older cases — those opened before the case record began taking creditors from reports automatically. On a newer case the report's creditors already arrive on their own and there is nothing to import.

An earlier version of this import cleared every creditor on the case before adding the report's, which would have discarded questionnaire-entered creditors. It no longer removes anything.

> TODO: Confirm where the import action appears on the case and which roles can run it.

### When a report comes back with no creditors

A credit report pull can finish successfully and still leave the case with no creditors on it — the report is retrieved and stored, but none of its accounts reach the schedules.

- This happened when a report described a foreclosure in a format Glade could not read. A single unreadable property record discarded every tradeline in the report, so the pull reported success while the schedules stayed empty.
- Property records Glade cannot read are now skipped individually. The accounts in the report come across regardless, and only the property record itself is left out.
- **Reports already in this state are not repaired automatically.** If a case shows a completed credit report but no creditors from it, contact support to have the stored report re-read — do not re-pull, since pulls are billed from the first pull.

## Edge Cases & Limitations

- Creditor name formatting applies as creditors are brought onto a case, including from reports pulled before the formatting existed. It does not reach back over creditors already saved on a case — those keep the form they were written with and need correcting by hand. On a case where the same creditor already appears in two casings, expect to fix the older rows yourself.
- An abbreviation that is neither a recognized initialism nor a normal word may stay capitalized — `SW STDNT SRV`, for example. The name is still readable and filed as shown; correct it by hand if the court copy needs it spelled out.
- The original creditor is recorded only when the report names one. A collection account whose report gives no original creditor shows the agency alone, as before.
- A creditor that arrives from the report with no address at all — some collection agencies come through this way — opens for editing with empty address fields, and appears normally in creditor lists and pickers. Previously such a creditor could stop the creditor form or the list from loading at all. An address is still required before the creditor can be saved, so fill it in before filing.
- The owned-property filter on imported real-estate addresses applies to reports pulled or refreshed after this behavior took effect. If an owned property is missing from the imported real estate on a report that was pulled earlier, re-pull the report to apply the current filter.
- Importing a report into case data adds the report's creditors and updates ones it has already contributed. It does not remove a creditor, so a creditor that should not be on the case has to be removed by hand.
- A report that completed with no creditors because of an unreadable property record needs support to re-read the stored report. Re-pulling produces a fresh billable pull and is not the fix.
- Importing creditors on the first successful pull does not reach back over joint reports that already completed. On a joint case where the main debtor's creditors never arrived and the report is already marked complete, contact support to have the stored report re-read rather than re-pulling.

## Related Features

- [Credit Reports](./README.md)
- [Pulling a Credit Report](./pulling-a-report.md)
- [Pulling a Report Again](./pulling-again.md)
- [Case Management](../../back-office/case-management.md)
