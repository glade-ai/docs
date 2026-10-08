# Handoffs

## Overview

A workflow template can require a **handoff** before a step starts: the case must have an owner who holds a specific role, such as an attorney or a paralegal. Until someone with that role is assigned, the case waits at that step. An **Assign <role>** task on the case tells staff what the case is waiting for. This page covers how that task behaves and how to find every case currently waiting on a handoff.

## Key Behaviors

### The Assign <role> task

- **The task exists for as long as the case is waiting.** Whenever a case starts waiting on a handoff, Glade makes sure an open **Assign <role>** task is on it. Previously about half of the cases waiting on a handoff had no open task. Staff saw "all tasks are done" and could not tell why the next step had not started.
- **A case with no owners still gets the task.** It is created unassigned. Previously the task was skipped when the case had no owners at all.
- **The task can't be ticked off without a handoff.** Completing an **Assign <role>** task is refused while no owner on the case holds a role the step accepts. Assign someone with the role, and the task closes.
- **Filed and Pending no longer closes it.** Moving a case to Filed and Pending closes the case's other tasks but leaves an unmet **Assign <role>** task open. Moving a case to Completed, or archiving it, still closes every task.
- **Any accepted role clears the step.** Where a step accepts more than one role (for example, "attorney or paralegal"), assigning an owner with either role closes every **Assign <role>** task for that step. Previously the task for the other role could stay open forever.
- **The gate itself is unchanged.** The next step still waits until the handoff is met.

### Finding cases waiting on a handoff

- The workflows list and custom reports can be filtered to cases that **need a handoff**. These are the same cases that show as waiting on a handoff on the case screen.
- Two columns describe the wait:
  - **Handoff role**: the role or roles the case is waiting for.
  - **Handoff since**: when the case started waiting. When a case is waiting at more than one step, this is the oldest wait.
- Sorting by **Handoff since** lists the longest-waiting cases first. Cases that are not waiting on a handoff sort last whichever direction you sort.
- The CSV export includes the handoff columns and respects the handoff filter, so a filtered export contains only the cases waiting on a handoff.

> TODO: Confirm where the "handoff needed" filter and the Handoff role / Handoff since columns appear in the dashboard (workflows list, custom reports, or both), and how the case screen names the missing role.

## Configuration

- **Owner assignments on workflow steps.** Handoffs are set up on your firm's workflow template, by choosing which roles a step needs before it starts. See [Task Templates](../task-templates.md).

## Edge Cases & Limitations

- The task changes apply to cases that start waiting on a handoff, or whose **Assign <role>** task changes, from now on. Cases that were already waiting without an open task were not given one automatically. Use the handoff filter to find them.
- A role that has been deleted from your firm is not listed in the **Handoff role** column.

## Related Features

- [Tasks](./tasks.md)
- [Case Status](./case-status.md)
- [Workflow List](./workflow-list.md)
- [Task Templates](../task-templates.md)
- [Custom Reports](../../back-office/reporting/custom-reports/README.md)
