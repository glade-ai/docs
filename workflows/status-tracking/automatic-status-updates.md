# Automatic Status Updates

## Overview

A case's status and progress change automatically as its workflow steps complete. Workflow designers choose which steps move a case to which status, Glade recalculates progress after every trigger, and a case moves to Completed on its own when every step is done. This page covers step-driven status changes, the Case Filed step, progress recalculation, and automatic completion.

## Key Behaviors

- **Automatic status updates**: When a workflow trigger completes, the case status can automatically update to a specific value. This is configured per workflow step, so workflow designers control exactly when status transitions happen.
- **Automatic status update when a case is filed**: A case that is e-filed and comes back with a court case number can move to your firm's filed status on its own, instead of waiting for someone to change it by hand. Your firm adds a **Case Filed** step to its workflow template and sets that step's status to whichever status it uses for filed cases — firms name this differently ("Case Filed", "Filed", the built-in "Filed and Pending"), and the step points at whichever one you use. Cases filed manually with a case number recorded count the same as ones filed through PACER.
  - This applies to cases started after your firm publishes a template containing the step. Cases already in flight stay on the template version they started on and continue to be moved by hand; there is no retroactive update.
  - It runs once. A re-filing, or a filing deficiency resolved later, does not move the case backward or re-apply the status, and a case that has already moved past the filed status stays where it is.
  - Only the case that was filed moves. If the same client has two open matters that both carry the step, filing one leaves the other alone.
- **Automatic progress calculation**: After each trigger completes, the system recalculates the case's progress, step counts, and task counts based on what has been completed so far.
- **Automatic completion**: When all workflow steps are done, the system automatically transitions the case to "Completed" status. Attorney-case type workflows may have specialized completion logic for certain case types.

## Configuration

- **Status per workflow step**: Individual workflow steps can specify a status that the case automatically transitions to when that step's trigger completes.
- **Case Filed step**: A workflow template can include a **Case Filed** step whose status is applied when the case is e-filed and receives a case number. Set the step's status to your firm's own filed status; no other configuration is required, and the step is added to a template like any other.
- **Workflow type**: The workflow type ("basic" or "attorney case") affects how automatic status progression and completion logic behave.

## Edge Cases & Limitations

- The Case Filed step is not retroactive: cases already in flight when the template is published continue to be moved by hand.
- The Case Filed step runs once per case and never moves a case backward.

## Related Features

- [Status Tracking](./README.md)
- [Case Status](./case-status.md)
- [Triggers](../triggers.md) — trigger completion drives automatic status updates
- [Automation Rules](../automation-rules.md)
- [PACER Integration](../../integrations/pacer/README.md)
