# Who Can Clear a Blocking Finding

## Overview

A blocking pre-filing finding gates submission until it is resolved or someone signs off on it. Signing off is limited to people accountable for the decision to file over a known problem.

## Key Behaviors

- Signing off on a blocking finding so a filing can proceed is limited to firm owners, firm Admins, Glade Admins, and team members holding a workflow role that is allowed to override filing checks (below). Other team members working the case see the review and everything it found, and can work through the items, but cannot set a blocker aside to let the filing through. A decision to file over a known problem stays with someone accountable for it.
- **A workflow role can be allowed to clear findings.** A firm Admin can mark a workflow role as allowed to override filing checks (see [Workflow Roles](../../../back-office/settings.md#workflow-roles)). A team member who holds that role on a case, as one of the case's current owners, can then sign off on any blocking pre-filing finding on that case, including missing required documents, and can withdraw a sign-off. The bulk sign-off control works for them too. This suits a filing team, such as an ECF department, that needs to file over a known problem without being made firm Admins. The permission doesn't make anyone an Admin, so they still can't delete the case or edit the workflow. Holding the same role on a different case doesn't count, and neither does holding a role that hasn't been marked.
- Each missing required document needs its own sign-off. Signing off on one document does not clear the others, and withdrawing sign-off on one document re-gates only that document.
- A **debtor with no pay advices to file** is the case where this matters most in practice. Setting that requirement aside is reserved to Glade — contact support on a joint case whose second debtor has no pay advices, and the item can be cleared so the filing proceeds. Your firm's own attorneys cannot waive it themselves.

## Edge Cases & Limitations

- The attorney override for missing required documents does not clear the block on a non-PDF file in a slot the court expects as a PDF. See [PDF and image conversion](../filing-packet/file-conversion.md).
- The workflow role permission applies only while the person is a current owner of the case with that role assigned. Removing them from the case, or unassigning the role, removes the permission on that case.
- Some blocking findings cannot be cleared on the case at all — for example the New Mexico non-filing-spouse rule and the New Mexico and Ohio Southern Chapter 7-only rule. See [District rules](./district-rules.md).

## Related Features

- [Pre-filing Review](./README.md)
- [Required documents check](./required-documents.md)
- [District rules](./district-rules.md)
- [Workflow Roles](../../../back-office/settings.md#workflow-roles)
