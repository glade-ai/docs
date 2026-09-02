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

Supported field types include: short text, long text, numeric, number, currency, date, phone number, SSN, name, US address, international address, single select, multi-select, list, table, percent, and domain-specific types like creditor select, court division select, bankruptcy statute select, median income, and means test summary.

The **means test summary** field is a read-only display field rather than an input. Instead of collecting an answer from the client, it shows a consolidated summary of the case's means test information. A single field type serves all four Means Test forms — the Chapter 7 forms (B122A-1 and B122A-2) and the Chapter 13 forms (B122C-1 and B122C-2) — and displays the summary appropriate to the form it appears on.

Currency fields support a **Default to blank** setting in the template editor. When enabled, the field starts empty instead of showing $0.00 when first loaded. This is useful for optional amounts where a $0.00 default would be misleading.

### Field Validation

Fields support validation rules including minimum and maximum values, minimum and maximum lengths, patterns, required status, and custom validators (for example, age validation).

When a field fails validation, the field itself is visually highlighted — input borders, checkboxes, radio buttons, and date pickers change to indicate the error — and an error message appears below the field. This applies to all field types including short text, long text, date, address, and select fields.

Dropdown fields follow the same layout as every other field type: the label turns red, the box is outlined, and the message appears once, below the box. Previously a dropdown such as **District of:** printed its message twice — once above the box and once below — while the field beside it showed a single message underneath, so the same error looked different on two adjacent fields.

#### Validation rules on a cell of a table or list

Your firm's template administrator can write validation rules that check one field against another across the form. A rule can now be anchored on a **cell inside a table or a list** — for example, Form 122A-1 line 5 for Debtor 1 — rather than only on a standalone field.

- These rules previously did not run at all. A rule anchored on a cell was skipped silently: it was switched on, it appeared in the rule list, and it never produced a finding. If your firm wrote rules against a table cell and never saw them fire, that is why.
- **A rule is checked once per column of a table, or once per row of a list**, and each column or row that fails produces its own finding pointing at that cell. On a joint case, a rule on a two-debtor table is checked for both debtors.
- **A column that nobody has filled in is still checked.** A table column left untouched is a real column with unanswered cells, not an absent one.
- A rule can be narrowed to a **single column** where it is only meant to apply to one debtor.
- Where a rule is written incorrectly — it points at a cell that cannot be found, for example — that is reported once against the rule itself rather than repeated on every row.

Because a rule written for one debtor is otherwise checked against both, a rule that means "at least one debtor" needs to be either narrowed to a column or rewritten to ask the question once across the whole table. Otherwise a joint case where only one debtor runs a business can raise a blocking finding on the other debtor's column that nobody can clear.

> TODO: Confirm which rules your firm's templates ship with this enabled, and where a rule is narrowed to a single column in the template editor. The set of rules switched on at release was still being reviewed rule by rule.

#### When a rule's answers have not been given yet

A rule that compares fields cannot reach a verdict until the fields it reads have been answered. Where one of them is still blank, Glade reports the blank rather than the comparison:

- The rule's own message is withheld, and a finding reading **Needed to check '<field name>'** appears on the blank field instead, carrying the rule's severity. The finding names the field the rule is anchored on, so it is clear which check is waiting.
- The finding sits on the field that needs the answer, which is the one you can act on — not on the field the rule reports against.
- Once the blank field is answered, the finding clears and the rule is evaluated normally, raising its own message only if the answers genuinely disagree.

Previously a rule fired its full message as soon as one of its inputs was blank — telling a filer their answers contradicted each other before they had given one of the answers. Working down a long form produced a run of contradiction warnings that cleared themselves as the filer caught up.

**Not every blank means "not answered yet".** Your firm's template administrator can mark an individual field a rule reads as one that is allowed to be blank, so the rule is evaluated with the blank treated as nothing rather than as a missing answer. The distinction is between an amount that is blank because there is none — no income of that kind, a column a single filer does not have — and an answer that is blank because the filer has not reached it. The setting is per field per rule, so the same field can be required in one rule and optional in another.

### Field Options

Select-type fields define their options as a list of choices, each with a label, key, default flag, and optional PDF fill key.

### Conditional Visibility

Sections and fields can be dynamically shown or hidden based on the values of other fields. Conditions use an expression system with variables that reference other fields or external data.

Conditions can be built two ways: a guided builder where you pick a field and a comparison, and an advanced mode where you write the condition yourself.

#### Conditions on currency fields

A currency answer carries more than a number — it also records the currency and whether the amount was marked unknown. A condition built on a currency field now compares the **dollar amount**, which is almost always what the author intends.

- A condition such as "greater than 0" on a currency field works as written. Previously the comparison was made against the whole answer rather than the amount, so it could never be true — a section set to appear when an amount was above zero stayed hidden no matter what the client entered.
- **Existing conditions are left exactly as they are.** The fix applies only to conditions created from now on. Editing a different condition in the same rule does not silently change how an existing currency condition behaves. To pick up the new behavior on a condition built earlier, delete it and add it again.
- **Filled / Not filled reads the amount too**, on conditions created from now on. A currency field holding $0.00 counts as *not filled* under a newly created condition. If you want a rule that fires whenever the client has touched the field at all, including a deliberate $0.00, check the amount rather than using **Filled**.
- Conditions written by hand in advanced mode are unchanged — the amount is not selected for you there, so keep writing those conditions the way you do today.

> TODO: Confirm the in-product names for the guided builder and advanced mode, and whether the guidance above should name the specific controls.

### Linked Fields

Linked fields let one field's value automatically propagate to another field within or across sections, keeping data synchronized. Changes propagate in real time as clients fill out the form.

### Referenced Lists

Fields can reference other list fields to create cross-references between data sets. For example, a creditor select field can reference a creditor list so clients choose from items they have already entered.

When you choose a creditor from a referenced creditor list — for example, in the SOFA Part 3 "creditors paid over $600" selection or other creditor dropdowns — each option is identified by the creditor's **account number** underneath the name. This makes creditors that share a name distinguishable: a client with several accounts at the same bank shows one option per account number, instead of several identical-looking entries labeled with an internal identifier. Referenced lists other than creditors are unaffected.

### Table Columns

List fields can be displayed in table view. Table columns have settings for editability and visibility, controlling how the data appears and whether clients can modify values inline. The "Visible in table view" setting is available for all fields within a list, including fields nested inside explanation sections at any depth.

Table columns are sortable. Currency and percent columns sort by their numeric value; date columns sort chronologically. This means sorting a currency column orders rows from lowest to highest dollar amount (or vice versa), not alphabetically by the displayed text. Sort order is preserved when you switch between the default view and full screen view — sorting a column in full screen keeps that ordering when you return to the standard view.

A list's display toggles — for example **Show duplicates** and **Show zero'd accounts** on the creditor list — are available in full screen view as well as the standard view. They appear in the full screen toolbar and share their setting with the standard view, so a toggle you change in full screen still reflects that state when you exit. Previously these toggles sat underneath the full screen overlay and could not be reached without leaving full screen first.

Dropdowns that list options alphabetically sort without regard to capitalization, so a list of names reads `Aaron, alice, bob, Zack` rather than putting every capitalized entry ahead of the lowercase ones.

### PDF Fill Mappings

PDF fill mappings connect questionnaire fields to PDF template fields, enabling automatic generation of filled court forms and legal documents from questionnaire responses. Individual fields connect to specific PDF fields, and each section can reference a PDF template.

Dynamic PDF templates support generated PDFs with custom layouts and assets, going beyond simple field-to-field mapping.

#### Supplemental and local court forms

Alongside the official bankruptcy forms, Glade can generate supplemental forms that a district requires or that support an answer on an official form. One is newly available:

- **Schedule I line 8a business statement** — the *Financial Review of the Debtor's Business* attachment that supports the business-income line on Schedule I. A section on the questionnaire collects each business's name, its gross receipts, and the twenty official expense lines; total expenses and net income are calculated for you. The generated attachment prints **one page per business**. The section appears only when Schedule I line 8a carries an amount for either debtor — including a business reporting a loss, since a negative figure on line 8a is still business income to disclose.

Three corrections to how that attachment is produced:

- **It stays in the petition packet.** The attachment is no longer dropped when the petition's documents are regenerated. Previously it was removed from the packet on every regeneration, so a firm that had filled the section in could compile the petition and find the statement gone, with nothing on screen to say why.
- **Only real businesses print.** Opening the section pre-renders a set of blank business rows, and every row with anything on it used to produce a page — two businesses could generate a twenty-four-page supplement, twenty-two pages of it near-blank. A row now reaches the attachment only when it has a business name or a gross amount on it.
- **The pages are numbered.** The footer continues the numbering of the form the attachment follows. Because Form 106I is two pages, the first business prints as page 3, the second as page 4, and so on.

These apply to documents generated from here on; re-generate the petition on a case prepared earlier to pick them up.

Equity on the Texas form is worked out per asset before the category is totalled, and never goes below zero, so an asset with liens above its value contributes nothing rather than a negative amount. An exemption claimed at 100% of fair market value is capped at the equity remaining after liens.

The questionnaire fields for the Texas exemptions schedule are labelled with the same wording the printed form uses for its columns — for example **1. Real Estate — Total Encumbrances** and **Totals — Total Amount Non-Exempt**. Earlier labels used internal shorthand such as *— Enc* and *— Gross*, carried a line reference that meant nothing to a filer, and spelled the non-exempt column two different ways, so it was hard to tell which column of the form a field corresponded to. Only the wording changed: answers already recorded are unaffected, and the generated form is unchanged.

Both forms are added to your firm's questionnaire template by Glade rather than switched on in the template editor. Contact support if your firm files in these situations and does not see the section.

> TODO: Confirm which firms and templates these sections have been added to. They are rolled out per firm rather than to everyone at once.

Generated forms paginate by content: a section that runs longer than a single page continues onto the next page. Previously a section was kept together as one block, so anything that no longer fit was pushed whole to the following page — leaving a large blank area at the bottom of the page before it. This was most visible on Schedule A/B, where the residence details plus a long property list pushed the entire section down a page.

#### Business and other interests on Schedule A/B line 19

Line 19 of Schedule A/B asks for the debtor's interests in businesses that are not publicly traded. The generated petition prints the **name recorded on the entry together with the brief description** entered alongside it, on the one line the form provides.

Previously only the name reached the form and the brief description was dropped, so a line that had been filled in on the questionnaire printed as a bare name with no indication of what the interest actually is. Entries with no brief description print the name on its own, as before.

Petitions generated before this change are not rebuilt. Re-generate the petition on a case whose line 19 entries carry a description if the filed copy should show it.

### Autofills

Autofills populate field values from external data sources, AI inference, or computed expressions. AI autofills allow AI to infer field values from uploaded documents or prior responses.

**When an autofill may overwrite an answer.** An answer someone typed by hand is protected — an autofill does not replace it. Two situations are treated as *not yet an answer*, so an autofill fills them:

- **The field is empty.** A field left blank, holding only spaces, or holding an empty value counts as unanswered even if a person was the last to touch it.
- **The field says No and the computed result is Yes.** A Yes/No field answered "No" is upgraded to "Yes" once the data behind it says yes — for example, a Schedule A/B category answered "No" before anything was entered on the Master Property List is upgraded once matching assets are added there.

Both situations previously blocked the autofill for good, so a Schedule A/B category answered early — left blank, or answered "No" — never picked up assets added later and the generated schedule shipped without them. If your team has been re-checking Schedule A/B by hand for assets that failed to carry over, that is no longer necessary. Free text someone has actually written is still never overwritten.

**Combining several rows into one answer.** An autofill that draws from a list can join every matching row into a single answer instead of taking only the first one. This matters on Schedule A/B lines that ask for one brief description covering several items — several tax refunds, or several claims — where previously only the first row's description reached the field and the rest were dropped without any indication. Amounts can be totalled the same way. The joined text carries through to the generated PDF as well, so a schedule that previously printed a single description now prints all of them.

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

### How a submitted questionnaire appears to the client

When a questionnaire uses the review workflow, a client who has submitted it sees it marked **Submitted — under review** with a clock icon, and the "Complete this task" prompt is removed — so the client can tell the questionnaire is already in and does not look like it still needs their attention. Your team's dashboard continues to show "Review required by you" for the same questionnaire.

Anyone with view or edit access who opens a questionnaire that is not currently editable for them — for example, a client opening a questionnaire they have already submitted for review, or a view-only team member opening one that is still in progress — sees the questionnaire's answers in read-only form. Previously some of these combinations showed a "We are generating your form results…" message that never cleared (most noticeably after submitting a questionnaire for review from the client's own profile); that stuck message no longer appears for anyone who has permission to view the questionnaire.

### Filling Out Forms

When using Glade's native form provider, initial values can be pre-populated from field mappings tied to the client's workflow or from the inheritance scheme. Clients fill out sections and fields through the client portal, with changes auto-saved and synced in real time.

When two people edit the same questionnaire at the same time — for example, a client and a paralegal, or an attorney working alongside an AI autofill — each person's edits to different fields are preserved. If two edits target the same field, the newer value wins and the older one is discarded silently rather than producing a save error. Edits to other fields in the same save attempt still go through.

When a list row is deleted, the values inside the row are deleted along with it. Restoring the row from **Removed Items** brings the inner field values back as they were.

Response history tracks when responses are modified, supporting undo and audit.

Default values configured in the questionnaire template are saved automatically when the questionnaire is set up, so a displayed default is recorded as a real answer from the start — even if nobody ever opens the section that contains the field. This covers every kind of field the template can carry a default for, not only single-select options, and it covers the cells of list and table rows that already exist as well as top-level fields.

Because the answer is stored up front:

- A field showing a default counts as answered during validation and is not flagged as incomplete. Previously a filer could see the answer on screen while the Petition Check reported the field as blank.
- The default appears on any generated PDF court form, including checkbox selections such as a **No** answer on the Statement of Financial Affairs. Previously those lines printed blank on a sworn document.

Answers already given are never touched — a default is only written where the field has no answer at all. Questionnaires started as a copy of another questionnaire inherit the original's answers and are not re-defaulted.

> TODO: Confirm what happens to fields a *newer template version* introduces on a questionnaire that is upgraded in place — whether their defaults are written at upgrade time or only once the field is touched.

Template defaults are filled in as the last step of setting up a new questionnaire, after any information Glade already holds on the case has been carried across. A default therefore only ever fills a field that has no answer yet — it never replaces something the case record already knows, so a client's real figure is not shadowed by a template placeholder. Because the defaults are in place before anyone opens the form, the duplicate check that runs on a newly created list sees them too.

A field that starts out at its template default — for example a currency field showing $0.00 — is still eligible for autofill the first time the questionnaire loads. Fields such as the applicable median family income on Chapter 7 Form 122A-1 now populate from the client's state and household size on open, instead of sitting at $0.00 with no indication that anything was missing. Values you have typed yourself are never replaced by this initial pass.

A field inside a list can also be given a default **value** in the template, which is filled in automatically each time a new row is added. For example, on bankruptcy Schedule A/B a new property row can default the **% of asset owned by the debtor** to 100% — the common case for individual filers — so your team does not re-enter it on every property. The default applies only to newly-added rows; existing rows keep their values. The seeded value is saved with the row, so it persists after you save, and you can change it before or after saving.

### Phone Number Fields

Phone number fields default to the United States and format as the client types. A US number entered as `2125551234` displays as `+1 212-555-1234` — the country code, the area code, and dashes appear automatically without the client having to type them. Partial numbers format progressively, so `212` shows as `+1 212-` and `212555` as `+1 212-555-`, making it easy to tell at a glance how much of the number is filled in.

The country selector next to the input is still available for international clients. Selecting a different country switches the formatting to that country's convention and updates the country code prefix.

### Currency Field Behavior

By default, currency fields show $0.00 on first load. You can delete the value to leave the field blank — it stays blank after saving rather than resetting to $0.00. An empty currency value is treated as intentionally unset, distinct from a $0.00 value.

If the questionnaire template has **Default to blank** enabled for a currency field, that field starts empty rather than showing $0.00. Enabling or disabling this setting is done in the questionnaire template editor by your firm's template administrator.

When an autofill fills a currency field but cannot work out an amount, the field is set to **$0.00** rather than being left with no amount at all. Previously a field in this state could print as a blank line on the generated petition — a sworn figure with nothing in it. Anything that represents a deliberate answer is left exactly as it is and is never replaced by the $0.00 default:

- a value marked **Unknown**,
- a value **overridden with text**, and
- an amount you have entered yourself.

### Court Division

The **court division** field lists the divisions belonging to the case's filing district. Where a district has only one division to file in, that division is selected for you when the field is still empty, so the questionnaire is not held up by a choice with only one answer.

- Districts with more than one division still require you to pick one.
- Divisions that exist only as electronic-filing variants of another division are not offered, and divisions that appear more than once in the underlying court list are shown once.
- Auto-selection only fills an empty field. A division you have chosen is never replaced.

### Marking a Value as Unknown

On bankruptcy Schedule A/B, an asset's current value can be marked **Unknown** (or overridden with custom text) instead of a dollar amount. When that value feeds a calculated line — for example, a figure carried onto another line or copied to Schedule C — the calculated line now shows **Unknown** (or the entered text) rather than $0.00. This matches how the value already appears in the answer view, and it carries through to both the live preview and the generated and filed petition. Section and part totals that are meant to stay numeric continue to show a dollar amount.

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

### Importing List Data from Another Questionnaire

**The one-off import actions have been removed.** The questionnaire's overflow menu no longer offers **Import from credit report**, **Import case data**, or **Import from client questionnaire**, and the master and client creditor lists no longer carry an **Import** dropdown.

These actions copied a whole list over the top of the answers already on the form, which is how a schedule an attorney had prepared could revert to older client-supplied data in a single click. The credit report import had additionally stopped working — it reported that no creditors had been imported even on cases whose credit report held them. Case data sync is now the one route by which a credit report, a client questionnaire, or the case record reaches the schedules — it applies changes as they happen and lets you review them first, rather than replacing a list wholesale. See [Case Data Sync Fields](#case-data-sync-fields) and [Reviewing changes before you sync](#reviewing-changes-before-you-sync).

- **Run Deduplicator** is unchanged and still sits on both creditor lists.
- **Pay organizer and income organizer imports are unaffected.** **Import data from pay organizer** still appears on a case that has a pay organizer, and the Means Test section keeps **Import Data from Income Organizer**. Pay organizers are not yet carried by case data sync, so those two are still how income figures reach the schedules.

Lists that are pre-filled automatically from another questionnaire on the same case continue to work as before. The copied rows stay linked to the same case record entity as their source rows, so pre-filled assets, creditors, and other list items update the existing entity in case data instead of creating a duplicate, and they keep their positions and values when the page refreshes.

### Restoring Removed List Items

Rows removed from a list are kept under **Removed Items** on the list field and can be put back from there. Restoring a row returns the original row rather than re-entering its values as a new one:

- The row keeps the place it had in the list, so a list your team has sorted comes back in the order you left it.
- If the row was marked as a duplicate of another creditor, or had duplicates grouped under it, those links come back with it. Restoring no longer costs your team the deduplication work they had already done.
- The row stays attached to the creditor, asset, or other case record it was already linked to, instead of creating a second, near-empty copy of it on the case.
- Only rows that had at least one field filled in appear in Removed Items — completely empty rows are not shown.

Previously a restore re-added the values as brand-new rows. On a master creditor list that had been deduplicated and sorted, restoring meant the duplicate links and the sort order were gone and the case record picked up a set of near-empty creditors alongside the real ones — hours of re-work on a large list.

> Restoring a row whose case record entry was deleted at the same time brings the questionnaire row back but leaves that entry deleted until the row is next edited. If a restored creditor or asset is missing from the case record, open the row and save it.

### Resource Panel

The resource panel appears on the right side of the form and displays supplementary information and tools while you work — including autofill explanations, tutorial videos, reference data, and the Exemptions Calculator. All such content opens in the panel rather than as a separate popup dialog.

The panel scrolls independently of the questionnaire content. Scrolling through the form does not move the resource panel, and scrolling the panel does not move the form.

This now holds for the panel opened with **Show External Data** as well. It stays pinned in view as you work down a long form and scrolls within its own bounds. Previously that panel moved with the page, so it disappeared off the top of the screen as soon as you scrolled past the first few questions — the point at which you are most likely to want to check a figure against it. On a narrow screen the two columns stack and the panel scrolls with the rest of the page, as it always has.

### Chapter 13 Plan Calculator

On Chapter 13 questionnaires, a **Plan Calculator** button appears in the questionnaire header toolbar. Clicking it opens the Chapter 13 Plan Calculator in a new tab, pre-loaded with the current case. The calculator lets you model plan payments, trustee fees, creditor treatments, and liquidation analysis without leaving your workflow.

> TODO: Confirm exact tab behavior and whether feature-flag gating is still in place once the calculator is fully released.

### Source Data Access

While filling out certain forms (for example, Bankruptcy Schedules), a **Source Data** dropdown lets you reference related data without leaving the form. For bankruptcy workflows that include an Income Organizer, an **Income Organizer** option appears in the dropdown — clicking it opens the Income Organizer in a new tab with the table view already expanded, so you can review income figures alongside the schedules form. The option only appears when the workflow has an associated Income Organizer.

The questionnaire content and the resource panel scroll independently — scrolling through a long questionnaire does not affect the position of the resource panel, and vice versa.

### Property Liens on Schedule A/B

On a Schedule A/B property, you can attach more than one lien to the same property. The property's lien field lets you search for and select existing secured creditors from the Master Creditor List, and you can add as many as apply.

- As you select liens, the property's **total claim amount** updates automatically to the sum of the selected creditors' balances.
- A summary below the selector shows the **total liens** (with a count of how many) and the **equity after liens** — the property's value minus the total liens, which never goes below zero.
- The same creditor can't be selected twice on one property: liens already chosen drop out of the remaining choices, and the option to add another lien is disabled once every available lien is selected or while an empty selection is open.
- A selected creditor with a blank or zero balance adds nothing to the total.

The Exemptions Calculator uses the summed total of the selected liens when calculating equity available to exempt. If no liens have been selected for a property, it falls back to the single lien amount entered directly on the property.

### Property Summary

A **Property summary** button on the Schedule A/B property section opens a summary of the case's properties side by side, with each property's value, equity, the exemption claimed against it, and any unexempt amount.

- The **Equity** column is the property's value minus the liens attached to it, and never goes below zero. Previously it showed the property's value before liens — so a residence worth $520,000 against a $519,000 mortgage read as $520,000 of equity, and a vehicle that was fully underwater read as though it had positive equity. The summary now agrees with the lien detail on the property row and with the Exemptions Calculator.
- An exemption claimed at 100% of fair market value claims the equity remaining after liens, not the property's full value.
- The **Unexempt** column never goes below zero. A $15,000 homestead exemption claimed against $1,000 of real equity shows as fully exempt rather than as a negative amount.

If your team reviewed a property summary before this correction, re-check the equity figures on any case with liened property — the corrected figures are lower, and a property that appeared to hold equity may hold none.

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

#### Fields That Both Sync With Case Data and Autofill

Some fields are set up to sync with case data *and* to be populated by an autofill — most of the income lines on Schedule I are in this position, since they are filled from the Income Organizer. On these fields the indicator names the source the current value actually came from:

- A value that came from an autofill reads as populated from that source (for example, **Populated from Internal data**) and keeps its re-run control, so you can refresh it. Clicking the indicator opens the autofill's explanation panel.
- A value that case data genuinely produced still reads **Synced with case data** and opens the case data view, and a value you have typed over still reads **Manually overridden** with the option to revert.

Previously any field with a case data connection claimed to be synced with case data even when something else had filled it, and the re-run control was hidden — so on a Schedule I income line filled from the Income Organizer, there was no way to refresh the value and the stated source was wrong. Where the value is refreshed from and where edits are saved has not changed; only the reported source and the availability of the re-run control.

> TODO: Confirm the in-product wording of the "Populated from Internal data" label — the underlying source name may read differently to a preparer.

#### Overriding a Schedule I or Means Test figure the calculator produced

The Schedule I and Means Test lines the Income Organizer calculates are handled differently from ordinary case data sync fields, because an attorney's correction to one of them needs to survive the next recalculation.

- These fields name the calculator as their source rather than reading **Synced with case data**.
- **A figure you type over sticks.** The field reads **Manually overridden**, and a later Income Organizer recalculation leaves it alone. Previously the most recent recalculation won, so a correction an attorney made could be replaced without warning the next time income figures changed.
- **Re-run is always available on these fields**, whether or not you have edited them. Using it puts the calculator's current output back on the field and hands the line back to the calculator, so a later recalculation updates it again.
- Because these figures are calculated rather than stored on the case record, the re-run control replaces the case data view on them — there is no case record entry behind the line to open.
- Ordinary case data sync fields are unchanged: editing one still leaves it on case data with the usual revert option.

#### Autofills From Reference Data

Some autofills fill a field from reference data Glade already holds for the case rather than from a document or an AI inference — the IRS standard deduction amounts on the Chapter 7 means test (Form 122A-2) are the common example.

These fields populate when you open the questionnaire, with no action needed from you. Previously they arrived empty and only filled in after you triggered them by hand, which was easy to miss and left the means test showing no deductions. You can still re-run one of these autofills at any time to pick up changed case data, and a value you have entered or corrected by hand is not overwritten.

The national standard deduction amounts — including food and clothing — are selected using the debtor's state and household size together. An amount that was filled in before this behavior was corrected may have used another state's figure, so re-check the deductions on any means test prepared earlier and re-run the autofill to refresh them.

#### Secured Debt Deductions on the Means Test

The autofills that carry secured debts onto the means test forms — mortgages, vehicles, and other secured debts on Form 122A-2 (Chapter 7) and Form 122C-2 (Chapter 13) — read the case's Master Creditor List and only bring across creditors that are actually being filed:

- Creditors marked as omitted from the petition, creditors that have been removed, and the hidden duplicate entries grouped under another creditor are left out. Previously these were copied onto the form, so zeroed-out accounts and credit-report duplicates appeared as separate deduction rows that had to be deleted by hand.
- Where a creditor has no linked property, the property description entered on the creditor itself is used, so the collateral column is filled rather than left blank.
- **Arrearage cure amounts** can be populated on line 34 of Forms 122A-2 and 122C-2 from the arrearages recorded on the Master Creditor List. Each active creditor with an arrearage above zero produces one row carrying the creditor name, the secured property, and the total cure amount. Creditors with a zero arrearage, and creditors excluded as above, produce no row.
- The **monthly cure amount** on that line is not set by this autofill — it continues to be calculated from the total cure amount, so re-running the autofill does not disturb it.

#### Autofills and Values You Typed in List and Table Rows

Glade does not replace a value you entered by hand with an autofilled one. That protection applies to fields inside list and table rows — creditors, properties, income lines — as it does everywhere else on the form. It had stopped working there:

- **An autofill could overwrite a value your team typed into a list or table row.** Glade failed to recognise the row's existing value as manually entered and treated the field as empty and therefore safe to fill. Every list and table field was affected. A figure a paralegal had corrected could be quietly replaced by an autofilled one, with nothing in the form to indicate the correction had been lost.
- **A value calculated for one row could be written into a different row.** With a row's detail view open, an autofill computed for another row could land on the open row's field instead, overwriting whatever was there — including a manually entered value, which was never checked before the write. Values computed for any row other than the one you have open are now skipped rather than redirected, so a value never lands on a row it was not calculated for.

Both were silent. If your team reviewed list or table data and found figures that did not match what was entered, the values are worth re-checking against the source documents; nothing was flagged at the time.

#### Autofills That Combine Several Values

Some autofills gather several values into one field — for example collecting the descriptions of a client's assets onto a single line of a court form.

- The values are separated by a **semicolon and a space**, not a comma. Free-text entries such as asset descriptions routinely contain commas of their own, which made a comma-separated line impossible to read as a list.
- Lines filled before this change may still use commas. Re-run the autofill on the field to re-join it with semicolons.

### AI Autofills

When an AI agent autofills a group of related fields (for example, property exemptions in a bankruptcy case), re-running the agent preserves any values you have already entered or confirmed. The agent incorporates existing data rather than overwriting it, so you can re-run an analysis after adding new items without losing prior work.

Manual edits to fields in a list also stick when the AI auto-runs after rows have been added, removed, or reordered. For example, on the Bankruptcy Schedules questionnaire, the schedule classifier may run repeatedly as the form changes — moving a creditor from Schedule D to Schedule F by hand will not be reverted by a later automatic run.

#### Re-running an agent over a list

The agents that fill a whole list — exemptions on Schedule C, vehicles, secured debts, mortgages, and arrearages — **replace** the rows from the previous run rather than adding a second set alongside them.

- Running the exemptions agent a second time used to leave the earlier claims in place underneath the new ones, so each run doubled the Schedule C list and the extra rows had to be deleted one at a time. The same could happen on the other list agents and when importing into a list.
- **Duplicates already sitting on a case are not cleaned up.** If a list on one of your cases was doubled by an earlier re-run, delete the extra rows once; re-running the agent from now on will not add more.
- A re-run **updates the rows that are already there** instead of rebuilding the list from scratch, so an exemption claim stays attached to the property it was claimed against. The generated Schedule C, the property's link to its exemption, and the Chapter 13 liquidation analysis all continue to point at the right claim after a re-run.
- Changing a claim from a custom amount to the property's full market value clears the amount and the explanation that went with it, rather than leaving the earlier figure on the row.

Two things to be aware of when you re-run:

- A claim you added or edited by hand can be overwritten by a later run of the agent when it sits on a property the agent also produces a claim for. Values elsewhere in the questionnaire are untouched.
- Re-running the vehicles agent when it finds nothing to claim leaves the previous run's rows in place. Clear them yourself if the earlier result no longer applies.

Each autofilled field shows a status indicator describing its current state:

- **Synced with [source]** — the autofilled value is current and up to date with the source data.
- **Import Autofill** — the autofill has not run yet. Click the pill to trigger it immediately.
- **Edited** — the field value was manually changed after autofill. A re-run button lets you re-apply the autofill if needed.
- **Out of sync** — the source data has changed and the autofilled value may be stale. Re-run to update.
- **Error** — the autofill encountered an error. A re-run button lets you try again.

### Chapter 13 Plan Calculator

On Chapter 13 questionnaires, a **Plan Calculator** button appears in the form header. Clicking it opens the Chapter 13 Plan Calculator in a new tab alongside the questionnaire. The calculator uses case data to help attorneys analyze payment structures, classify claims, and prepare the repayment plan without leaving the questionnaire workflow.

The Plan Calculator button only appears on questionnaires identified as Chapter 13. If the button is not visible on a Chapter 13 questionnaire, contact support to confirm the feature is enabled for your firm.

#### Plan Elections

Some entries on the Chapter 13 plan are choices the calculator does not compute for you. You set these directly in the calculator, and they appear on the generated plan:

- **Vesting of estate property** — when property of the estate vests back in the debtor (for example, at plan confirmation or at discharge).
- **Plan payment method** — how the debtor makes plan payments to the trustee.
- **Tax-refund treatment** — how the debtor's tax refunds are handled during the plan.
- **Amended sections** — the list of plan sections being amended, when you are filing an amended plan.

Each election offers the standard choices plus an **Other** option with a free-text box for anything outside the preset list. These elections are optional — a plan with one left blank still generates, and the calculator flags any blank election so you can fill it before filing. If the list of amended sections is longer than the space on the form, the calculator warns you that it will not all fit.

On the **Northern District of Ohio** plan, an unanswered plan payment method is now flagged the same way it already was on the Northern District of Georgia plan. Previously that section printed blank with no warning at all, so a plan could go out with no payment method elected and nothing to indicate it. An **Other** election whose description is left empty is treated as unanswered and raises the same warning, since a blank "Other" prints identically to no election. Choosing payroll deduction, direct payment, or **Other** with a description clears the warning. The unanswered election also appears in the plan's completeness report.

#### Lump-Sum Payments

Alongside the regular monthly plan payment, you can schedule one-time lump-sum contributions to the trustee — a tax refund, a bonus, or the proceeds of a sale, for example. Each entry records:

- The **amount** of the payment.
- The **date** the payment is anticipated, as a calendar date.
- A short **description** of where the money comes from, so the plan says what the payment is.

How lump sums are used:

- They count toward the plan's total funding, its payment schedule, and the trustee fee. The figures on a finalized plan match what the calculator shows, so the printed plan and the calculator no longer disagree about total funding.
- On the Northern District of Georgia plan, each lump sum prints on the "additional payments to the trustee" line as the amount, the date, and the description — for example, `$4,500 on 10/15/2026 (tax refund)`. The description is left off when you have not entered one. Entries print in date order, earliest first.
- That section of the form has room for two lines. If you enter more lump sums than fit, the calculator warns you that they will not all print.
- An entry with no amount, or with a date before the plan's start date, is left off the plan.
- Lump sums recorded before dates and descriptions were available still print in their original form, showing the amount and the plan month it falls in rather than a calendar date.

#### Amounts Promised to Unsecured Creditors

The plan's general-unsecured section states a minimum the plan will pay to unsecured creditors. That figure now prints the amount the plan actually delivers to unsecured creditors after every other treatment is funded, rather than the ceiling your firm set on the unsecured pool.

- Previously the printed figure was the pool ceiling. On a plan whose funding does not reach that ceiling, the form promised more than the plan pays — a plan paying $11,700 to unsecured creditors could print "at least $50,000".
- The two figures are the same on a plan funded to the ceiling, so plans that were fully funded are unchanged.
- This applies to both the Northern District of Georgia and Northern District of Ohio plans.

If your firm filed a plan with an unsecured pool ceiling set on it before this correction, check the stated minimum against what the plan actually pays.

**A plan that pays nothing to unsecured creditors states the plain remainder.** On the Northern District of Georgia plan, the general-unsecured section offers two elections: pay whatever funds remain, or pay the larger of a stated dollar figure and the funds remaining. Where your firm has set a ceiling on the unsecured pool and nothing actually reaches general unsecured creditors, the plan now takes the first election.

- Previously setting any ceiling took the second election regardless of amount, so a plan delivering nothing to the pool printed a promise to pay "the larger of the sum of $0.00 and the funds remaining" — a statement that says nothing and reads as an unfinished form.
- This covers both ways the pool can come to nothing: a ceiling entered as $0, and a positive ceiling that the plan's funding never reaches.
- Plans that do deliver a positive amount to unsecured creditors are unchanged and keep the stated-figure election.

This affects the Northern District of Georgia plan only.

#### Lien Avoidance and Collateral Value

When a secured claim is treated as a lien avoidance, the plan's lien-avoidance worksheet and the secured amount the plan schedules for that creditor now use the same numbers.

- Glade derives the claim's collateral value from the worksheet entries you fill in — the lien amount, other liens against the property, the exemption claimed, and the property's value — using the same impairment test the worksheet itself applies.
- Previously the worksheet and the plan's secured split were computed from separate inputs, so a worksheet showing a lien as fully avoided could sit alongside a plan that still scheduled a secured payment to that creditor.
- A collateral value you enter directly as an override still wins over the value derived from the worksheet.

#### Generated Plan Document

When you finalize a Chapter 13 plan, Glade regenerates the plan PDF and stores it, so the workflow's Documents tab reflects the version you just finalized instead of an out-of-date copy.

- Every finalized version of the plan is kept in the Documents tab as chronological version history. The most recent version is the one used for court filing; earlier versions stay available for reference rather than being replaced.
- All finalized versions appear together under a single **Chapter 13 Plans** folder, listed as individual files. Each version is no longer split out into its own separate folder, so you can see the full version history of the plan in one place.
- Interest rates on the generated plan display as percentages — for example, a 9% rate prints as `9.00%` rather than `0.09%`.
- A claim whose treatment does not carry interest — a pro-rata secured treatment, for example — prints a blank interest rate rather than a figure. On the Northern District of Ohio plan form, changing a claim to one of these treatments used to leave the rate from the treatment you selected before it sitting in the §3.2 and §3.3 rate cells, so the plan showed an interest rate for a claim that pays none.
- **Dollar signs come from the value, not the form.** A money entry that holds a number prints with a dollar sign — `$1,234`. A money entry you have **overridden with text** prints exactly the text you typed, so `TBD` prints as `TBD` rather than `$TBD`. A money entry with no value at all prints as an empty cell rather than a lone `$`.
- Every amount in the plan's payment schedule carries a dollar sign, including the first one. Previously the first amount in a schedule printed bare while the rest were marked.
- District and court-level figures are locked to the version you finalized. The values the plan is built from — the no-look attorney fee cap, the filing fee, the trustee's name, the prime rate and other applicable rates — are recorded with each finalized version. If the district later changes one of those figures, re-opening or regenerating an already-finalized plan still shows the figures that were in effect when you finalized it, so a filed plan does not silently change after the fact. Any per-case adjustments you entered by hand are kept with the version as well and continue to apply.
- **Northern District of Ohio** cases can generate a Chapter 13 plan. The district's plan form is available from the calculator, and the generated plan is built from the district's own figures — the trustee fee percentage, the no-look attorney fee cap, and the applicable interest rate — in the same way as other plan-generation districts. There is no per-firm setting to switch on.
- **Western District of Washington** cases can generate a Chapter 13 plan on the district's Local Bankruptcy Form 13-4. It works the same way as the other plan-generation districts: the form is available from the calculator, the plan is built from the district's own recorded figures, and there is no per-firm setting to switch on. Cases in this district previously reported that plan generation was not available for them.

> TODO: Confirm the Western District of Washington's recorded no-look attorney fee cap and trustee fee percentage before firms rely on a generated plan — these were still carrying placeholder values when the district was switched on, and the fee cap prints on the plan itself.
- Versions finalized after a district change pick up the new figures. When you start the next version of a plan, it tracks the district's current values rather than inheriting the locked figures from the previous version. An amended plan therefore reflects the figures in effect at the moment you finalize it.

#### Secured Claims With an Arrearage Cure

When a secured creditor — for example a mortgage servicer — is both maintained going forward and has past-due arrears to cure, the generated plan lists that creditor as a **single line** in the secured-claims section. The ongoing payment and the arrearage cure amount appear together on that one line rather than as two separate rows for the same creditor.

- You can set the arrearage cure's own **first and last payment months** — the months the cure payments start and stop — separately from the ongoing payment. When you set these in the calculator, they carry through to the generated plan.
- Clearing an override field back to blank — collateral value, contract payment, or interest rate — restores the value from the questionnaire for that creditor rather than leaving it empty, so a cleared field no longer wipes the underlying figure.
- On the **Northern District of Ohio** plan form, the ongoing installment and the arrearage cure are combined onto one line per creditor, as that district's form requires. The arrearage amount, its interest rate, and the monthly cure payment all appear on the creditor's own line, and no separate arrearage row is listed. The **current installment** on that line is the payment from the plan's payout schedule rather than the contract payment, so it reflects what the plan actually pays. The trustee-payments exhibit continues to count both the ongoing payment and the cure.

#### Unsecured Creditor Pool on the Ohio Northern Plan

The unsecured creditors section of the Northern District of Ohio plan shows one figure, not two:

- If you have entered a pool amount by hand, that amount is used and the liquidation minimum is not also shown. Your entry takes priority.
- If you have not entered one, the liquidation minimum — the amount unsecured creditors would receive in a Chapter 7 liquidation — is shown as the reference figure.

Previously both could appear, which left the plan stating a minimum that your manual figure was meant to replace.

#### Plan Form Explanation

The plan preview's **Explanation** view describes what each field on the plan form means. Those descriptions are grouped under a heading for each part of the plan document — the case caption, then each numbered part, and the trustee-payments exhibit where the district's form has one — so you can collapse the parts you are not working on and find the field you are looking at. Previously every description arrived as one unbroken list under a single heading.

- Grouping is available on the plan forms for the **Northern District of Georgia** and the **Northern District of Ohio**.
- Only parts of the form that have mapped fields get a heading. A part that is fixed text with nothing to fill in — for example vesting on the Northern District of Georgia form — has no heading rather than an empty one.

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

Fields that sit inside a table underneath an explanation heading receive synced values like any other. Schedule I line 8 is the common example: those business and rental income lines are nested this way, and values sent from the Income Organizer were being skipped, so the lines stayed at $0.00 with nothing to indicate a figure had been missed. They fill on the next sync. If your team has been re-typing Schedule I line 8 figures by hand, re-sync the case and the lines should populate on their own.

#### Turning sync off for one questionnaire

You can stop a single questionnaire from syncing with case data without waiting for an out-of-sync banner to offer it. On an in-progress Glade questionnaire, the same three-dot menu that holds the questionnaire's other actions offers:

- **Disable case data sync** while the questionnaire is syncing. You are asked to confirm, and syncing stops for that questionnaire only. Answers already on the form are left exactly as they are.
- **Re-enable case data sync** while syncing is off. Choosing it only turns syncing back on — no answer is replaced, and there is nothing to review first. Use this when a questionnaire's edits have stopped carrying over to the rest of the case.

A disable you make from the menu is remembered through submission. Submitting a questionnaire turns syncing off, and re-opening one normally turns it back on again when the case data behind it has not changed — so a questionnaire you had deliberately disconnected used to reconnect itself the moment someone submitted and re-opened it. It now stays disconnected until you turn syncing back on yourself.

- Turning syncing back on — from the menu, or from the out-of-sync banner — clears the manual disable. From then on, submitting and re-opening reconnects the questionnaire automatically again, as it does for any other questionnaire.
- **Re-enable is not offered in the menu while the out-of-sync banner is showing.** Use the banner's own action in that case, so you see which values case data would change before anything is replaced. See [Reviewing changes before you sync](#reviewing-changes-before-you-sync).
- Upgrading the questionnaire to a newer template version does not reconnect a questionnaire you disabled by hand.

### Entity-Bound List Fields

Some list and table fields are linked directly to case entities such as creditors or assets. When a questionnaire has this binding configured, adding, editing, or removing rows in those lists updates the corresponding case entities.

- When a firm team member removes a row from an entity-bound list, the corresponding entity (creditor or asset) is deleted from the case record immediately.
- When a client removes a row, the deletion is held for team review rather than applied immediately. A team member must approve the change before the entity is removed from the case record.
- Writes (adding and editing rows) follow the same case data sync behavior as other synced fields.

### Deleting and Restoring Case Data Entities

Case records hold entities such as creditors and assets that feed synced questionnaire lists. When an entity is deleted from the case record, it is removed from live lists, entity counts, and any synced questionnaires — but it is not erased. The deletion is recorded so your team can review what was removed and undo it.

- Each deletion is kept with who deleted it and when, and is retained as history rather than silently discarded. Restoring an entity is recorded the same way.
- Deleted entities appear in a removed-items view. Restoring an entity returns it to the case record and re-creates its corresponding questionnaire row with the values it had.
- Deleting entities from the case record keeps synced questionnaire lists in step: the matching rows are removed, and the remaining rows in a sync-enabled list continue to show their values. Previously, deleting case-data entities could leave blank rows where the deleted items used to be in lists such as "Your Property"; those rows now display correctly, and the deleted items still appear under Removed Items.
- **Removal history on a removed item.** Opening an item in the removed-items view shows every time it was removed or restored, oldest first, with who did it and when. An item that was removed, restored, and removed again shows all three events rather than only the most recent one — so on an amended schedule your team can explain why an asset or creditor is no longer on the petition. Removals Glade carries out on its own, such as a credit report resync, a questionnaire resync, or duplicate cleanup, are recorded with no person named against them.

### Blank Rows Are Not Written to the Case Record

An empty row left behind in a questionnaire list — a creditor row someone started and abandoned, a blank property row — is not written to the case record. Only rows with at least one field filled in create a creditor, asset, or other case entity.

- A blank row alongside filled rows is skipped; its filled siblings are still saved as normal.
- A partly-filled row is kept. Only rows where every field is empty (or contains nothing but spaces) are dropped.
- Nameless entries created before this took effect are cleaned up the next time the questionnaire syncs — they are treated as no longer present and removed from the case record.

Blank creditor rows previously became nameless creditors on the case, which then spread into the schedules and could leave them unusable until someone cleaned the case record up by hand.

### Upgrading a Questionnaire and Case Data

Upgrading a questionnaire to a newer template version does not remove case data that the questionnaire does not cover.

- Property, creditors, and other case entities that came from elsewhere — a sibling questionnaire, a credit report import, your team entering them directly — survive the upgrade.
- Case entities are only cleared out during an upgrade when the questionnaire being upgraded is the bankruptcy schedules questionnaire *and* it is actively syncing with case data. That is the only case where the form genuinely owns those lists.
- Previously, upgrading any questionnaire cleared every live asset and creditor that the new version did not contain. Upgrading a form with no property list, for example, could wipe all of the case's property. If a case lost case-data entries after a questionnaire upgrade, restore them from the removed-items view (see [Deleting and Restoring Case Data Entities](#deleting-and-restoring-case-data-entities)).

**An upgrade does not switch case data sync back on for a questionnaire that had it switched off.** Submitting a questionnaire stops it syncing, deliberately, so that a form the client has already handed in cannot go on overwriting the case record — or be overwritten itself. Until this correction, an upgrade re-enabled syncing on any questionnaire that was not marked *completed*, and a questionnaire sitting in **submitted for review** is not completed. Because the schedules template is republished often and questionnaires upgrade when they are opened, a client questionnaire that had been submitted weeks earlier could quietly become an authoritative source again and push its stale answers back over schedules an attorney had prepared since.

- Syncing is now re-enabled by an upgrade only where the questionnaire is still **in progress** and has never synced — the case the re-enabling was written for, where a template gains its first case data connections.
- A questionnaire whose syncing was switched off deliberately, whether by submission or by your team, stays switched off through an upgrade. Turn it back on from the questionnaire itself when you want it (see [Re-opening](#re-opening)).
- This stops further overwrites; it does not undo any that already happened. If prepared schedules on a case were replaced with older client answers, the replaced values need correcting on the case.

**An upgrade no longer empties a prepared list.** Opening a schedules questionnaire on a case whose template had moved to a newer version could remove most of the case's creditors and assets — on one reported case, 102 of 149 creditors were gone the next morning, with only the deduplicated ones left behind. The upgrade was reading the freshly-copied list back before it had finished being written, saw nothing there, and treated the case's creditors as though they had been deleted. It now reads the list as it stood before the upgrade, which is settled and complete.

Two safeguards sit behind that, so a bad read can no longer take a list with it:

- If the upgrade reads back an empty list while it is about to remove entries, it stops and removes nothing.
- If it would remove ten or more entries and more than half of what it looked at, it stops and removes nothing.

In either case the upgrade still completes and the questionnaire is usable — only the removals are skipped. Cases affected before this correction are being repaired case by case; contact support with the case if creditors or assets are missing after an upgrade rather than re-entering them, so the repair can restore the deduplication and ordering along with the rows.

### Creditor Duplicate Status

When you mark a creditor as a duplicate of another in a bankruptcy questionnaire, that status is saved to the case record and stays consistent everywhere the case's creditors appear:

- The duplicate mark syncs to the case record and to other questionnaires on the same case. The client and Schedules questionnaires keep their duplicate marks in step while both are open, so marking a creditor as a duplicate in one is reflected in the other.
- When a new questionnaire is seeded from the case record — for example, when Schedules is started — creditors already marked as duplicates come in already marked, instead of being dropped from the new list.
- Manual duplicate marks are preserved. Starting a new questionnaire no longer re-derives duplicates from scratch, so a creditor you marked by hand — for example, two creditors with the same name but no account number, which automatic matching cannot link on its own — stays marked.
- Un-marking a creditor clears its duplicate status the same way, across the case record and the other questionnaires.

**A list that has duplicates says so.** Rows marked as a duplicate are hidden from the list, and the list now carries a banner above it reading **"N items are currently marked as duplicate in this list"**, with a **Show Duplicates** action next to it for revealing them. The banner counts the hidden rows and appears only when the list actually has some — a list with no duplicates shows neither the banner nor the action. Previously the only sign that items had been tucked away was a small **Show duplicates** toggle, which was easy to miss, so a Master Creditor List could look shorter than it was with nothing to indicate why.

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

### Navigating to Fields with Errors

When a section or subsection shows a validation-error badge, clicking the badge opens a dialog that lists every field in that subsection still needing attention, each with its label and error message. Selecting a field takes you straight to it — switching to the right subsection if needed — scrolls it into view, focuses it, and briefly highlights it, so you can fix each issue without scanning the whole subsection by eye.

Every issue leads with the label of the field it belongs to, so an entry reads **8b. Interest and dividends — 'Amount' is required** rather than a bare *'Amount' is required* that could belong to any line on the form. Where the message already names the field, the label is not repeated.

Issues on a table cell also name the column they sit in, next to the subsection — for example **Part 2: Give Details About Monthly Income · Debtor 1**. A questionnaire table repeats the same fields across columns, so without this, a form such as Schedule I's income table produced runs of identical entries (eight consecutive *'Amount' is required* lines) with no way to tell which line or which debtor each one was for.

Composite fields — an address, a name, a currency amount — list each missing part under one heading rather than as unattributed fragments: **Firm address — 'City' is required; 'State' is required; 'ZIP Code' is required**.

Completion and error counts treat a deliberate **0** or a **No** (false) answer as a valid, complete response. Number and yes/no fields answered this way are no longer counted as incomplete, so the badge counts reflect only fields that are genuinely unanswered.

### Submitting with Incomplete Fields

When you click **Submit Questionnaire** and required fields are missing, a **Fields Need Attention** dialog opens immediately. The dialog shows how many fields are incomplete and which sections they are in (up to five sections are listed by their position in the form, with a count of any additional). The dialog only lists sections with errors that are currently visible and actionable — sections whose errors only come from hidden or non-actionable fields are not flagged, so completed sections no longer appear in the dialog as needing attention. Submission is only blocked when at least one visible, actionable error remains. You must check the acknowledgment checkbox before the **Submit Anyway** button becomes active. Clicking **Submit Anyway** bypasses validation and submits the form — useful when a field is not applicable to a particular client and cannot be left blank under normal validation rules. Clicking **Continue Editing** closes the dialog and leaves the questionnaire open for further editing. If you complete all incomplete fields before clicking Submit again, the form submits directly without the dialog appearing.

When a questionnaire is submitted this way, an entry is recorded in the workflow activity timeline showing the questionnaire name and the number of required fields that were left unanswered. This gives your team a full audit trail of bypass submissions.

**Who can submit anyway.** Waiving a blocking issue is limited to firm owners, firm Admins, and Glade Admins. Everyone else — case workers, paralegals, and clients working in the portal — still sees the full list of what needs attention, but the acknowledgment checkbox and the **Submit Anyway** button appear disabled, with a note reading *"Only an Admin can submit a questionnaire that has fields needing attention."* They can correct the flagged fields and submit normally; they cannot push a petition past a blocker. This applies on the firm dashboard and in the client portal alike.

**Findings that do not block are shown, not waived.** Not every finding stops a filing. When a submit turns up findings but none of them block:

- The review dialog still opens, so the findings are read rather than passing unseen.
- There is no acknowledgment checkbox and no Admin restriction — the action is a plain **Submit**, available to anyone who can edit the questionnaire, including a client filling out their own forms.
- Nothing is recorded as a bypass in the workflow activity timeline, and the dialog does not describe the filing as incomplete, because nothing was waived.
- A required signature is still confirmed at submission time in the usual way.

When at least one blocking finding is present, the dialog behaves exactly as described above — acknowledgment, **Submit Anyway**, Admin only, and an activity entry — even if advisory findings are listed alongside it.

Informational findings on their own do not interrupt a submit at all. They appear in **Check petition** (see [Petition Check Summary](#petition-check-summary)), which is where to look for them.

Previously the dialog was decided by which button opened it rather than by what the findings said. A submit whose findings were all advisory went through in silence and those findings were never shown to anyone who did not separately run Check petition. Expect one extra confirmation step on those submissions where there was none before.

**Submit Anyway** is also available when a required signature has been skipped — you can submit the questionnaire without completing the signature.

When the signature confirmation modal appears at submission time, you have three choices:

- **Sign** — apply or confirm the signature and submit.
- **Skip** — submit while keeping any signature values that were already entered in the questionnaire. Use this when you have manually typed signatures earlier and want them preserved on the saved draft or PDF.
- **Clear & Submit** — clear every signature field on the questionnaire (including signatures inside list and table rows) and then submit. Use this when you are saving the questionnaire as a draft for client review and the draft should not show any signatures or signing dates.

When a questionnaire is submitted using Submit Anyway, the workflow activity timeline records an entry showing that the questionnaire was submitted with the number of fields left unanswered. This lets your team see at a glance which submissions bypassed validation and how many fields were incomplete at the time.

### Generating a Draft Petition

While you are still working on a bankruptcy schedules questionnaire, you can generate a draft petition to review or send for review — without submitting the questionnaire. Three actions sit together on the form: **Check petition**, **Generate draft**, and **Submit petition**.

- **Generate draft** builds the petition PDF from the answers as they stand right now. The schedules task stays open, the workflow does not advance, and the client is not notified. Only **Submit petition** does those things, and its behavior is unchanged.
- **Generate draft** offers two choices — the marked draft described below, and an unmarked copy for signing. See [An unmarked copy for signatures](#an-unmarked-copy-for-signatures).
- You can generate a draft as many times as you need while you keep editing. Each run produces a fresh PDF from the current answers.
- A short status message appears while the PDF is being assembled. When it is ready, a **Draft petition generated** message with an **Open draft** link stays on the form — the link opens that exact draft in a new tab, so you can come back to it after the status message has gone.
- Clicking **Generate draft** again while a draft is already being built does not start a second run.

Generating a draft is available to your team on a supported bankruptcy schedules questionnaire. Previously the only way to produce a petition PDF was to submit the questionnaire, which also completed the schedules task and moved the case forward — so a paralegal who wanted a copy to check had to advance the case to get one.

#### The draft is marked as a draft

Every page of the **Petition (Draft)** document carries a marking down the right-hand margin: the Glade mark, the word **DRAFT** repeated down the page, and a shield showing how many blocking issues the petition check found at the moment the draft was built.

- The marking exists so a printed draft cannot be mistaken for the filing copy once it is off the screen and in a stack of paper on a desk.
- The **shield count matches the Petition Check badge** — it counts blocking findings, and it leaves out signature fields, exactly as the badge in the questionnaire header does. It is a snapshot from when the draft was generated, so it does not move as you correct fields; generate a new draft to refresh it.
- **Signature Pages are not marked.** The pages a client signs in ink come from the unmarked copy, so nothing overprints a signature block.
- **The petition compiled for filing is not marked.** Only the draft carries it.
- If the marking or the issue count cannot be produced for some reason, the draft is still generated — just without the marking — rather than the generation failing.

#### An unmarked copy for signatures

The marking down the margin is what makes the draft unsuitable to sign, so **Generate draft** also produces an unmarked copy on request. Choosing it opens two options:

- **Generate draft petition (with watermark)** — the marked **Petition (Draft)** document described above. This is what the button has always done.
- **Generate petition for signatures** — the same petition, built from the same answers, with no marking. It is saved as **Petition for Signatures (Draft)** in Forms & Schedules, next to the marked draft rather than in place of it.

Use the second when you are collecting wet-ink signatures from the debtor before the case is ready to file, and the first when you want a review copy that cannot be mistaken for the filing version.

- Both documents are produced when you ask for the unmarked one, so the marked draft stays available.
- **The two never drift apart.** Once a case has an unmarked copy, it is rebuilt every time the draft is regenerated — by hand or automatically — so the pages the debtor signs always match the current draft.
- The **Open draft** link after generation opens whichever document you asked for.
- If the unmarked copy cannot be produced, the action reports an error rather than quietly handing back the marked draft in its place.

### Petition Check Summary

Before a client or preparer submits a petition questionnaire, a **Petition Check** dialog gives a single, consolidated view of everything still needing attention, instead of surfacing problems one field or section at a time:

- Summary tiles at the top count the outstanding **validation errors**, the **sections affected**, the **incomplete dates**, and the **incomplete signatures**, so you can gauge the overall state at a glance.
- Below the tiles, every outstanding issue is grouped by section and subsection in an expandable list. Each entry shows the field label and what is wrong, and a **Go to field** action takes you straight to that field — switching sections if needed, scrolling it into view, and focusing it.
- Issues on list rows are included in both the counts and the list. Previously, required-field issues inside a list row — for example, blank fields on a row of the Master Property List — could be dropped from the section badges and this summary when the row took its section from the parent list, so a list with many missing fields might read as a single issue or none. All of a row's outstanding issues now appear.
- Standalone date fields — such as a date of birth or the date a debt was incurred — appear in the normal issue list and section badges alongside every other field, rather than being separated into their own tile where they were easy to overlook.
- **Issues on fields the form never shows are left out.** A section that is divided into subsection tabs displays its fields inside those tabs. A leftover field belonging to no tab is not displayed anywhere, so it can never be filled in — and when such a field was marked required, it produced a permanent blocking issue with no way to resolve it, sometimes with nothing but a generic label to identify it. **Go to field** had nowhere to take you. These issues no longer appear in the Petition Check dialog, in the section and subsection badge counts, or in the count that gates submission. Fields you can actually reach are unaffected, including fields on sections that have no subsection tabs at all and the means-test summary fields that appear on every tab.

Once a check has run, the results stay available while you work through them:

- A shield icon with a count of the outstanding findings remains in the questionnaire header. Selecting it reopens the results you already have, without running the check again — so going back to the list after correcting a field is immediate.
- The count stays current as you fix errors on the form. Resolving a field lowers the number without a second check.
- Previously the results dialog closed as soon as you navigated to a field, and getting back to the findings meant re-running the whole check, which is slow and interrupts correction work.
- **The results open whatever the check found.** A run that turned up only advisory or informational findings used to show a "No validation issues found" message and no dialog, while reopening the same results from the header shield listed them in full — so the same check appeared to contradict itself between the first click and the second. Both routes now open the results for any finding, and the "no issues found" message appears only when the check genuinely found nothing.

**Issues are listed in the order they appear on the form.** Working the list from top to bottom walks you down the questionnaire in one pass, rather than sending you back and forth through it:

- Within a section, entries follow the subsection tabs left to right, then field order within each tab. An issue on a field that sits above the tab strip comes before the tabbed subsections.
- Issues on a list or table row sit with the field they belong to, instead of being collected after every ordinary field in the section. A table reads down each row before moving to the next column, and a list reads each row's fields together — so both of a joint case's debtors are grouped rather than interleaved.
- A list's own issue comes before the issues on its rows.
- Severity no longer controls the order. Blockers and advisories are interleaved in form order, and each entry is tagged with its severity so you can still tell them apart. Previously every blocker was listed ahead of every advisory, which reordered the list around a distinction the entries gave no visible sign of.
- **Go to first error** lands on the earliest failing field in the form rather than an arbitrary one.
- The order is stable. Re-running the check on an unchanged questionnaire produces the same list in the same order; previously it could come back differently each time.

Each row is laid out as the field label, the subsection it sits in, and then the finding itself in a speech bubble pointing at the Glade AI mark, so a several-sentence cross-check explanation reads as commentary from the assistant rather than competing for urgency with a four-word required-field message. Findings previously printed inline in warning orange, at the same weight whether they were one word or a paragraph.

The findings themselves are written to say only what is wrong, since the row already names the field:

- A missing answer reads **Required** rather than restating the whole question back to you — a difference that mattered most on long labels, where a single question could fill five lines of the dialog.
- Related wordings follow the same pattern: **At least one entry required**, **Invalid date**, **Must be a valid number**.
- **Findings about part of a field keep naming that part.** On a name, address, or amount that is only partly filled, the finding still reads `'Last Name' is required`, `'ZIP Code' is required`, or `'Amount' is required` — the label alone does not tell you which piece is missing.
- Messages your firm's template administrator wrote on a validation rule are shown exactly as written and are not shortened.

Glade validates signature, date, and currency answers precisely so the check's counts match what you see on the form:

- A signature that is missing its date flags the date field itself, not just a generic "signature and date are required" message, so you can tell which part is missing.
- A signature mark with no name after it (an empty electronic-signature placeholder) is not accepted as a completed signature.
- A date that is present but not a recognizable date is flagged as **invalid** rather than passing silently. A date entered as free-form text, instead of picked from the calendar, counts as filled.
- A currency amount marked **Unknown** or overridden with explanatory text counts as an answered field and is no longer reported as missing.

#### Findings appear on the field itself

Not every finding blocks a submission, and the ones that do not are now shown on the field they name, not only in the check dialog.

- An advisory or informational finding prints as a note directly beneath its field, with its severity named and the message written out in full. A cell inside a table or a list row carries its note the same way.
- The field is not marked as failing: its border and label stay as they are, and the finding does not gate the submit. Only blocking findings turn a field red, and they appear as they always have — a blocking finding is not repeated as a second note.
- Colour follows severity consistently everywhere a finding is shown. Blocking findings are red, advisory findings amber, and informational findings grey — the same treatment in the field note, the Petition Check dialog, and the subsection popover.
- Findings listed in the subsection popover are now tagged with their severity, matching the Petition Check dialog. Previously the popover printed every message in the same warning colour with no tag, so an advisory note and a blocker looked identical. Where the popover collapses several findings into a single "N issues in the list" line, that line takes the strictest severity among them.

Previously **Go to field** on an advisory finding took you to a field that looked completely clean — the message existed in the dialog and in the subsection popover, but nowhere on the form — which read as a broken check rather than as a finding you were meant to act on.

#### Rules that check answers inside tables and lists

A validation rule can be written against a single cell of a table or a list — "Form 122A-1 line 5, Debtor 1", for example, rather than a standalone field. Rules written that way are now evaluated and their findings appear in the Petition Check results alongside every other issue.

- Previously a rule anchored on a table or list cell was skipped silently. It produced no finding whether the answer was right or wrong, so a template could look fully checked while a substantial share of its rules never ran. On the standard bankruptcy schedules template this covered a large part of the business-disclosure cross-checks.
- A rule reads the cell in the row it is anchored to, so a check comparing Debtor 1's figure against Debtor 2's compares the right two cells rather than the first value it finds in the column.
- **Expect to see findings on petitions that previously reported none.** A questionnaire that passed the check before may now raise issues on answers that were always wrong but never examined. These are real findings, not a new restriction.

#### Rules that compare two answers

Some rules exist to confirm that two answers match — an address entered in two places, identity details repeated across forms — or that they differ, such as a creditor's address that must not be the debtor's own.

- **A blank answer on either side passes.** A comparison rule does not fire on an answer that has not been filled in yet, so working through a questionnaire from the top does not produce a cascade of mismatch warnings on fields you have not reached. Missing answers are reported by the ordinary required-field check instead.
- Once both answers are present, the comparison is made and any mismatch is reported as a normal finding, with the message your firm's template administrator wrote on the rule.

### Cross-Form Consistency Checks

Some answers have to agree with each other across different forms in the petition package. Glade compares them and reports a contradiction while the questionnaire is being authored, rather than leaving it to be found at the court.

The checks currently cover business and self-employment income, which has been the most common source of a self-contradicting petition — gig or business income picked up on **Schedule I line 8a** while the petition's own business question is left unanswered.

- **Business income reported without the sole-proprietor disclosure.** When Schedule I line 8a or **Form 122A-1 line 5** (gross receipts) reports business income, but petition **question 12** — *"Are you a sole proprietor of any full or part time business?"* — does not reflect it, the check flags the discrepancy.
- **Business income reported without a matching Statement of Financial Affairs answer.** When Schedule I line 8a reports business income but **SOFA question 27** does not, the check flags the discrepancy.
- **Findings point at the answer you need to change.** The sole-proprietor check reports against question 12 itself, so you are taken to the field that needs correcting rather than to a neighboring one.
- These findings are **blocking**, which means they raise the submit-anyway confirmation described under [Submitting with Incomplete Fields](#submitting-with-incomplete-fields) rather than preventing submission outright. An attorney who has reviewed the discrepancy and is satisfied the answers are correct can still submit.

A further check comparing question 12 against **SOFA question 4** (business gross income) and **SOFA question 27** is built but not yet switched on. It is held back because the two questions cover different periods — question 12 asks about a business the debtor runs *now*, while question 27 looks back four years and question 4 covers the two prior calendar years. A debtor whose business closed before filing answers question 27 *Yes* and question 12 *No*, both correctly, and the check would interrupt them anyway.

> TODO: Confirm which petition questionnaire templates these checks are active on. They are turned on per template rather than across the board, so a firm may not see them on every petition questionnaire yet.

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

### Very Large Questionnaires

Questionnaires with hundreds of list rows stay responsive while you work in them. On the largest bankruptcy schedules — a master property or creditor list running to several hundred rows — the form could previously stall long enough that the browser offered to close the page, most often while autofilled and calculated values were being recalculated after an edit. Editing, saving, and moving between sections on those forms now proceed without that pause.

Nothing about how answers are recorded changed, and there is no setting to adjust — only how quickly the form keeps up with you.

### Outdated Template Upgrade Prompt

If you try to save responses on a questionnaire whose template version is no longer accepting changes, a modal appears explaining that the template has been updated. The modal includes an **Upgrade Questionnaire** button that moves the questionnaire onto the current template version and reloads it so you can continue editing. Until you upgrade, saves on the old version are blocked.

### Re-opening

Questionnaires can be re-opened with a message explaining why, returning them to "in progress" status.

When you click **Edit** on a completed questionnaire, Glade first checks whether the case data it draws from has changed since the questionnaire was last in sync, and asks you what to do about it before the questionnaire re-opens:

- **Nothing changed** — no prompt appears. The questionnaire re-opens immediately and case data sync turns back on automatically, so edits to the case record flow into the questionnaire again just as they did before it was submitted. The out-of-sync banner does not appear at all in this case — previously it could flash briefly on re-open and then disappear on a page refresh, which looked like a problem when there was none.
- **Case data changed** — a confirmation appears *before* the questionnaire re-opens, so you decide how to handle the difference up front rather than after you are already editing. You have two choices:
  - **Get back in sync** — the questionnaire re-opens, you review the changes case data would make and choose which of them to apply, and sync turns back on. See [Reviewing changes before you sync](#reviewing-changes-before-you-sync).
  - **Keep current answers** — the questionnaire re-opens with the answers as they were, and sync stays off so the newer case data does not overwrite them.

If you choose to keep the current answers, a warning banner appears at the top of the questionnaire, with an action to reconnect it to case data. The banner is shown to team members with edit permission. Depending on how your firm's case-data syncing is set up, the action works one of two ways:

- **Reconnect without changing answers** — the banner explains the questionnaire is no longer syncing with case data and offers a **Reconnect to case data** action. Choosing it simply turns syncing back on: your current answers are kept exactly as they are, and there is no confirmation prompt. From then on, edits to the questionnaire flow back into the case record — and into downstream documents such as the petition — again. Use this when a reopened questionnaire's edits have stopped carrying over to the rest of the case.
- **Get back in sync (replaces answers)** — the banner reads *"This questionnaire is out of sync with case data."* and offers a **Get back in sync** action. Choosing it opens the preview described below, where you decide which of the pending changes to take. After you apply, Glade turns syncing back on and clears the banner.

### Reviewing changes before you sync

**Get back in sync** does not overwrite anything until you have seen what it would do. Choosing it opens a preview listing each change the sync would make, with a checkbox on every one:

- Only values that have actually drifted since the questionnaire last synced are listed. Values that already agree are left out, so the list is the difference rather than the whole case record.
- Changes are grouped by filer — primary and secondary — and labelled the way the Case Data panel labels them. Amounts, addresses, and Yes/No answers are formatted for reading rather than shown raw.
- Individual field changes and whole records (a creditor or an asset, for example) are listed separately, and each can be taken or left alone.
- Applying replaces only what you checked. Anything left unchecked keeps the answer it has now.
- Applying with nothing checked reconnects the questionnaire to case data without changing a single answer — this is the way to resume syncing while keeping the answers exactly as they are.

Previously **Get back in sync** replaced every answer with the current case record in one step. There was no way to see the list first, and no way to take some changes while leaving others, so a sync could quietly pull in a change an attorney would have declined — or be avoided entirely because of that risk.

#### What the sync preview shows

Before you apply anything, the **Get back in sync** preview shows what would change, as a before-and-after comparison rather than only the incoming value. This lets you judge each difference on its merits instead of accepting the whole set on trust.

- **Individual fields** show the questionnaire's current answer alongside the value from the case record — *current → proposed*. Where the questionnaire has no answer yet, the row reads as setting the value rather than changing it.
- **Existing creditors and properties** show a per-field comparison of only the fields that would actually change. Previously these rows were labeled just "Update", with no indication of which details differed or by how much — so the only way to know was to apply the change and compare afterwards.
- **New creditors and properties** are shown as additions with the values that would be added. There is nothing to compare against for these.
- You choose which changes to apply. Applying nothing at all simply reconnects the questionnaire to case data without overwriting any answers.

### Compare case data

**Get back in sync** only appears when Glade has detected drift since the last sync, and the list it shows is scoped to that drift. There are cases where the questionnaire and the case record genuinely disagree but no banner appears — most often after a schedules upgrade, and most visibly with creditors, where a case record can hold creditors the questionnaire has omitted, or creditors that came from a credit report and never reached the form. The default creditor list looks empty or short, and nothing offers to fix it.

**Compare case data** is a manual action you can run at any time on the bankruptcy schedules questionnaire. It compares the whole questionnaire against the whole case record, rather than only what has drifted, and it includes rows the questionnaire has omitted.

- Each difference is listed as one of: **only in the case record**, **only in the questionnaire**, **the two hold different values**, or **omitted on the questionnaire but present in the case record**.
- Every row gives you both directions — **Use case data** or **Use questionnaire** — so you can pull a missing creditor onto the form or push a correction you made on the form back to the case record, row by row.
- Taking **Use case data** on an omitted row brings that row back onto the form, so a creditor list that appeared short fills out to match the case record's creditors.
- After you apply, syncing is turned back on and the questionnaire is marked as in sync.
- The out-of-sync banner and its **Get back in sync** preview are unchanged. Use **Compare case data** when you suspect a difference the banner is not reporting; use the banner when it appears.

> TODO: Confirm where **Compare case data** appears in the questionnaire — header action or overflow menu — and whether it is limited to team members with edit permission.

### Editing a Completed Questionnaire After the Petition Is Drafted

When a **completed** Bankruptcy Schedules questionnaire is edited, Glade rebuilds the case's petition draft packet on its own — the filled court forms, the **Petition (Draft)** document, and the **Signature Pages** — so Forms & Schedules shows the edit instead of an out-of-date packet. Previously the packet stayed as it was at completion, and a correction made afterward did not reach the draft until someone regenerated it by hand.

- Rebuilding happens only for a questionnaire that has already been completed. Saves made while a questionnaire is still in progress do not rebuild anything; the packet is first produced when the questionnaire is completed.
- The replacement documents are put in place before the previous ones are removed, so the case is never left with no draft.
- If a rebuild produces no signature pages, the earlier Signature Pages file is still removed rather than leaving an obsolete packet on the case.
- Several edits saved in quick succession produce one rebuild from the latest answers, not one per save.
- Only the documents are rebuilt. Downstream workflow steps, notifications, and tasks that ran when the questionnaire was first completed are not triggered again.
- This applies to Glade's own questionnaire templates. Questionnaires on an external form provider are not rebuilt this way.

### Free-Text Dates on the Statement of Financial Affairs

Some Statement of Financial Affairs answers accept a free-text date instead of a single calendar day — for example, entering `May, Jun, & Jul 2026` for a series of payments to one creditor, or for the month an account was closed.

What you type is what prints. The text you entered appears on the generated draft and the filed form, matching what the in-form preview has always shown. Previously the preview showed your text but the generated and filed copies replaced it with one system-picked calendar date — so `May, Jun, & Jul 2026` filed as `05/01/2026`, and a firm reviewing only the preview had no way to see that the filed form disagreed.

- This applies to the payment, transfer, and closed-account date questions on Form 107 where a text override is offered.
- Dates entered as an ordinary calendar date continue to print as `MM/DD/YYYY`.
- If your firm filed Form 107 with text overrides before this was corrected, regenerate the draft on those cases so the filed forms carry the text you entered.

### Collaborators

Collaborators (additional team members) can be assigned to questionnaires with view or edit permissions.

### Completion

When a questionnaire is completed, it triggers downstream workflow steps, updates case data, generates compiled documents, creates tasks, and sends notifications.

Links between related case records — a creditor and the property securing it, or a property and the lien against it — are re-checked once every record the questionnaire creates exists. A link entered on only one side of the pair (for example, choosing the collateral on a creditor without also adding the lien from the property) is applied rather than dropped. Previously these one-sided links could go missing on the case and only appear after the questionnaire was submitted a second time.

When a questionnaire generates multiple documents — for example, filled court forms alongside supplemental documents such as a creditor matrix — the documents appear in the case document list in a consistent order: filled court forms first, followed by other questionnaire-generated documents. This ordering is maintained even when new sections are added to the questionnaire after some documents have already been created.

The creditor mailing matrix is assembled from every party who should receive notice on the case: the master creditor list, anyone added to the Schedule D and Schedule E/F "others to be notified" lists, and co-debtors entered on Schedule H. Because Schedule H co-debtors are pulled in automatically, you no longer need to add them to the matrix by hand or list them elsewhere to make sure they are noticed — entering a co-debtor on Schedule H is enough for them to appear on the generated matrix.

#### Keeping a creditor off the matrix but on the schedules

The Master Creditor List carries an **Omit from creditor matrix** checkbox. A creditor checked this way is left out of both the **Creditor Matrix** document and the creditor list submitted to the court, while staying everywhere else it belongs — on its schedule, in case data, in the Chapter 13 calculator, and on the filled schedule PDFs.

This is for the creditor a case has to disclose but should not notice. The usual example is a landlord on Schedule G where the debtor is current on the lease and is not rejecting it: the lease is disclosed, but there is no reason to mail the landlord notice of the case.

- **It is a different control from Omit from PDFs**, which takes the creditor off the schedules as well as the matrix. Use **Omit from PDFs** when the creditor should not appear at all, and **Omit from creditor matrix** when the creditor must still be disclosed on a schedule.
- A creditor checked **Omit from PDFs** is still left off the matrix, as before. Checking either one keeps the creditor off the mailing matrix.
- Both the Creditor Matrix document and the court's creditor list honor the checkbox, so the two agree.

> TODO: Confirm whether omitting a creditor from the matrix is recorded on the case activity feed. A follow-up change to log who omitted or restored a creditor was planned but is not part of this behavior yet.

#### How duplicate entries are collapsed

The same creditor entered more than once produces one entry on the matrix rather than several. Two changes make that more reliable:

- **A nine-digit ZIP and its five-digit form are treated as the same address.** An entry at `60184-1234` and one at `60184` are the same creditor, and are collapsed into one. Previously they were kept as two separate notice entries for the same party.
- **The more complete address is the one that prints.** Where the same creditor appears with both forms, the matrix keeps the nine-digit ZIP. Which entry your team happened to add first no longer decides which address the court sees.
- Capitalization, punctuation, and stray spacing in a creditor's name or address no longer prevent two entries from being recognized as the same one.
- **Genuinely different ZIP codes stay separate.** `60184` and `60185` are two addresses and produce two entries. Glade does not merge creditors that differ in a way it cannot be sure about — dropping a genuinely distinct creditor from the mailing matrix is a notice problem, so the collapse is deliberately conservative.

The same rules apply to both the **Creditor Matrix** document and the creditor list submitted to the court, so the two always agree. A matrix that had no duplicates in it is unchanged.

The creditor matrix is also included in the **petition draft** — the review copy generated when the Schedules Builder questionnaire is submitted. Firms read this draft page by page with the debtor at the signing appointment, so anything left out of it is not reviewed with the client. The matrix is appended as the final pages:

- It is added at the end, so the page numbering of everything before it is unchanged and signature pages fall where they did before.
- It is treated as a review page, not a page requiring a signature — the debtor reads it, but is not asked to sign it.
- If the matrix cannot be generated for some reason, the draft is still produced without it rather than failing outright. If a draft comes out with no matrix at the end, generate it again.
- This applies to the draft only. The petition compiled for filing does not include the matrix in its pages — the matrix is filed as its own document in the packet.

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
- Case data sync only writes to questionnaires that are still in progress. Once a questionnaire is submitted, submitted for review, snapshotted, or otherwise past the in-progress stage, incoming case data updates no longer modify its responses — completed work is preserved as it was at submission. Add or edit data on an in-progress questionnaire to apply new values from the case record. Re-opening a submitted questionnaire also resumes syncing when case data has not changed since it was last synced; if case data has changed, syncing stays off until you choose **Get back in sync** (see [Re-opening](#re-opening)).
- A field that appears only once another field carries an amount — for example the **Specify** box on Schedule I line 8h, shown once "Other monthly income" has a figure in it — is validated like any other required field. It is highlighted when empty, counted in its section's badge, and listed in the Petition Check. Fields gated on a money amount this way were previously treated as hidden and skipped by validation altogether, so a package could reach ready-to-file with an unnamed income line on a sworn schedule. Re-run the Petition Check on cases prepared before this correction to catch any that got through.
- Required-field validation skips list rows that will not be filed. Rows merged into another as duplicates (for example, deduplicated creditors) and rows explicitly marked to omit from the petition are not checked for missing required fields, so leftover data on those rows does not block submission.
- A field that is connected to case data but has never been populated still reports itself as synced with case data and offers no re-run control, because there is no value on it whose source could say otherwise. Fill or autofill the field once and the indicator reports its real source.
- Validation issues on a **list row** name the field but not the row. A list of vehicles with the make missing on two rows produces two issues that read alike, with nothing to distinguish one vehicle from the other. Table cells do name their column; list rows do not yet.
- When more than one questionnaire on the same case can sync case data — for example, the client questionnaire and the schedules questionnaire — each one syncs independently. Starting or initiating a second questionnaire does not turn off syncing on another that is still in progress: both keep syncing while open. A questionnaire stops syncing only when it is itself submitted, not when a sibling questionnaire is created.

## Related Features

- [Client Portal](../intake/client-portal.md)
- [Document Collection](./document-collection.md)

