# Triggers and Filters

## Overview

An automation's trigger decides whether it fires on an incoming court notice. The trigger combines a required notice type with optional chapter, judge, and trustee filters, and is evaluated again when a notice that arrived unlinked is later linked to its case.

## Key Behaviors

A trigger has four parts. All must match for the automation to fire:

- **Notice type** (required) — exact match against the classified PACER notice type. For example, an automation with match type "Notice of Hearing" fires only on notices classified as "Notice of Hearing".
- **Chapter** (optional) — restricts the automation to a specific chapter (Chapter 7 or Chapter 13). When left blank, the automation matches any chapter.
- **Judge** (optional) — restricts the automation to a specific judge (matched by judge initials, case-insensitive). When left blank, the automation matches any judge.
- **Trustee** (optional) — restricts the automation to notices naming a specific trustee. When left blank, the automation matches any trustee.

The judge picker is populated from the judges who have actually appeared on PACER notices for your firm in the last 12 months, sorted by how often they appear so the most common judges are at the top.

Because the notice type match is exact, what an automation fires on depends on how the notice was classified — see [Notice Classification](./notice-classification.md).

### Filtering by trustee

Trustee was already available as a condition for deciding *who* a created task is assigned to. As a trigger filter it decides something different: whether the automation runs at all. Use it when a trustee needs different wording — or no message — from the others.

- **One trustee per automation.** To cover two trustees with different treatment, set up two automations. To cover two trustees with identical treatment, leave the filter blank and use the chapter or judge filters to narrow instead.
- The trustee filter is combined with the chapter and judge filters — a notice has to satisfy every filter that is set.
- Matching ignores capitalisation and surrounding spaces, but is otherwise an exact match on the trustee's name as it appears on the notice.
- **A notice that names no trustee does not match an automation with a trustee filter set.** If a trustee-specific automation is not firing where you expect, check that the notices in question actually carry a trustee name.
- Existing automations are unaffected. An automation with no trustee filter continues to match every trustee, as it always has.

### Notices that arrive before the case is linked

A court notice can reach Glade before it has been matched to a case. Case-opening notices do this by construction: the court issues its notice the instant a petition is filed, so it routinely arrives a few seconds ahead of the case number Glade matches it on. While a notice is unlinked there is no case for the chapter and judge filters to read, so an automation carrying either filter could not match it — and the notice then linked to its case moments later and looked entirely correct in the notice list, with nothing to show that its automation had been abandoned.

- **An automation is evaluated again when its notice is linked to a case.** A notice that could not be matched while it was unlinked gets a second evaluation as soon as the link exists, so the automation fires as intended.
- Linking never causes a second firing. An automation that already ran on the notice is not run again.
- **Voluntary Petition automations were affected most.** An automation with a chapter or judge filter fired on a minority of the case-opening notices it should have; one with neither filter was unaffected, because it had nothing on the case to check.
- Nothing on your existing automations needs changing.

## Configuration

| Setting | Description |
|---------|-------------|
| Match type | Notice type to match (exact). |
| Chapter | Chapter 7, Chapter 13, or any. |
| Judge | Specific judge or any. |

## Edge Cases & Limitations

- The match type is exact. Notices with a slightly different classification do not match — set up additional automations for related notice types if needed. This matters where a single type has been split into several: an automation that watched for means test and current-monthly-income notices needs one automation per form to keep the same coverage.
- Notices that were missed while they were still unlinked are not fired retroactively. If your firm relies on a filtered Voluntary Petition automation, expect it to start firing where it previously stayed silent, and handle any earlier case-opening notices by hand.
- Conditional logic inside a single automation is limited to assignment rules on a task action — they decide *who* a task goes to, not whether the automation fires or what the email says. The automation's own trigger has no branching; use separate automations for separate scenarios.

## Related Features

- [Court Notice Automations](./README.md)
- [Notice Classification](./notice-classification.md)
- [Automations and Actions](./automations-and-actions.md)
- [Create Task Actions](./create-task-actions.md) — trustee, chapter, and judge as assignment-rule conditions
