# Swapping the Debtor and Spouse

## Overview

On a joint bankruptcy case, your team can swap which person is the primary debtor and which is the spouse from the petition workflow's settings. This page covers which cases can be swapped and what a swap changes when the case has linked workflows, such as a triage, retainer and petition workflow on one case.

> TODO: Document the full swap flow — where the action sits in the workflow settings, who can use it, the eligibility checks it runs, and exactly what it changes on the case.

## Key Behaviors

- **Cases with linked workflows can be swapped.** A case that is part of a linked group — for example a petition workflow linked to the triage and retainer workflows before it — can be swapped from the petition workflow's settings, as long as the other checks pass. Previously the swap was refused on any case that wasn't a standalone workflow.
- **A warning is shown for a linked group.** The swap is still allowed, but your team is told the case is part of a linked group before going ahead.
- **Only the workflow you swap from changes.** The swap updates the questionnaires that belong to that workflow, plus questionnaires that belong to the case as a whole rather than to one workflow. Questionnaires on the linked triage or retainer workflows are left exactly as they were.

## Edge Cases & Limitations

- The intake questionnaires on the other workflows in the group keep the original primary debtor and spouse. Update them separately if they need to match.

> TODO: Confirm the wording of the linked-group warning.

## Related Features

- [Status Tracking](./README.md)
- [Switching a Case to Another Workflow](./switching-workflows.md)
- [Questionnaires](../questionnaires/README.md)
