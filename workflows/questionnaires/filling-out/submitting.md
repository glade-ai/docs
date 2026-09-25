# Submitting a Questionnaire

## Overview

Submitting a questionnaire runs its validation and, if anything still needs attention, opens a review dialog before the questionnaire is handed in. This page covers finding fields with errors, the **Fields Need Attention** dialog and who can submit anyway, and what happens when a questionnaire is completed.

## Key Behaviors

### Navigating to Fields with Errors

When a section or subsection shows a validation-error badge, clicking the badge opens a dialog that lists every field in that subsection still needing attention, each with its label and error message. Selecting a field takes you straight to it — switching to the right subsection if needed — scrolls it into view, focuses it, and briefly highlights it, so you can fix each issue without scanning the whole subsection by eye.

Every issue leads with the label of the field it belongs to, so an entry reads **8b. Interest and dividends — 'Amount' is required** rather than a bare *'Amount' is required* that could belong to any line on the form. Where the message already names the field, the label is not repeated.

Issues on a table cell also name the column they sit in, next to the subsection — for example **Part 2: Give Details About Monthly Income · Debtor 1**. A questionnaire table repeats the same fields across columns, so without this, a form such as Schedule I's income table produced runs of identical entries (eight consecutive *'Amount' is required* lines) with no way to tell which line or which debtor each one was for.

Composite fields — an address, a name, a currency amount — list each missing part under one heading rather than as unattributed fragments: **Firm address — 'City' is required; 'State' is required; 'ZIP Code' is required**.

Completion and error counts treat a deliberate **0** or a **No** (false) answer as a valid, complete response. Number and yes/no fields answered this way are no longer counted as incomplete, so the badge counts reflect only fields that are genuinely unanswered.

### Submitting with Incomplete Fields

When you click **Submit Questionnaire** and required fields are missing, a **Fields Need Attention** dialog opens immediately. The dialog shows how many fields are incomplete and which sections they are in (up to five sections are listed by their position in the form, with a count of any additional). The dialog only lists sections with errors that are currently visible and actionable — sections whose errors only come from hidden or non-actionable fields are not flagged, so completed sections no longer appear in the dialog as needing attention. Submission is only blocked when at least one visible, actionable error remains. You must check the acknowledgment checkbox before the **Submit Anyway** button becomes active. Clicking **Submit Anyway** bypasses validation and submits the form — useful when a field is not applicable to a particular client and cannot be left blank under normal validation rules. Clicking **Continue Editing** closes the dialog and leaves the questionnaire open for further editing. If you complete all incomplete fields before clicking Submit again, the form submits directly without the dialog appearing.

When a questionnaire is submitted this way, an entry is recorded in the workflow activity timeline showing the questionnaire name and the number of required fields that were left unanswered. This gives your team a full audit trail of bypass submissions, so your team can see at a glance which submissions bypassed validation and how many fields were incomplete at the time.

**Who can submit anyway.** Waiving a blocking issue is limited to firm owners, firm Admins, and Glade Admins. Everyone else — case workers, paralegals, and clients working in the portal — still sees the full list of what needs attention, but the acknowledgment checkbox and the **Submit Anyway** button appear disabled, with a note reading *"Only an Admin can submit a questionnaire that has fields needing attention."* They can correct the flagged fields and submit normally; they cannot push a petition past a blocker. This applies on the firm dashboard and in the client portal alike.

**Findings that do not block are shown, not waived.** Not every finding stops a filing. When a submit turns up findings but none of them block:

- The review dialog still opens, so the findings are read rather than passing unseen.
- There is no acknowledgment checkbox and no Admin restriction — the action is a plain **Submit**, available to anyone who can edit the questionnaire, including a client filling out their own forms.
- Nothing is recorded as a bypass in the workflow activity timeline, and the dialog does not describe the filing as incomplete, because nothing was waived.
- A required signature is still confirmed at submission time in the usual way.

When at least one blocking finding is present, the dialog behaves exactly as described above — acknowledgment, **Submit Anyway**, Admin only, and an activity entry — even if advisory findings are listed alongside it.

Informational findings on their own do not interrupt a submit at all. They appear in **Check petition** (see [Petition Check](../petition/petition-check.md)), which is where to look for them.

Previously the dialog was decided by which button opened it rather than by what the findings said. A submit whose findings were all advisory went through in silence and those findings were never shown to anyone who did not separately run Check petition. Expect one extra confirmation step on those submissions where there was none before.

**Blocking findings are listed on their own tab.** Where a run turns up both kinds of finding, the dialog separates them instead of listing everything together:

- It opens on a **Blocking** tab showing only the findings that have to be cleared. Advisory and informational findings sit on a second **Advisory** tab.
- Where every finding is of one kind, there are no tabs and the findings appear as a single list, exactly as before.
- Inside each tab the findings stay in the order they appear on the form. Severity decides which tab a finding is on, not where it sits within the tab.
- Signatures keep their own summary tile and do not decide whether the tabs appear.

On a petition check that flags a long mixed list, the items that actually stop the filing were previously buried among advisory notes and had to be picked out by reading the whole list.

**Submit Anyway** is also available when a required signature has been skipped — you can submit the questionnaire without completing the signature. For the signature confirmation at submission time, see [Signatures](../petition/signatures.md).

### Completion

When a questionnaire is completed, it triggers downstream workflow steps, updates case data, generates compiled documents, creates tasks, and sends notifications.

Links between related case records — a creditor and the property securing it, or a property and the lien against it — are re-checked once every record the questionnaire creates exists. A link entered on only one side of the pair (for example, choosing the collateral on a creditor without also adding the lien from the property) is applied rather than dropped. Previously these one-sided links could go missing on the case and only appear after the questionnaire was submitted a second time.

When a questionnaire generates multiple documents — for example, filled court forms alongside supplemental documents such as a creditor matrix — the documents appear in the case document list in a consistent order: filled court forms first, followed by other questionnaire-generated documents. This ordering is maintained even when new sections are added to the questionnaire after some documents have already been created.

For how the creditor mailing matrix is assembled, see [Creditors](../schedules/creditors.md#creditor-matrix). Editing a completed Bankruptcy Schedules questionnaire rebuilds the petition draft packet — see [Generating a Draft Petition](../petition/draft-petition.md#editing-a-completed-questionnaire-after-the-petition-is-drafted).

## Edge Cases & Limitations

- Submitting a questionnaire stops it syncing with case data — see [Case Data Sync](../case-data/case-data-sync.md).

## Related Features

- [Questionnaires](../README.md)
- [Filling Out Questionnaires](./README.md)
- [Petition Check](../petition/petition-check.md)
- [Signatures](../petition/signatures.md)
- [Validation Rules](../templates/validation-rules.md)
- [Statuses and Access](./statuses-and-access.md)
