# Exemptions Calculator

## Overview

The Exemptions Calculator is a panel available in bankruptcy cases that helps attorneys analyze how claimed exemptions apply to a client's assets. It aggregates properties and exemptions from the case's schedules and shows at a glance which assets are fully exempt, partially exempt, or over-limit — along with the applicable statutes. This page also covers the exemptions AI agent that fills Schedule C claims, the automatic homestead answer on Schedule C, and the Texas exemptions schedule.

## Key Behaviors

### The panel

- The Exemptions Calculator panel opens while viewing Schedule A/B, Schedule C, or the Master Creditor List. It opens in the questionnaire's resource panel and provides a summary alongside the schedule so you can review exemption coverage without leaving the form.
- A top-level **Exemptions Summary** card shows the total exempted value and the total non-exempt value across all assets.
- Two tabs organize the data in different ways:
  - **By Property** — Groups assets by category in collapsible cards. Each card shows the property name in bold, any liens indented beneath it, and the exemptions claimed against that property displayed as styled pills with the statute citation. Use **Expand All** or **Collapse All** to open or close all category cards at once.
  - **By Exemption** — Groups exemptions by statute. Each exemption card shows the statute as a subheading, the claimed amount, and the properties it applies to, indented beneath, with the amounts applied to each. Use **Expand All** or **Collapse All** to open or close all exemption cards at once.
- Status banners show the utilization state for each exemption:
  - **Purple banner** — Remaining capacity is available under this exemption.
  - **Green banner** — The exemption is fully utilized (claimed amount equals the statutory limit).
  - **Warning banner** — The claimed amount exceeds the statutory limit.
- Non-exempt rows are highlighted in red with bold text so over-limit items stand out.
- A **Only show non-exempt** toggle filters both tabs to display only properties or exemptions with a non-exempt balance, letting you focus on items that need attention.
- When viewing Schedule A/B, property names are clickable links that navigate to the property's detail view. Property links are not shown when viewing from Schedule C.

### How equity and limits are calculated

- The amount available to exempt for each asset is the debtor's **net equity** — the asset's value minus any secured liens against it — not its gross value. Liens are taken from the secured creditors selected for that property on the Master Creditor List, and every creditor secured by the property is summed and subtracted. A property can have multiple liens attached, and the total of all selected liens is used. If no creditors have been selected for a property, the calculator falls back to the single lien amount entered directly on the property. For example, a vehicle worth $3,000 with a $1,000 lien shows $2,000 of equity to exempt, not $3,000. When the secured liens exceed the asset's value, the equity to exempt is $0 (it does not go negative). A creditor whose claim amount is unknown or blank contributes nothing to the lien total. See [Property Liens on Schedule A/B](./property.md#property-liens-on-schedule-ab).
- Equity is worked out the same way everywhere it appears on a case — the Exemptions Calculator, the lien detail on a property row, the **Property summary** on Schedule A/B, and the Chapter 13 liquidation analysis all subtract the same set of liens from the same asset value. The Property summary previously showed pre-lien value in its Equity column and so could disagree with this panel on the same case; the two now match. See [Property Summary](./property.md#property-summary).
- **Joint cases are measured against the joint statutory limit.** Where a statute allows a higher amount for two filers, the calculator applies that higher limit once a second debtor is named on the Voluntary Petition — Florida personal property, for example, is measured against $2,000 on a joint case rather than the $1,000 solo cap. Every case was previously measured against the solo limit no matter who was filing, so a joint case could show an asset as partly non-exempt when the joint limit covered it in full. Re-open the calculator on any joint case you reviewed before this correction and confirm the limits it now applies.

### Live recalculation

- **Totals update as you type.** Editing an exemption amount on the Exemptions List, or a property value on the Master Property List, recalculates the summary on each keystroke. Previously the figures only moved once you clicked or tabbed out of the field, so the totals read $0 while an amount was being entered — a common source of confusion when learning the calculator. Any autofill notice on the field stays visible while you type.
- Live recalculation does not save anything. The calculator modal still requires an explicit submit to record your changes.

### Homestead question on Schedule C

On Schedule C, the homestead exemption question ("Are you claiming a homestead exemption of more than $214,000?") is automatically answered based on the client's total real estate value minus total secured liabilities from Schedule D. The field updates as those values change — no manual entry is needed.

### The exemptions agent

An AI agent can fill the exemption claims on Schedule C. For general behavior when re-running it — replacing rather than doubling the list, and keeping claims attached to their properties — see [Re-running an agent over a list](../autofills/ai-agents.md#re-running-an-agent-over-a-list).

#### Firm instructions for the exemptions agent

The exemptions agent follows the rules your firm has written for it under **Settings → Your AI agents**, and those rules take precedence over Glade's default exemption strategy. A firm that requires a custom dollar amount rather than a claim of 100% of fair market value, or that caps what may be claimed under a wildcard exemption, has that applied on every run.

- The instructions used are the ones belonging to the firm the case is filed by, so a case opened from a shared template — or one being worked by Glade staff — still follows the filing firm's rules.
- Previously these instructions were saved but never reached the agent, so every run followed the default strategy no matter what a firm had written. If your firm wrote instructions and found them ignored, re-run the exemptions agent on affected cases to pick them up, and re-check the claims on Schedule C.
- **A claim of a custom dollar amount stays a custom dollar amount**, including when the amount happens to equal the property's value. Previously a figure equal to the value was recorded as a claim of 100% of fair market value instead, which clears the amount claimed — the opposite of what a firm asking for custom amounts wants.

#### Exemption claims at 100% of fair market value

When the exemptions agent claims a property at 100% of its fair market value, the claim carries that fair market value as its dollar amount.

- Previously these claims were recorded at **$0.00** while the agent's own explanation alongside them said it was claiming the full fair market value — so Schedule C showed a claim worth nothing against a property the agent had decided to exempt in full. Properties whose ownership was recorded as unknown were affected most.
- **Claims already recorded this way are not repaired.** Re-run the exemptions agent on any case where a 100%-of-fair-market-value claim reads as $0.00, and check Schedule C before filing.
- An exemption claimed at 100% of fair market value claims the equity remaining after liens, not the property's full value, on the Property summary.

> TODO: Confirm what the agent records when the property has no fair market value entered against it — whether the claim is left unpriced, skipped, or recorded at zero.

### Texas exemptions schedule

Glade can generate the Texas exemptions schedule as a supplemental form alongside the official bankruptcy forms (see [PDF Fill Mappings](../templates/pdf-fill-mappings.md#supplemental-and-local-court-forms)).

Equity on the Texas form is worked out per asset before the category is totalled, and never goes below zero, so an asset with liens above its value contributes nothing rather than a negative amount. An exemption claimed at 100% of fair market value is capped at the equity remaining after liens.

The questionnaire fields for the Texas exemptions schedule are labelled with the same wording the printed form uses for its columns — for example **1. Real Estate — Total Encumbrances** and **Totals — Total Amount Non-Exempt**. Earlier labels used internal shorthand such as *— Enc* and *— Gross*, carried a line reference that meant nothing to a filer, and spelled the non-exempt column two different ways, so it was hard to tell which column of the form a field corresponded to. Only the wording changed: answers already recorded are unaffected, and the generated form is unchanged.

The Texas form is added to your firm's questionnaire template by Glade rather than switched on in the template editor. Contact support if your firm files in these situations and does not see the section.

> TODO: Confirm which firms and templates these sections have been added to. They are rolled out per firm rather than to everyone at once.

## Configuration

The Exemptions Calculator pulls data from the case's scheduled assets and claimed exemptions. No separate configuration is required — it reflects whatever has been entered in the relevant schedules.

Firm-specific exemption strategy for the AI agent is set under **Settings → Your AI agents**.

## Edge Cases & Limitations

- The calculator reflects the current state of the schedules. If schedules are incomplete or have not been submitted, the totals may be partial.
- Statute citations are displayed as entered in the exemption data. If a statute citation is missing or malformed, the pill still appears but may show an incomplete citation.
- Moving a secured creditor's collateral between properties previously could leave the creditor on both properties' lien lists, understating equity in this calculator — see [Property Liens on Schedule A/B](./property.md#property-liens-on-schedule-ab).
- A claim you added or edited by hand can be overwritten by a later run of the exemptions agent when it sits on a property the agent also produces a claim for.

## Related Features

- [Questionnaires](../README.md)
- [Schedule Tools](./README.md)
- [Schedule A/B Property](./property.md)
- [AI Agents](../autofills/ai-agents.md)
- [Chapter 13 Plan Calculator](./chapter-13-plan-calculator.md)
- [Document Collection](../../document-collection/README.md)
- [Settings](../../../back-office/settings.md)
