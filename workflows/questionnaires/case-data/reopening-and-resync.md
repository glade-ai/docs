# Re-opening and Re-syncing

## Overview

A completed questionnaire can be re-opened for further edits, and a questionnaire that has drifted from the case record can be brought back in sync. This page covers what happens when you re-open a questionnaire, the **Get back in sync** preview, reconnecting without changing answers, and **Compare case data** for differences the out-of-sync banner does not report.

## Key Behaviors

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

### Compare case data

**Get back in sync** only appears when Glade has detected drift since the last sync, and the list it shows is scoped to that drift. There are cases where the questionnaire and the case record genuinely disagree but no banner appears — most often after a schedules upgrade, and most visibly with creditors, where a case record can hold creditors the questionnaire has omitted, or creditors that came from a credit report and never reached the form. The default creditor list looks empty or short, and nothing offers to fix it.

**Compare case data** is a manual action you can run at any time on the bankruptcy schedules questionnaire. It compares the whole questionnaire against the whole case record, rather than only what has drifted, and it includes rows the questionnaire has omitted.

You reach it from the questionnaire's three-dot menu — the same menu that holds the questionnaire's other actions — on an in-progress Glade questionnaire. It is offered alongside **Disable case data sync**, described under [Turning sync off for one questionnaire](./case-data-sync.md#turning-sync-off-for-one-questionnaire).

- Each difference is listed as one of: **only in the case record**, **only in the questionnaire**, **the two hold different values**, or **omitted on the questionnaire but present in the case record**.
- Every row gives you both directions — **Use case data** or **Use questionnaire** — so you can pull a missing creditor onto the form or push a correction you made on the form back to the case record, row by row. **Use case data** is preselected on every row, so applying without changing anything takes the case record's version throughout; switch the rows you want to keep from the form before applying.
- Creditors that came from a credit report and never reached the form are listed here, as are creditors the questionnaire has marked omitted. These are the two that the out-of-sync banner hides.
- Taking **Use case data** on an omitted row brings that row back onto the form, so a creditor list that appeared short fills out to match the case record's creditors.
- After you apply, syncing is turned back on and the questionnaire is marked as in sync.
- **Only the details this form actually asks about are compared.** Information that lives on the case record but has no question anywhere on the form — the attorney's bar number or the case type, for example — is no longer listed as a difference. Those rows were selectable but applying **Use case data** to one had no effect on the form, and they crowded out the disagreements worth reviewing. A question the form does ask that nobody has answered still appears, so you can pull a case record value onto the form.
- The out-of-sync banner and its **Get back in sync** preview are unchanged. Use **Compare case data** when you suspect a difference the banner is not reporting; use the banner when it appears.

> TODO: Confirm whether **Compare case data** is limited to team members with edit permission.

## Edge Cases & Limitations

- **Get back in sync** only appears when Glade has detected drift since the last sync. Differences it does not detect — most often after a schedules upgrade — need **Compare case data**.
- The reconnect banner is shown only to team members with edit permission.

## Related Features

- [Questionnaires](../README.md)
- [Case Data](./README.md)
- [Case Data Sync](./case-data-sync.md)
- [Template Upgrades](./template-upgrades.md)
- [Statuses and Access](../filling-out/statuses-and-access.md)
- [Creditors](../schedules/creditors.md)
