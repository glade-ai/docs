# Firm Validation Settings

## Overview

Your firm can change how the checks on a petition questionnaire apply to its own cases without changing the shared Bankruptcy Schedules template. From **Petition Settings**, a firm admin can turn a validation rule or a required field off, or choose whether a missing required answer or document is **Blocking** or **Advisory**. The settings affect your firm's cases only, and are reflected wherever findings appear: the [Petition Check](./petition-check.md), the notes on each field, and the submit dialog.

## Key Behaviors

### Turning a check off

- **Validation rules.** A Run-check rule your firm turns off no longer produces a finding when anyone runs the check on one of your firm's questionnaires.
- **Required fields and required documents.** A field your firm turns off is no longer reported as missing, and a document upload your firm turns off is no longer reported as required. A rule that would only have reported the field as *Needed to check* because it was blank is not raised either.
- **Format checks still run.** Turning a required field off only stops the "this is missing" finding. If the field is filled in, checks on what was entered — minimum or maximum values, length, or format — still apply and stay blocking.
- Turning a check back on brings its findings back the next time the check runs.

### Advisory or Blocking for required fields

A required field or document can be kept on but run at a different strength:

- **Advisory** — the missing answer is still reported, as an advisory finding, but it does not stop submission. Use this for answers your team wants to be reminded about without being held up, such as an SSN or an employer's name.
- **Blocking** — the missing answer has to be supplied, or overridden by someone allowed to override, before the questionnaire is submitted. Use this to make a missing document stop submission.

By default a required field is **Blocking** and a required document upload is **Advisory**.

- The setting covers every finding that exists because the field is required — *Required*, a missing part of a name or address, a missing signature or date, and a missing required document.
- **A blank Advisory field stays advisory.** If another rule reads a field your firm has made Advisory and the field is blank, the *Needed to check* finding for it is capped at Advisory too, so the rule cannot turn it back into a blocker.
- **An Advisory required finding can be dismissed.** Like any advisory finding, any team member can dismiss it once it has been looked at (see [Dismissing an advisory finding](./petition-check.md#dismissing-an-advisory-finding)). A field kept at Blocking still needs an override from someone allowed to override — see [Submitting a Questionnaire](../filling-out/submitting.md#submitting-with-incomplete-fields).
- Validation rules can already be run at Blocking or Advisory per firm in the same settings.

> TODO: Confirm where the Advisory / Blocking choice for required fields appears in Petition Settings and when it is available to firms. The choice is supported by Glade but the control for it was released separately.

## Configuration

| Setting | Where | Who can change it |
|---|---|---|
| Turn a validation rule on or off | Petition Settings | Firm owners and firm admins |
| Turn a required field or required document on or off | Petition Settings | Firm owners and firm admins |
| Run a required field or document at Advisory or Blocking | Petition Settings | Firm owners and firm admins |

Any team member can view the settings; case workers and other team members without admin rights cannot change them.

## Edge Cases & Limitations

- The settings apply to every questionnaire your firm runs on the Bankruptcy Schedules template, including questionnaires still on an older template version.
- A setting applies to your firm only. Another firm using the same shared template is unaffected.
- Checks on what was entered in a field (values, length, format) cannot be turned off or made advisory through these settings; only the requirement that the field be answered can.
- A field can be either turned off or set to Advisory or Blocking, not both.
- These settings cover the questionnaire's checks only. The [pre-filing review](../../../integrations/efiling/pre-filing-review/README.md) is not affected.

## Related Features

- [Petition Check](./petition-check.md)
- [Submitting a Questionnaire](../filling-out/submitting.md)
- [Validation Rules](../templates/validation-rules.md)
- [Petition Settings](../../../back-office/settings.md#petition-settings)
