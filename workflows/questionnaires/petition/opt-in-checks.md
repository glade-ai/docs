# Opt-In Petition Checks

## Overview

Most Schedules Builder validation rules run for every firm, and a firm can turn individual rules off. Some rules are **opt-in** instead: they are off for every firm until a firm turns them on. Opt-in rules cover checks that suit some practices and not others — such as a firm that does not take a particular kind of case and wants those cases caught before the petition is filed. Firm admins turn them on in Petition settings, and their findings appear on the field and in the [Petition Check](./petition-check.md) like any other rule.

## Key Behaviors

- **Off until your firm turns it on.** An opt-in rule never runs for a firm that has not enabled it, so its findings appear only on that firm's cases.
- **Turned on in Settings → Petition settings → Validation rules**, in the same list where rules can be turned off. Turning an opt-in rule off again stops it running.
- **Setting a severity for an opt-in rule turns it on.**
- Turning an opt-in rule on applies to the firm's questionnaires on any template version that carries the rule.
- Re-saving a field in the template editor does not turn an opt-in rule on for every firm; the rule stays opt-in.

### Eviction judgment check

The first opt-in rule is **Flag an eviction judgment for attorney review**, on Form 101 line 11.

- When "Has your landlord obtained an eviction judgment against you?" is answered **Yes**, the check raises a **blocking** finding stating that the firm does not handle eviction judgment cases and that an attorney must review the case before filing.
- A **No** answer, or no answer yet, passes. A blank answer is reported by the ordinary required-field check instead.
- Because the finding is blocking, submitting the questionnaire past it follows the usual rules for waiving a blocking finding — see [Submitting a Questionnaire](../filling-out/submitting.md).

## Configuration

| Setting | Where | Default |
|---------|-------|---------|
| Opt-in validation rules | Settings → Petition settings → Validation rules | Off |

## Edge Cases & Limitations

- An opt-in rule must be present on the Bankruptcy Schedules template version a questionnaire uses. A questionnaire on an older template version that lacks the rule is not checked by it.

> TODO: Confirm who can change Validation rules in Petition settings, and whether a questionnaire must be upgraded to a newer template version before the eviction judgment check applies to it.

## Related Features

- [Petition](./README.md)
- [Petition Check](./petition-check.md)
- [Validation Rules](../templates/validation-rules.md)
- [Submitting a Questionnaire](../filling-out/submitting.md)
- [Settings](../../../back-office/settings.md#petition-settings)
