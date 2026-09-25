# AI Agents

## Overview

AI agents autofill fields and groups of related fields by inferring values from uploaded documents, prior responses, and the rest of the case — for example property exemptions, schedule classification, vehicles, secured debts, or the filing district in a bankruptcy case. This page covers how agent-filled fields behave, re-running an agent, and the explanation recorded beside each answer.

## Key Behaviors

### Re-running preserves your work

When an AI agent autofills a group of related fields (for example, property exemptions in a bankruptcy case), re-running the agent preserves any values you have already entered or confirmed. The agent incorporates existing data rather than overwriting it, so you can re-run an analysis after adding new items without losing prior work.

Manual edits to fields in a list also stick when the AI auto-runs after rows have been added, removed, or reordered. For example, on the Bankruptcy Schedules questionnaire, the schedule classifier may run repeatedly as the form changes — moving a creditor from Schedule D to Schedule F by hand will not be reverted by a later automatic run.

### Fields an Agent Is Meant to Fill Now Actually Fill

Every field an AI agent is set up to produce is filled by that agent. Previously only a subset were: a field could be listed as one of an agent's outputs and still never be filled, because the field itself had not separately been marked as AI-filled. Roughly three in four agent-filled fields were in that position, so this was the ordinary case rather than a rare one.

- **Nothing on the form indicated a problem.** The field simply sat empty — no value, no error, no re-run prompt — and looked the same as a question nobody had got to yet. Preparers filled these in by hand without knowing an agent was supposed to.
- **These fields now behave like any other AI-filled field**: they populate as the answers they depend on are entered, show the usual status indicator, carry the agent's explanation, and can be re-run.
- **Expect more fields to fill themselves on questionnaires that use agents**, including inside lists — an agent-filled column on a long creditor or property list now produces a value for every row rather than none.
- **A failed run now says so.** When the AI could not produce a value for one of these fields, the field reported a *lookup failed* message that pointed at a filing-district lookup which was never involved. It now reports the AI run as the thing that failed, which is what the re-run control retries.
- Values already entered by hand are not disturbed — the protection described under [A Value You Typed Is Not Re-Derived](./manual-overrides.md#a-value-you-typed-is-not-re-derived) applies to these fields as it does to every other.

### Re-running an agent over a list

The agents that fill a whole list — exemptions on Schedule C, vehicles, secured debts, mortgages, and arrearages — **replace** the rows from the previous run rather than adding a second set alongside them.

- Running the exemptions agent a second time used to leave the earlier claims in place underneath the new ones, so each run doubled the Schedule C list and the extra rows had to be deleted one at a time. The same could happen on the other list agents and when importing into a list.
- **Duplicates already sitting on a case are not cleaned up.** If a list on one of your cases was doubled by an earlier re-run, delete the extra rows once; re-running the agent from now on will not add more.
- A re-run **updates the rows that are already there** instead of rebuilding the list from scratch, so an exemption claim stays attached to the property it was claimed against. The generated Schedule C, the property's link to its exemption, and the Chapter 13 liquidation analysis all continue to point at the right claim after a re-run.
- Changing a claim from a custom amount to the property's full market value clears the amount and the explanation that went with it, rather than leaving the earlier figure on the row.

Two things to be aware of when you re-run:

- A claim you added or edited by hand can be overwritten by a later run of the agent when it sits on a property the agent also produces a claim for. Values elsewhere in the questionnaire are untouched.
- Re-running the vehicles agent when it finds nothing to claim leaves the previous run's rows in place. Clear them yourself if the earlier result no longer applies.

For exemptions-agent specifics — firm instructions and claims at 100% of fair market value — see [Exemptions Calculator](../schedules/exemptions-calculator.md#the-exemptions-agent).

### The Filing District an Agent Works Out

Where the filing district is filled in for you, it is worked out from the **ZIP code of the client's first residence address** rather than from the address as a whole.

- Handing over the whole address let other parts of it contradict the ZIP code. A city that sits across a district boundary from the ZIP code beside it could produce the wrong district, and nothing on the form indicated a disagreement had been resolved the wrong way.
- **A case with no residence address, or a residence with no ZIP code, produces no district at all** rather than a guess. An empty field is the prompt to enter the district yourself.
- The first row of the residence list is the one used. Removing a later row does not change which row counts as the first.
- A ZIP code beginning with a zero is read as written.

The filing district is worth re-checking on cases prepared before this change, along with the figures that follow from it. The median income comparison and the means test lookups are all selected by district, so a district that came out wrong carried into those figures as well.

### The Explanation Beside an AI-Filled Answer

Clicking an AI-filled field's status indicator opens the explanation of how the agent reached the value. The explanation is recorded at the same moment as the answer it describes, so the two always refer to the same run.

- Previously the explanation could be left behind — the answer updated on each automatic run while the explanation stayed at whatever the last hand-triggered re-run had recorded. A reviewer reading it was reading the reasoning for an answer that was no longer on the field.
- Where two runs of the same agent overlap, a run that finishes against a version of the form that has since moved on writes neither an answer nor an explanation. A newer answer is not replaced by an older one, and its explanation is not either.
- An agent that fills several fields at once records each field's explanation against that field, so accepting one field's result does not disturb another's.

## Edge Cases & Limitations

- A hand-added or hand-edited claim on a property the agent also produces a claim for can be overwritten by a later run (see above).
- Duplicate rows left on a list by earlier re-runs are not cleaned up automatically.

## Related Features

- [Questionnaires](../README.md)
- [Autofills](./README.md)
- [Autofill Status Indicators](./status-indicators.md)
- [Manual Overrides](./manual-overrides.md)
- [Exemptions Calculator](../schedules/exemptions-calculator.md)
- [Field Behaviors](../filling-out/field-behaviors.md) — debtor county and court division
