# Working With Lists

## Overview

List-type fields — creditors, properties, income sources, and similar — hold one row per entry. This page covers opening and editing a row, selecting and removing rows, restoring removed rows, and how rows are kept intact when several people edit a list at once or rows have been deleted.

## Key Behaviors

### List Row Detail Views

List-type fields allow you to click into individual rows to view or edit details:

- When you open a row, the page link updates so you can share it directly — anyone who opens that link sees the same row's details immediately.
- Required sub-fields in each row are validated individually. Rows with missing required fields show a red dot indicator.
- The section's error badge count includes errors from incomplete list rows and table cells, in the same way it counts errors from other field types. Error badges always appear on the source list section — for example, errors in a property list appear under "Property (Real & Personal)", not under a derived section like "Schedule D Creditors". Completing required fields in a row reduces the section count; clearing them increases it. Deleted rows (rows that have been removed to the Removed Items panel) are excluded from the error count — only active, non-deleted rows are included. Error badge counts update when the questionnaire is submitted, not in real time as fields are edited. After saving a list row, any validation errors that were shown for that row clear immediately — the error count reflects only fields that are currently incomplete in active rows. When error counts change (for example, after a row is saved or a field is corrected), the badge count animates to its new value. Section sidebar navigation and subsection tab badges display error counts in amber.
- When a list row has validation errors, each subsection tab in the detail view (for example, **Details** or **Exemptions**) shows an error count badge so you can navigate directly to the tab with missing required fields. An error summary popover is also available within the row detail view — it lists the specific fields that need attention, and clicking any item jumps directly to that field.
- When editing a row in the detail view and the questionnaire requires all fields to be complete, saving highlights any incomplete required fields and prompts you to confirm before saving with incomplete data. This prompt also appears if you clear a required field that previously had a value. On questionnaires that do not require completion, saving always proceeds without a prompt. Fields that are hidden by conditional logic are not considered incomplete and do not trigger the prompt.
- When a list row references items in another section (for example, an exemption row linked to a property), the detail header shows the parent item's name as context so you always know which item you are editing.
- A **Save & Next** button saves the current row and opens the next row immediately — no need to return to the full list between edits. **Previous** and **Next** buttons let you move between rows; if you have unsaved changes, you will be prompted before switching.
- The Save button shows a loading indicator while the save is in progress. After saving, the view returns to the full list.
- Deleted list rows are accessible via the **Removed Items** option on the list field. Only rows that had at least one field filled in appear in Removed Items — completely empty rows are not shown. Rows can be restored from this panel; see [Restoring Removed List Items](#restoring-removed-list-items).

### Selecting and Removing List Rows

When a list row has duplicate sub-rows (for example, a creditor that appears on more than one schedule), selecting the parent row automatically selects its indented duplicates so they are removed together.

The **Remove X selected** button in the list footer counts only the real items you picked, not the duplicates that were auto-selected along with them. Selecting one creditor that has two duplicates reads **Remove 1 selected**, not "Remove 3 selected." Removing still deletes the parent row and its duplicates together — only the displayed count excludes the duplicates.

**Add Item starts a blank row.** Removing a row and then clicking **Add Item** straight away gives you an empty row to fill in. For a period, the new row could open pre-filled with another row's answers — most noticeable on the property lists, where a freshly added item arrived carrying a neighbouring item's details. Rows that shifted position because of the removal also load their own answers rather than the answers of the row that used to sit in that place.

When a list row is deleted, the values inside the row are deleted along with it. Restoring the row from **Removed Items** brings the inner field values back as they were.

### Restoring Removed List Items

Rows removed from a list are kept under **Removed Items** on the list field and can be put back from there. Restoring a row returns the original row rather than re-entering its values as a new one:

- The row keeps the place it had in the list, so a list your team has sorted comes back in the order you left it.
- If the row was marked as a duplicate of another creditor, or had duplicates grouped under it, those links come back with it. Restoring no longer costs your team the deduplication work they had already done.
- The row stays attached to the creditor, asset, or other case record it was already linked to, instead of creating a second, near-empty copy of it on the case.
- Only rows that had at least one field filled in appear in Removed Items — completely empty rows are not shown.

Previously a restore re-added the values as brand-new rows. On a master creditor list that had been deduplicated and sorted, restoring meant the duplicate links and the sort order were gone and the case record picked up a set of near-empty creditors alongside the real ones — hours of re-work on a large list.

> Restoring a row whose case record entry was deleted at the same time brings the questionnaire row back but leaves that entry deleted until the row is next edited. If a restored creditor or asset is missing from the case record, open the row and save it.

### Concurrent Edits to List Rows

Questionnaires can be open in multiple browser sessions at once — for example, a paralegal and an attorney reviewing the same form, or one user editing the form while a teammate imports data into a list field. List and table rows are now preserved across those concurrent saves:

- A row added by one user is not silently deleted when another user saves a stale view of the same list. Rows are only removed when someone explicitly deletes them, not because they were missing from another session's payload.
- When two sessions update the same list in different orders (for example, one user sorts while another edits a specific row), real-time sync applies each update to the correct row by identity rather than by its position in the list — edits land where they should even when the row order has shifted.
- When a user deletes a row locally and a concurrent update for that same row arrives from another session before the delete has finished syncing, the deleted row stays gone rather than reappearing in the form.
- Bulk list replacements that happen automatically — the Income Organizer pull and case data populate flows, for example — correctly delete the rows that were replaced, instead of leaving orphaned rows behind that would re-appear later.
- Deleting an item from a deduplicated list — for example, removing a creditor from the Bankruptcy Schedules Master Creditor List — now also removes the hidden duplicate entries grouped under it. Previously those duplicates were left behind and one would resurface as a visible row after the form reloaded, so a creditor you had just deleted appeared to come back. The removed creditor now stays gone after a refresh.
- Deletions made in a linked list (a list that mirrors another list) now save reliably. Previously a row removed from a linked list could be silently ignored and reappear after reloading.

### Lists That Have Had Rows Deleted

Deleting a row from a list leaves a gap in the list's stored ordering, and on a long list those gaps could break the form outright. Opening an affected bankruptcy schedules questionnaire and then opening a creditor row's detail tabs — the **Collateral** tab on a Schedule D creditor was the reported case — or clicking **Add item** replaced the whole questionnaire with a full-page error, with no way forward but to reload the page.

- Lists are now rebuilt without the gaps. Every row is kept, in the same order and with the same values — nothing is added, removed, or reordered.
- **Attribution on the rows after a deleted row is correct.** "Last edited" and the source badge on each row could previously read the details of a neighbouring row on any list where something had been deleted. That also let an autofill overwrite an answer someone had typed, because the form was reading the wrong row's history when deciding whether the value was hand-entered.
- Petition Check findings on a list point at the row they belong to rather than at a nearby one, and a finding is no longer dropped from the results because the row it belonged to had shifted.
- **Table columns are unaffected.** A table's columns keep their own positions, and an untouched column stays empty rather than sliding data under a different column heading.
- A questionnaire in this state tidies its own stored ordering the first time anyone saves it, so an affected case stops being affected as soon as your team edits it.

## Edge Cases & Limitations

- Editing a table row and saving preserves all column data. Columns are not dropped or lost when a row is saved after being edited.
- Removing a row from an entity-bound list can delete the matching creditor or asset from the case record — see [Case Data Sync](../case-data/case-data-sync.md#entity-bound-list-fields).

## Related Features

- [Questionnaires](../README.md)
- [Filling Out Questionnaires](./README.md)
- [Fields, Lists, and Tables](../templates/fields-and-tables.md)
- [Creditors](../schedules/creditors.md)
- [Case Data Sync](../case-data/case-data-sync.md)
- [Manual Overrides](../autofills/manual-overrides.md)
