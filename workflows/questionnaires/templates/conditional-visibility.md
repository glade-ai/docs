# Conditional Visibility

## Overview

Sections and fields on a questionnaire can be dynamically shown or hidden based on the values of other fields. Your firm's template administrator builds these conditions in the template editor.

## Key Behaviors

- Conditions use an expression system with variables that reference other fields or external data.
- Conditions can be built two ways: a guided builder where you pick a field and a comparison, and an advanced mode where you write the condition yourself.
- A field whose condition is false is hidden from the moment the questionnaire first loads. For a short period, some conditioned fields — for example an exemption question set to appear only when its parent question is answered "yes" — were shown on first load even though their condition was not met, and only hid after another answer changed. That is corrected.

### Conditions on currency fields

A currency answer carries more than a number — it also records the currency and whether the amount was marked unknown. A condition built on a currency field now compares the **dollar amount**, which is almost always what the author intends.

- A condition such as "greater than 0" on a currency field works as written. Previously the comparison was made against the whole answer rather than the amount, so it could never be true — a section set to appear when an amount was above zero stayed hidden no matter what the client entered.
- **Existing conditions are left exactly as they are.** The fix applies only to conditions created from now on. Editing a different condition in the same rule does not silently change how an existing currency condition behaves. To pick up the new behavior on a condition built earlier, delete it and add it again.
- **Filled / Not filled reads the amount too**, on conditions created from now on. A currency field holding $0.00 counts as *not filled* under a newly created condition. If you want a rule that fires whenever the client has touched the field at all, including a deliberate $0.00, check the amount rather than using **Filled**.
- Conditions written by hand in advanced mode are unchanged — the amount is not selected for you there, so keep writing those conditions the way you do today.

> TODO: Confirm the in-product names for the guided builder and advanced mode, and whether the guidance above should name the specific controls.

## Edge Cases & Limitations

- Fields that are hidden by conditional logic are not considered incomplete and do not trigger the incomplete-row save prompt (see [Working With Lists](../filling-out/working-with-lists.md)).
- A field that appears only once another field carries an amount — for example the **Specify** box on Schedule I line 8h, shown once "Other monthly income" has a figure in it — is validated like any other required field. It is highlighted when empty, counted in its section's badge, and listed in the Petition Check. Fields gated on a money amount this way were previously treated as hidden and skipped by validation altogether, so a package could reach ready-to-file with an unnamed income line on a sworn schedule. Re-run the Petition Check on cases prepared before this correction to catch any that got through.

## Related Features

- [Questionnaires](../README.md)
- [Building Templates](./README.md)
- [Fields, Lists, and Tables](./fields-and-tables.md)
- [Validation Rules](./validation-rules.md)
