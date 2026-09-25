# Create Task Actions

## Overview

As well as sending an email, an automation can create a task on the case when it fires, so the work lands in someone's queue instead of only in an inbox. Who that task is assigned to can depend on the notice, using **assignment rules**.

## Key Behaviors

- The task's **assignees** are chosen the same way as email recipients — case-party tokens (`debtor1`, `debtor2`, `attorney`) and team members at your firm. At least one assignee is required.
- **Due in** sets the task's due date as a number of days after the notice date, calculated in your firm's timezone. Leave it blank for no due date.
- The task carries a title and description, which support the same tokens as the email subject and body (see [Email Tokens](./email-tokens.md)). The same case-party and hearing details are available to **Create task** actions, so a task raised from a 341 notice can state the meeting date, time, and join details in its description.
- Assignees are notified through the normal task notifications and the task appears in their inbox, exactly as a task created any other way.
- A create-task action is **skipped** when the notice is not linked to a workflow, or when none of its assignees resolve at fire time (for example because every assignee was a team member who has since been removed). Glade never creates a task with no assignee.
- Team member assignees are checked against your firm at fire time; anyone no longer at the firm is dropped.
- Two create-task actions on one automation produce two separate tasks.

### Assignment rules

Each rule combines up to three conditions with a list of the people to assign:

| Condition | Matches on |
|-----------|-----------|
| **Chapter** | Chapter 7 or Chapter 13, compared the same way as the automation's own chapter filter |
| **Judge** | The judge on the notice, compared by initials and case-insensitive, the same way as the automation's judge filter |
| **Trustee** | The trustee named on the notice. Trustee names are free text, so they are compared ignoring capitalization and surrounding spaces |

This lets one automation route work the way your firm actually divides it — Chapter 13 notices to the Chapter 13 paralegal, notices in front of one judge to the person who covers that judge, anything from a particular trustee to both.

**How the conditions combine:**

- Each condition is joined to the next by **and** or **or**, and the rule is read strictly left to right: chapter, then judge, then trustee. There is no precedence between **and** and **or** — "chapter **and** judge **or** trustee" means "(chapter and judge) or trustee", never "chapter and (judge or trustee)". Order your conditions with that in mind.
- A condition you leave blank drops out of the rule entirely, along with the operator that joined it. It is not treated as a match. A rule with a chapter and a trustee joined by **or**, and no judge, matches a notice that is either in that chapter or from that trustee.
- A rule with all three conditions blank always matches. Use one as a catch-all so notices that fit none of your specific rules still land with someone.

**How assignees are worked out when the automation fires:**

- Every rule is evaluated against the notice, and **one task** is created — not one per rule and not one per person.
- The assignees from every rule that matched are combined. Someone named by two matching rules is assigned to the task once.
- If no rule matches the notice, no task is created and the run is recorded as skipped.
- If rules matched but none of their assignees can be resolved — for example every one of them was a team member who has since been removed — no task is created and the run is recorded as skipped.
- An automation with two separate task actions still creates two tasks, as before.

The trustee picker is populated from the trustees who have actually appeared on PACER notices for your firm in the last 12 months, most frequent first — the same way the judge picker works.

Automations set up before assignment rules existed keep working unchanged. Their single list of assignees reads as one rule with no conditions, so the same people are assigned on every firing until you add conditions.

## Configuration

| Setting | Description |
|---------|-------------|
| Assignment rules | For an automation that creates a task: a list of rules, each with an optional chapter, judge, and trustee condition joined by **and**/**or**, plus the people to assign. At least one assignee per rule. |
| Task assignees | For a **Create task** action: case-party tokens and team members. At least one is required; literal email addresses are not available here. |
| Task due in | For a **Create task** action: the number of days after the notice date that the task is due, in your firm's timezone. Optional. |

## Edge Cases & Limitations

- Tasks created by an automation appear in the inbox and in the newer task views. They may not yet appear in the older dashboard task lists, which show only a fixed set of task kinds.
- A **Create task** action needs the notice to be linked to a workflow. Court notices that never matched a workflow — the majority of notices for many firms — cannot raise a task, so an automation whose only action is Create task will show runs as skipped on those notices. Pair it with a **Send email** action if someone should still be told.
- Conditional logic inside a single automation is limited to assignment rules on a task action — they decide *who* a task goes to, not whether the automation fires or what the email says. The automation's own trigger has no branching; use separate automations for separate scenarios.
- Assignment-rule conditions cover chapter, judge, and trustee only. There is no condition on other notice details.
- Assignment-rule conditions are evaluated strictly left to right with no operator precedence. A rule that mixes **and** and **or** may not mean what it reads like at a glance — check the grouping described above.
- A rule whose conditions are all blank matches every notice. Leaving a rule empty by accident assigns its people to every firing.
- Re-sending an automation's email does not run its **Create task** action again, so a run that failed to create its task is not repaired by a re-send.

## Related Features

- [Court Notice Automations](./README.md)
- [Automations and Actions](./automations-and-actions.md)
- [Triggers and Filters](./triggers-and-filters.md)
- [Email Tokens](./email-tokens.md)
