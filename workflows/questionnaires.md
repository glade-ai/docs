# Questionnaires

## Overview

Questionnaires are structured forms that collect information from clients as part of a workflow. Your team defines questionnaire templates with sections and fields, and clients fill them out through the client portal. Responses can auto-populate PDF court forms and legal documents, and feed data into downstream workflow steps.

Glade's native questionnaire system supports template versioning, field-level validation, conditional logic, linked fields, PDF fill mappings, AI-assisted autofills, and real-time sync as clients complete forms.

## Creating and Editing Templates

### Template Basics

A questionnaire template defines the structure of a form. Each template has a name, version, status (draft, current, or abandoned), label, and optional description. Templates are scoped to your firm.

When a template is updated, a new version is created. The current version is what new questionnaire instances are created from. Old versions become abandoned.

### Sections

Sections organize fields within a questionnaire. Each section has a label, optional description, optional tutorial video link, and optional subsections. Sections can be conditionally shown or hidden based on the client's answers to other fields.

### Fields

Fields define individual form inputs. Each field belongs to a section and has properties including label, type, required flag, placeholder, hint, validation rules, options (for select fields), and display configuration.

Supported field types include: short text, long text, numeric, number, currency, date, phone number, SSN, name, US address, international address, single select, multi-select, list, table, percent, and domain-specific types like creditor select, court division select, bankruptcy statute select, and median income.

Currency fields support a **Default to blank** setting in the template editor. When enabled, the field starts empty instead of showing $0.00 when first loaded. This is useful for optional amounts where a $0.00 default would be misleading.

### Field Validation

Fields support validation rules including minimum and maximum values, minimum and maximum lengths, patterns, required status, and custom validators (for example, age validation).

When a field fails validation, the field itself is visually highlighted — input borders, checkboxes, radio buttons, and date pickers change to indicate the error — and an error message appears below the field. This applies to all field types including short text, long text, date, address, and select fields.

### Field Options

Select-type fields define their options as a list of choices, each with a label, key, default flag, and optional PDF fill key.

### Conditional Visibility

Sections and fields can be dynamically shown or hidden based on the values of other fields. Conditions use an expression system with variables that reference other fields or external data.

### Linked Fields

Linked fields let one field's value automatically propagate to another field within or across sections, keeping data synchronized. Changes propagate in real time as clients fill out the form.

### Referenced Lists

Fields can reference other list fields to create cross-references between data sets. For example, a creditor select field can reference a creditor list so clients choose from items they have already entered.

When you choose a creditor from a referenced creditor list — for example, in the SOFA Part 3 "creditors paid over $600" selection or other creditor dropdowns — each option is identified by the creditor's **account number** underneath the name. This makes creditors that share a name distinguishable: a client with several accounts at the same bank shows one option per account number, instead of several identical-looking entries labeled with an internal identifier. Referenced lists other than creditors are unaffected.

### Table Columns

List fields can be displayed in table view. Table columns have settings for editability and visibility, controlling how the data appears and whether clients can modify values inline. The "Visible in table view" setting is available for all fields within a list, including fields nested inside explanation sections at any depth.

Table columns are sortable. Currency and percent columns sort by their numeric value; date columns sort chronologically. This means sorting a currency column orders rows from lowest to highest dollar amount (or vice versa), not alphabetically by the displayed text. Sort order is preserved when you switch between the default view and full screen view — sorting a column in full screen keeps that ordering when you return to the standard view.

### PDF Fill Mappings

PDF fill mappings connect questionnaire fields to PDF template fields, enabling automatic generation of filled court forms and legal documents from questionnaire responses. Individual fields connect to specific PDF fields, and each section can reference a PDF template.

Dynamic PDF templates support generated PDFs with custom layouts and assets, going beyond simple field-to-field mapping.

### Autofills

Autofills populate field values from external data sources, AI inference, or computed expressions. AI autofills allow AI to infer field values from uploaded documents or prior responses.

### Assignees

Assignees can be configured at the field level and at the questionnaire level, controlling which team members are responsible for specific fields or the entire questionnaire.

### Tags

Tags on questionnaire templates allow categorization with label/slug pairs.

### Inheritance Scheme

The inheritance scheme controls whether new questionnaires pre-fill values from previously completed submissions for the same template:

- **None**: No pre-filling.
- **Firm-wide**: Inherits from any prior submission by your firm.
- **Per-client**: Inherits only from the same client's prior submissions.

### Followup Reminders

Followup reminders configure automated reminders (frequency in minutes, hours, days, or weeks) for incomplete questionnaires.

### Review Workflow

A review workflow can be enabled on the template so that a questionnaire goes to "submitted for review" before being marked complete. Reviewers from your team are assigned to handle the review.

### AI Summary

An AI summary can be enabled to generate a summary of the questionnaire responses after completion. The summary voice (tone) is customizable.

### Other Settings

- A **require all fields** setting controls whether all required fields must be filled before the questionnaire can be completed.
- A questionnaire can be marked as generating a case document, which enables PDF generation from the questionnaire data.
- The form provider can be set to Glade's native system, Typeform, or Anvil.

## Using Questionnaires

### Statuses

Questionnaires progress through statuses: **in progress**, **submitted for review** (if review workflow is enabled), **completed**, and **skipped**.

### Filling Out Forms

When using Glade's native form provider, initial values can be pre-populated from field mappings tied to the client's workflow or from the inheritance scheme. Clients fill out sections and fields through the client portal, with changes auto-saved and synced in real time.

When two people edit the same questionnaire at the same time — for example, a client and a paralegal, or an attorney working alongside an AI autofill — each person's edits to different fields are preserved. If two edits target the same field, the newer value wins and the older one is discarded silently rather than producing a save error. Edits to other fields in the same save attempt still go through.

When a list row is deleted, the values inside the row are deleted along with it. Restoring the row from **Removed Items** brings the inner field values back as they were.

Response history tracks when responses are modified, supporting undo and audit.

Default options on single-select fields (configured in the questionnaire template) are automatically applied and saved when the questionnaire first loads. These defaults count as valid answers during validation — a field with a pre-set default is not flagged as incomplete.

A field inside a list can also be given a default **value** in the template, which is filled in automatically each time a new row is added. For example, on bankruptcy Schedule A/B a new property row can default the **% of asset owned by the debtor** to 100% — the common case for individual filers — so your team does not re-enter it on every property. The default applies only to newly-added rows; existing rows keep their values. The seeded value is saved with the row, so it persists after you save, and you can change it before or after saving.

### Phone Number Fields

Phone number fields default to the United States and format as the client types. A US number entered as `2125551234` displays as `+1 212-555-1234` — the country code, the area code, and dashes appear automatically without the client having to type them. Partial numbers format progressively, so `212` shows as `+1 212-` and `212555` as `+1 212-555-`, making it easy to tell at a glance how much of the number is filled in.

The country selector next to the input is still available for international clients. Selecting a different country switches the formatting to that country's convention and updates the country code prefix.

### Currency Field Behavior

By default, currency fields show $0.00 on first load. You can delete the value to leave the field blank — it stays blank after saving rather than resetting to $0.00. An empty currency value is treated as intentionally unset, distinct from a $0.00 value.

If the questionnaire template has **Default to blank** enabled for a currency field, that field starts empty rather than showing $0.00. Enabling or disabling this setting is done in the questionnaire template editor by your firm's template administrator.

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
- Deleted list rows are accessible via the **Removed Items** option on the list field. Only rows that had at least one field filled in appear in Removed Items — completely empty rows are not shown. Rows can be restored from this panel.

### Selecting and Removing List Rows

When a list row has duplicate sub-rows (for example, a creditor that appears on more than one schedule), selecting the parent row automatically selects its indented duplicates so they are removed together.

The **Remove X selected** button in the list footer counts only the real items you picked, not the duplicates that were auto-selected along with them. Selecting one creditor that has two duplicates reads **Remove 1 selected**, not "Remove 3 selected." Removing still deletes the parent row and its duplicates together — only the displayed count excludes the duplicates.

### Importing List Data from Another Questionnaire

List fields can be populated from a client's other questionnaire using **Import from client questionnaire**. When you import:

- Every cell on each imported row is saved, including cells whose value matches the row that was previously in that position. Imported rows no longer come back partially empty after a reload.
- Re-importing before the page has refreshed does not create duplicate rows. The rows from the first import are replaced rather than stacked on top of, so the list reflects the latest import instead of doubling up.
- Whether you import manually or a list is pre-filled automatically from another questionnaire on the same case, the copied rows stay linked to the same case record entity as their source rows. Imported assets, creditors, and other list items appear in case data and update the existing entity instead of creating a duplicate — so copying a property or creditor list no longer produces a second set of entities on the case.
- After importing, rows keep their correct positions and values when the page refreshes, instead of showing blank leading rows.

### Resource Panel

The resource panel appears on the right side of the form and displays supplementary information and tools while you work — including autofill explanations, tutorial videos, reference data, and the Exemptions Calculator. All such content opens in the panel rather than as a separate popup dialog.

The panel scrolls independently of the questionnaire content. Scrolling through the form does not move the resource panel, and scrolling the panel does not move the form.

### Chapter 13 Plan Calculator

On Chapter 13 questionnaires, a **Plan Calculator** button appears in the questionnaire header toolbar. Clicking it opens the Chapter 13 Plan Calculator in a new tab, pre-loaded with the current case. The calculator lets you model plan payments, trustee fees, creditor treatments, and liquidation analysis without leaving your workflow.

> TODO: Confirm exact tab behavior and whether feature-flag gating is still in place once the calculator is fully released.

### Source Data Access

While filling out certain forms (for example, Bankruptcy Schedules), a **Source Data** dropdown lets you reference related data without leaving the form. For bankruptcy workflows that include an Income Organizer, an **Income Organizer** option appears in the dropdown — clicking it opens the Income Organizer in a new tab with the table view already expanded, so you can review income figures alongside the schedules form. The option only appears when the workflow has an associated Income Organizer.

The questionnaire content and the resource panel scroll independently — scrolling through a long questionnaire does not affect the position of the resource panel, and vice versa.

### Exemptions Calculator

When working on bankruptcy Schedule A/B, Schedule C, or the Master Creditor List, an **Exemptions Calculator** panel is available alongside the questionnaire. The panel shows how exemptions apply to the properties and assets you have entered.

On Schedule C, the homestead exemption question ("Are you claiming a homestead exemption of more than $214,000?") is automatically answered based on the client's total real estate value minus total secured liabilities from Schedule D. The field updates as those values change — no manual entry is needed.

The panel has two tabs:

- **By Property**: Groups properties by category in collapsible cards. Each property shows the exemptions claimed against it as labeled pills with statute citations. Status banners indicate whether remaining exemption capacity is available (shown in purple), the exemption is fully utilized (shown in green), or the claimed amount exceeds the allowed limit (shown as a warning).
- **By Exemption**: Groups entries by statute, with each exemption card collapsible to show the properties it covers and the amounts applied to each.

Both tabs include **Expand All** and **Collapse All** controls. A **Only show non-exempt** toggle filters the view to items with non-exempt value remaining.

An **Exemptions Summary** card at the top of the panel shows the total exempted and non-exempt amounts across all properties.

When viewing from Schedule A/B, property names are clickable links that navigate to that property's entry. When viewing from Schedule C, those links are hidden.

### Autofill Status Indicators

Fields populated by autofill show a status indicator so you can see where the value came from and whether it is current:

- **Synced** — The field value matches the source data. Shown with a green checkmark (or the Glade AI icon for AI-sourced values).
- **Out of sync** — The source data has changed since the field was last filled. Shown with an amber warning icon. You can re-run the autofill to update the value.
- **Error** — The autofill encountered a problem and could not set the value. Shown with a red warning icon and a re-run button.
- **Edited** — You have manually changed the value after it was autofilled. Shown with a violet pencil icon and a re-run button if you want to restore the autofilled value.
- **Not yet run** — The autofill has not been applied yet. Shown as a blue **Import Autofill** pill. Click it to trigger the autofill.

### AI Autofills

When an AI agent autofills a group of related fields (for example, property exemptions in a bankruptcy case), re-running the agent preserves any values you have already entered or confirmed. The agent incorporates existing data rather than overwriting it, so you can re-run an analysis after adding new items without losing prior work.

Manual edits to fields in a list also stick when the AI auto-runs after rows have been added, removed, or reordered. For example, on the Bankruptcy Schedules questionnaire, the schedule classifier may run repeatedly as the form changes — moving a creditor from Schedule D to Schedule F by hand will not be reverted by a later automatic run.

Each autofilled field shows a status indicator describing its current state:

- **Synced with [source]** — the autofilled value is current and up to date with the source data.
- **Import Autofill** — the autofill has not run yet. Click the pill to trigger it immediately.
- **Edited** — the field value was manually changed after autofill. A re-run button lets you re-apply the autofill if needed.
- **Out of sync** — the source data has changed and the autofilled value may be stale. Re-run to update.
- **Error** — the autofill encountered an error. A re-run button lets you try again.

### Chapter 13 Plan Calculator

On Chapter 13 questionnaires, a **Plan Calculator** button appears in the form header. Clicking it opens the Chapter 13 Plan Calculator in a new tab alongside the questionnaire. The calculator uses case data to help attorneys analyze payment structures, classify claims, and prepare the repayment plan without leaving the questionnaire workflow.

The Plan Calculator button only appears on questionnaires identified as Chapter 13. If the button is not visible on a Chapter 13 questionnaire, contact support to confirm the feature is enabled for your firm.

### Non-Consumer Chapter 7 Means Test

Some Chapter 7 cases are non-consumer debt cases — the debtor's debts are primarily business rather than consumer in nature. Those cases follow the "no presumption of abuse" branch of Form B122A-1 (line 14a) and never need Form B122A-2 (the full means test calculation).

When the client's questionnaire indicates the case is non-consumer Chapter 7, Glade handles the means test paperwork automatically:

- The Form B122A-1 "no presumption" answer is filled in for the client. No manual entry is needed.
- The B122A-2 means test answers are skipped. Auto-fills that would have populated B122A-2 fields are blocked, so your team does not have to wipe them before filing.
- The B122A-2 PDF is not generated for the case, and any previously generated copy is removed from the case documents. Form B122A-1 (and the B122A-1 Supplement, where the district requires it) continue to be generated.

If a case was set up before this automation rolled out, your firm can request a one-time cleanup of existing non-consumer Chapter 7 cases — contact Glade support to coordinate.

### Case Data Sync Fields

Some questionnaire fields are linked to case data — they display a value pulled from the case record rather than a standalone response. These fields show the synced value by default.

When you edit a case data sync field, the updated value saves automatically and syncs to the case record immediately — no extra confirmation step is required.

### Entity-Bound List Fields

Some list and table fields are linked directly to case entities such as creditors or assets. When a questionnaire has this binding configured, adding, editing, or removing rows in those lists updates the corresponding case entities.

- When a firm team member removes a row from an entity-bound list, the corresponding entity (creditor or asset) is deleted from the case record immediately.
- When a client removes a row, the deletion is held for team review rather than applied immediately. A team member must approve the change before the entity is removed from the case record.
- Writes (adding and editing rows) follow the same case data sync behavior as other synced fields.

### Adding Creditors

The add-creditor flow in bankruptcy questionnaires is optimized to keep firms with large saved-creditor lists fast and to reduce manual schedule selection.

- Adding a creditor from the **Schedule E** tab defaults the new row's schedule to Schedule E. Adding from the **Schedule F** tab defaults to Schedule F. You can still change the schedule before saving, but the default matches the tab you're working from so the row lands on the right schedule without a manual pick.
- The saved-creditor search appears at the top of the add-creditor dialog (above the schedule selector), labeled with a magnifying-glass icon and a **Search for a creditor** placeholder. It lets you reuse a creditor your firm has previously saved instead of re-entering details.
- The saved-creditor search shows up to **100 matches** at a time. When more matches exist, a "Showing first 100 matches. Keep typing to narrow results." line appears at the bottom of the list — keep typing the creditor's name to narrow the result set. This keeps the dialog responsive for firms with tens of thousands of saved creditors.
- Saving a creditor row shows a **"Creditor saved successfully"** toast so you have explicit confirmation the row was written. If you save a row with required fields still missing, the confirmation prompt reads **"Item incomplete. Save anyway?"** — confirming saves the row in its incomplete state for you to come back to later.

### Mobile Experience

Clients filling out questionnaires on a mobile device see a redesigned navigation built for smaller screens:

- A **bottom navigation bar** provides four tabs:
  - **Overview** — shows the questionnaire's overall completion status
  - **Sections** — lists all sections so you can jump directly to any part of the form; includes filtering to narrow by section or progress
  - **Workflow** — shows the client's broader workflow timeline and step progress
  - **Help** — provides access to help resources and tutorials
- A **persistent action bar** at the bottom of each section keeps the save and continue button visible as you scroll, so you never need to scroll back to the top to advance.
- A **close affordance** lets clients dismiss the questionnaire and return to it later without losing progress.
- Clients can switch between questionnaires assigned to the same workflow directly from the mobile navigation, without returning to the home screen.

The mobile layout is only visible to clients accessing the questionnaire on a mobile device. Attorneys and firm staff viewing the same questionnaire on desktop see the standard layout.

### Access Control

If you navigate to a questionnaire you are not assigned to and are not a member of the firm it belongs to, you see a "You don't have access to this questionnaire" screen. This applies to direct links shared by others — opening the link shows the access denied message rather than an error.

### Submitting with Incomplete Fields

When you click **Submit Questionnaire** and required fields are missing, a **Fields Need Attention** dialog opens immediately. The dialog shows how many fields are incomplete and which sections they are in (up to five sections are listed by their position in the form, with a count of any additional). The dialog only lists sections with errors that are currently visible and actionable — sections whose errors only come from hidden or non-actionable fields are not flagged, so completed sections no longer appear in the dialog as needing attention. Submission is only blocked when at least one visible, actionable error remains. You must check the acknowledgment checkbox before the **Submit Anyway** button becomes active. Clicking **Submit Anyway** bypasses validation and submits the form — useful when a field is not applicable to a particular client and cannot be left blank under normal validation rules. Clicking **Continue Editing** closes the dialog and leaves the questionnaire open for further editing. If you complete all incomplete fields before clicking Submit again, the form submits directly without the dialog appearing.

When a questionnaire is submitted this way, an entry is recorded in the workflow activity timeline showing the questionnaire name and the number of required fields that were left unanswered. This gives your team a full audit trail of bypass submissions.

**Submit Anyway** is also available when a required signature has been skipped — you can submit the questionnaire without completing the signature.

When the signature confirmation modal appears at submission time, you have three choices:

- **Sign** — apply or confirm the signature and submit.
- **Skip** — submit while keeping any signature values that were already entered in the questionnaire. Use this when you have manually typed signatures earlier and want them preserved on the saved draft or PDF.
- **Clear & Submit** — clear every signature field on the questionnaire (including signatures inside list and table rows) and then submit. Use this when you are saving the questionnaire as a draft for client review and the draft should not show any signatures or signing dates.

When a questionnaire is submitted using Submit Anyway, the workflow activity timeline records an entry showing that the questionnaire was submitted with the number of fields left unanswered. This lets your team see at a glance which submissions bypassed validation and how many fields were incomplete at the time.

### Concurrent Edits to List Rows

Questionnaires can be open in multiple browser sessions at once — for example, a paralegal and an attorney reviewing the same form, or one user editing the form while a teammate imports data into a list field. List and table rows are now preserved across those concurrent saves:

- A row added by one user is not silently deleted when another user saves a stale view of the same list. Rows are only removed when someone explicitly deletes them, not because they were missing from another session's payload.
- When two sessions update the same list in different orders (for example, one user sorts while another edits a specific row), real-time sync applies each update to the correct row by identity rather than by its position in the list — edits land where they should even when the row order has shifted.
- When a user deletes a row locally and a concurrent update for that same row arrives from another session before the delete has finished syncing, the deleted row stays gone rather than reappearing in the form.
- Bulk list replacements that happen automatically — such as **Import from client questionnaire**, **Populate from credit report**, the Income Organizer pull, and Case Data populate flows — now correctly delete the rows that were replaced, instead of leaving orphaned rows in the database that would re-appear later.
- Deleting an item from a deduplicated list — for example, removing a creditor from the Bankruptcy Schedules Master Creditor List — now also removes the hidden duplicate entries grouped under it. Previously those duplicates were left behind and one would resurface as a visible row after the form reloaded, so a creditor you had just deleted appeared to come back. The removed creditor now stays gone after a refresh.
- Deletions made in a linked list (a list that mirrors another list) now save reliably. Previously a row removed from a linked list could be silently ignored and reappear after reloading.

### Outdated Template Upgrade Prompt

If you try to save responses on a questionnaire whose template version is no longer accepting changes, a modal appears explaining that the template has been updated. The modal includes an **Upgrade Questionnaire** button that moves the questionnaire onto the current template version and reloads it so you can continue editing. Until you upgrade, saves on the old version are blocked.

### Re-opening

Questionnaires can be re-opened with a message explaining why, returning them to "in progress" status.

### Collaborators

Collaborators (additional team members) can be assigned to questionnaires with view or edit permissions.

### Completion

When a questionnaire is completed, it triggers downstream workflow steps, updates case data, generates compiled documents, creates tasks, and sends notifications.

When a questionnaire generates multiple documents — for example, filled court forms alongside supplemental documents such as a creditor matrix — the documents appear in the case document list in a consistent order: filled court forms first, followed by other questionnaire-generated documents. This ordering is maintained even when new sections are added to the questionnaire after some documents have already been created.

## Edge Cases & Limitations

- Typeform and Anvil providers are supported, but Glade's native provider is the primary path. Typeform questionnaires redirect clients to an external URL. Auto-complete is only supported for the Anvil provider.
- When upgrading a questionnaire to a new template version, responses are copied from the old instance. Pre-filled initial values are not re-applied during the upgrade.
- List fields that use referenced lists depend on both the referencing and referenced fields existing in the same questionnaire template.
- List fields that are linked as destinations — populated automatically from another list in the questionnaire at filing time (for example, Schedule D Creditors mirroring the Creditors list) — are not counted as incomplete during validation. Only the source list needs to be filled.
- Deduplication of list items is available but requires specifying the field.
- Linked destination list fields (for example, a Schedule D creditors list that auto-populates from a master creditor list) are not independently validated. Completing the source list is sufficient — the destination list does not need to be filled out separately.
- Clearing a required date field and saving leaves the field in an invalid state — it is treated as empty, not as a valid cleared value, so validation correctly flags it as required.
- When using "Autofill from Glade questionnaire" on a list field, date entries that contain only a descriptive placeholder (no actual date value) are skipped — the destination date field is left blank rather than filled with invalid text. You can fill these fields manually after autofill completes.
- Editing a table row and saving preserves all column data. Columns are not dropped or lost when a row is saved after being edited.
- Case data sync only writes to questionnaires that are still in progress. Once a questionnaire is submitted, submitted for review, snapshotted, or otherwise past the in-progress stage, incoming case data updates no longer modify its responses — completed work is preserved as it was at submission. Add or edit data on an in-progress questionnaire (or re-open a submitted one) to apply new values from the case record.
- When more than one questionnaire on the same case can sync case data — for example, the client questionnaire and the schedules questionnaire — each one syncs independently. Starting or initiating a second questionnaire does not turn off syncing on another that is still in progress: both keep syncing while open. A questionnaire stops syncing only when it is itself submitted, not when a sibling questionnaire is created.

## Related Features

- [Client Portal](../intake/client-portal.md)
- [Document Collection](./document-collection.md)

