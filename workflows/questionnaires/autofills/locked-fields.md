# Locked Fields

## Overview

A field that has an autofill can be locked, so the value it computes is the only value the field can hold. Use this where the answer should stay system-owned — a figure carried from another form, a total the case record already knows — and a hand correction would put the questionnaire out of step with the rest of the case.

## Key Behaviors

### Locking a field in the template

- **Locking is available only on a field that has an autofill.** A field with nothing filling it cannot be locked, and removing a field's autofill unlocks it — there is no state where a field is locked with no source to fill it.
- **A locked field is still shown.** It appears on the questionnaire as normal, with its value and the explanation of where that value came from, so whoever is filling the form can see the answer and understand it. What they cannot do is change it.
- **The autofill still writes.** Locking blocks hand edits, not the autofill itself, so re-running or recalculating an autofill updates a locked field as it always did.
- **Locking a field replaces whatever was typed into it.** If someone had already entered a value by hand before the field was locked, the next autofill overwrites it — unlike an unlocked field, where a hand-entered answer is protected. Check the values on a field before locking it if the existing answers matter.
- **Fields are unlocked unless someone locks them.** Nothing changes on a questionnaire whose fields have not been locked.

> TODO: Confirm where the lock setting appears in the template editor and what it is labelled there.

### Fields You Cannot Type Into

A locked field shows a lock icon alongside the description of where its value came from, and its input is greyed out.

- **You can read it, you just cannot change it.** The value and its explanation are visible exactly as on any other autofilled field. Clicking the indicator still opens the autofill's explanation.
- **The value keeps updating.** Because the autofill continues to run, a locked field picks up changes to the data behind it without anyone touching the form.
- **On a locked row of a list or table, the row's cells cannot be edited either.** The whole row is held to what the autofill produced.
- **A save that includes a locked field goes through without it.** If a change reaches a locked field as part of a larger save — for example an import, or edits to several fields at once — that one field is left alone and everything else in the save is applied. Nothing fails, and nothing from the skipped edit reaches the case record.
- If a locked field holds a value you believe is wrong, correct the data the autofill reads rather than the field. Ask whoever maintains your firm's questionnaire templates if you need the field unlocked.

## Edge Cases & Limitations

- Locking a field is the one case where an autofill overwrites an answer someone typed. The protection that keeps hand-entered values from being replaced does not apply to a locked field, so a value entered before the field was locked is replaced the next time the autofill runs.
- A locked field cannot be corrected from the questionnaire at all — not by the client, and not by an attorney or paralegal filling on the client's behalf. Fixing a wrong value means fixing the data the autofill reads, or having the field unlocked on the template.

## Related Features

- [Questionnaires](../README.md)
- [Autofills](./README.md)
- [How Autofills Work](./how-autofills-work.md)
- [Manual Overrides](./manual-overrides.md)
- [Case Documents](../../case-documents.md)
