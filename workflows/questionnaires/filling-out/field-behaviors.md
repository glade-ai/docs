# Field Behaviors

## Overview

Several field types behave in specific ways as you fill them in — formatting, defaults, auto-selection, and how the value prints on a generated form. This page covers phone number, currency, court division, and debtor county fields, and free-text dates on the Statement of Financial Affairs.

## Key Behaviors

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

For marking an asset's value as **Unknown** on Schedule A/B, see [Schedule A/B Property](../schedules/property.md#marking-a-value-as-unknown).

### Court Division

The **court division** field lists the divisions belonging to the case's filing district. Where a district has only one division to file in, that division is selected for you when the field is still empty, so the questionnaire is not held up by a choice with only one answer.

- Districts with more than one division still require you to pick one.
- Divisions that exist only as electronic-filing variants of another division are not offered, and divisions that appear more than once in the underlying court list are shown once.
- Auto-selection only fills an empty field. A division you have chosen is never replaced.
- **A generated court form prints the division's name.** Where the court division is mapped onto a field of a court form, the generated PDF prints the division as it is named — *Tampa*, for example — rather than the abbreviated value stored behind it. E-filing and the court office lookup continue to read the stored value, so nothing about filing changes. Forms generated earlier keep the text they were generated with; re-generate them to pick up the correction.

> TODO: Confirm which generated forms this covers. It applies to forms filled from the court's own fillable PDFs; Glade's own generated layouts are unchanged.

### Debtor County

The debtor's filing county is worked out from the address on the case, by looking the address up rather than inferring it. The same address always produces the same county.

- **No AI model is involved.** On questionnaires where this field is computed for you, the county was previously produced by an AI model, which returned plausible but wrong counties for some addresses. It is now a direct lookup.
- The address has to be complete enough to identify. Where it cannot be resolved to a county, the field is left for you to fill in rather than filled with a guess.
- A county that Glade does not recognize for the state blocks e-filing and is reported in the pre-filing review. See [Electronic Court Filing](../../../integrations/efiling/README.md).

### Free-Text Dates on the Statement of Financial Affairs

Some Statement of Financial Affairs answers accept a free-text date instead of a single calendar day — for example, entering `May, Jun, & Jul 2026` for a series of payments to one creditor, or for the month an account was closed.

What you type is what prints. The text you entered appears on the generated draft and the filed form, matching what the in-form preview has always shown. Previously the preview showed your text but the generated and filed copies replaced it with one system-picked calendar date — so `May, Jun, & Jul 2026` filed as `05/01/2026`, and a firm reviewing only the preview had no way to see that the filed form disagreed.

- This applies to the payment, transfer, and closed-account date questions on Form 107 where a text override is offered.
- Dates entered as an ordinary calendar date continue to print as `MM/DD/YYYY`.
- If your firm filed Form 107 with text overrides before this was corrected, regenerate the draft on those cases so the filed forms carry the text you entered.

## Related Features

- [Questionnaires](../README.md)
- [Filling Out Questionnaires](./README.md)
- [Fields, Lists, and Tables](../templates/fields-and-tables.md)
- [How Autofills Work](../autofills/how-autofills-work.md)
- [AI Agents](../autofills/ai-agents.md) — the filing district
- [Electronic Court Filing](../../../integrations/efiling/README.md)
