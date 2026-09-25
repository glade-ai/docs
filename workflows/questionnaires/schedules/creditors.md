# Creditors

## Overview

Bankruptcy questionnaires keep the case's creditors on the Master Creditor List, from which Schedules D, E/F, G, and H and the creditor mailing matrix are produced. This page covers adding creditors, marking duplicates, how creditors are ordered on the schedules, and how the creditor matrix is assembled.

## Key Behaviors

### Adding Creditors

The add-creditor flow in bankruptcy questionnaires is optimized to keep firms with large saved-creditor lists fast and to reduce manual schedule selection.

- Adding a creditor from the **Schedule E** tab defaults the new row's schedule to Schedule E. Adding from the **Schedule F** tab defaults to Schedule F. You can still change the schedule before saving, but the default matches the tab you're working from so the row lands on the right schedule without a manual pick.
- The saved-creditor search appears at the top of the add-creditor dialog (above the schedule selector), labeled with a magnifying-glass icon and a **Search for a creditor** placeholder. It lets you reuse a creditor your firm has previously saved instead of re-entering details.
- The saved-creditor search shows up to **100 matches** at a time. When more matches exist, a "Showing first 100 matches. Keep typing to narrow results." line appears at the bottom of the list — keep typing the creditor's name to narrow the result set. This keeps the dialog responsive for firms with tens of thousands of saved creditors.
- Saving a creditor row shows a **"Creditor saved successfully"** toast so you have explicit confirmation the row was written. If you save a row with required fields still missing, the confirmation prompt reads **"Item incomplete. Save anyway?"** — confirming saves the row in its incomplete state for you to come back to later.

### Creditor Duplicate Status

When you mark a creditor as a duplicate of another in a bankruptcy questionnaire, that status is saved to the case record and stays consistent everywhere the case's creditors appear:

- The duplicate mark syncs to the case record and to other questionnaires on the same case. The client and Schedules questionnaires keep their duplicate marks in step while both are open, so marking a creditor as a duplicate in one is reflected in the other.
- When a new questionnaire is seeded from the case record — for example, when Schedules is started — creditors already marked as duplicates come in already marked, instead of being dropped from the new list.
- Manual duplicate marks are preserved. Starting a new questionnaire no longer re-derives duplicates from scratch, so a creditor you marked by hand — for example, two creditors with the same name but no account number, which automatic matching cannot link on its own — stays marked.
- Un-marking a creditor clears its duplicate status the same way, across the case record and the other questionnaires.

**A list that has duplicates says so.** Rows marked as a duplicate are hidden from the list, and the list now carries a banner above it reading **"N items are currently marked as duplicate in this list"**, with a **Show Duplicates** action next to it for revealing them. The banner counts the hidden rows and appears only when the list actually has some — a list with no duplicates shows neither the banner nor the action. Previously the only sign that items had been tucked away was a small **Show duplicates** toggle, which was easy to miss, so a Master Creditor List could look shorter than it was with nothing to indicate why.

For selecting, removing, and restoring creditors with duplicates, see [Working With Lists](../filling-out/working-with-lists.md).

### Creditors are alphabetized on Schedules D and E/F

When the schedules are filled, the creditors on **Schedule D** and **Schedule E/F** are put in alphabetical order by creditor name. Each part of Form 106E/F is ordered independently, so the priority creditors in Part 1 run A→Z and the nonpriority creditors in Part 2 start again at A.

- Previously these schedules printed creditors in the order the rows happened to sit in the Master Creditor List, which is the order they were added. The creditors loaded from the credit report arrived alphabetically, and everything added afterwards — by hand, or from the case record — was appended to the end. A filed schedule could therefore show two or three alphabetical runs stacked on top of each other, which is the state trustees have raised with firms.
- The **Creditor Matrix** and the creditor list sent to the court were always alphabetized and are unchanged. It was only the schedules that could disagree with them.
- A row with no creditor name on it sorts to the bottom, so a half-filled row cannot take the first line of a schedule.
- Only the Master Creditor List is ordered. The **others to be notified** lists on Schedule D and Schedule E/F are separate lists and are not sorted — check with your trustee whether they expect those alphabetized too.
- Existing cases are corrected the next time the petition is generated. Nothing needs to be re-entered, and a case already filed is unaffected.

The order shown in the questionnaire itself is still the order the rows were added, so the on-screen list will not match the filed schedule. The **Sort** action on the Master Creditor List reorders the stored rows if you want the two to agree.

### Creditor Matrix

The creditor mailing matrix is assembled from every party who should receive notice on the case: the master creditor list, anyone added to the Schedule D and Schedule E/F "others to be notified" lists, and co-debtors entered on Schedule H. Because Schedule H co-debtors are pulled in automatically, you no longer need to add them to the matrix by hand or list them elsewhere to make sure they are noticed — entering a co-debtor on Schedule H is enough for them to appear on the generated matrix.

#### Keeping a creditor off the matrix but on the schedules

The Master Creditor List carries an **Omit from creditor matrix** checkbox. A creditor checked this way is left out of both the **Creditor Matrix** document and the creditor list submitted to the court, while staying everywhere else it belongs — on its schedule, in case data, in the Chapter 13 calculator, and on the filled schedule PDFs.

This is for the creditor a case has to disclose but should not notice. The usual example is a landlord on Schedule G where the debtor is current on the lease and is not rejecting it: the lease is disclosed, but there is no reason to mail the landlord notice of the case.

- **It is a different control from Omit from PDFs**, which takes the creditor off the schedules as well as the matrix. Use **Omit from PDFs** when the creditor should not appear at all, and **Omit from creditor matrix** when the creditor must still be disclosed on a schedule.
- A creditor checked **Omit from PDFs** is still left off the matrix, as before. Checking either one keeps the creditor off the mailing matrix.
- Both the Creditor Matrix document and the court's creditor list honor the checkbox, so the two agree.
- **Omitting or restoring a creditor is recorded on the case.** The activity log names the creditor and the team member who made the change, so the decision has a name and a date against it. The entry is written when the schedules questionnaire is completed, since that is when the matrix is compiled. See [Case Management](../../../back-office/case-management.md).

#### How duplicate entries are collapsed

The same creditor entered more than once produces one entry on the matrix rather than several. Two changes make that more reliable:

- **A nine-digit ZIP and its five-digit form are treated as the same address.** An entry at `60184-1234` and one at `60184` are the same creditor, and are collapsed into one. Previously they were kept as two separate notice entries for the same party.
- **The more complete address is the one that prints.** Where the same creditor appears with both forms, the matrix keeps the nine-digit ZIP. Which entry your team happened to add first no longer decides which address the court sees.
- Capitalization, punctuation, and stray spacing in a creditor's name or address no longer prevent two entries from being recognized as the same one.
- **Genuinely different ZIP codes stay separate.** `60184` and `60185` are two addresses and produce two entries. Glade does not merge creditors that differ in a way it cannot be sure about — dropping a genuinely distinct creditor from the mailing matrix is a notice problem, so the collapse is deliberately conservative.

The same rules apply to both the **Creditor Matrix** document and the creditor list submitted to the court, so the two always agree. A matrix that had no duplicates in it is unchanged.

#### The matrix in the petition draft

The creditor matrix is also included in the **petition draft** — the review copy generated when the Schedules Builder questionnaire is submitted. Firms read this draft page by page with the debtor at the signing appointment, so anything left out of it is not reviewed with the client. The matrix is appended as the final pages:

- It is added at the end, so the page numbering of everything before it is unchanged and signature pages fall where they did before.
- It is treated as a review page, not a page requiring a signature — the debtor reads it, but is not asked to sign it.
- If the matrix cannot be generated for some reason, the draft is still produced without it rather than failing outright. If a draft comes out with no matrix at the end, generate it again.
- This applies to the draft only. The petition compiled for filing does not include the matrix in its pages — the matrix is filed as its own document in the packet.

## Edge Cases & Limitations

- The on-screen Master Creditor List keeps the order rows were added; only the generated Schedules D and E/F are alphabetized.
- The **others to be notified** lists on Schedule D and Schedule E/F are not sorted.

## Related Features

- [Questionnaires](../README.md)
- [Schedule Tools](./README.md)
- [Working With Lists](../filling-out/working-with-lists.md)
- [Schedule A/B Property](./property.md) — liens and collateral
- [Means Test](./means-test.md) — secured debt deductions
- [Generating a Draft Petition](../petition/draft-petition.md)
- [Electronic Court Filing](../../../integrations/efiling/README.md)
- [Case Management](../../../back-office/case-management.md)
