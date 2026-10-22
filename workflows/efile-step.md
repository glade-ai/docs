# eFile Step

## Overview

The eFile module marks the point in a workflow where the case is filed with the court. A firm adds it to a workflow step and chooses which filing it stands for — a complete filing, the first part of a skeleton filing, or the second part of a skeleton filing. The module completes on its own when a matching filing succeeds, and that releases the next step in the workflow. Without it, filing was only implied in a workflow, so steps that come after the petition (or after each part of a skeleton filing) had nothing to wait on and did not advance by themselves.

## Key Behaviors

- **Each module stands for one filing type**, chosen when it is added:
  - **Complete filing** — a new case filed with its full packet (not a skeleton filing).
  - **Skeleton filing, part 1** — a new case filed as a skeleton filing.
  - **Skeleton filing, part 2** — the remaining schedules filed after a skeleton filing.
- **The module completes when a matching filing succeeds.** A filing submitted through Glade that succeeds completes the module. A filing recorded as filed outside Glade completes it too, as long as a case number is recorded with it.
- **Only a matching filing counts.** A Part 1 skeleton filing does not complete a Complete filing module, and vice versa. A Part 2 module completes only on the remaining-schedules filing.
- **Completing the module releases the next step.** The workflow holds at the step until the module is complete, then continues on its own, in the same way a [payment gate](./payment-gates.md) releases a step once it is satisfied.
- **The module records which filing completed it.** Before that filing succeeds, clicking the **eFile** card opens **Electronic filing**. After it succeeds, clicking the card opens the filing that completed the module.
- **A case that was already filed when the step is reached is not held.** If a matching filing has already succeeded by the time the workflow reaches the step, the module is created already complete and the workflow carries on.
- **A filing that lands while Glade cannot check filings is still picked up.** If Glade cannot confirm the filing status when the step is reached, the step is sent anyway with the module pending, and Glade checks again shortly afterwards to catch a filing it missed.
- **A filing update received twice does not complete the module twice.** Once complete, the module keeps the filing that first completed it.
- **The module is visible to the firm only.** Clients do not see or open it in their portal. It is labeled **eFile**.

## Configuration

- In the workflow template editor, add an **eFile** module to a step. Its configuration panel asks for a **Filing type**: **Complete filing** (the default), **Skeleton filing, part 1**, or **Skeleton filing, part 2**. Assignees and conditions are set on the same panel.
- On a live case, **Add module** lists one **eFile** choice for each filing type. A filing type is required when adding the module to a live step.
- On the case, the module card is labeled **eFile**. It shows the filing type, and the case number once the filing has succeeded.
- Use separate modules on separate steps for a skeleton case — one for Part 1 and one for Part 2 — so each filing point advances the workflow independently.
- Adding the module is optional. Workflows and cases without one behave as before, and cases already in progress keep the workflow version they started on.

## Edge Cases & Limitations

- **A filing recorded with no filing type is treated as a complete filing.** For example, a case number entered by hand for a case filed outside Glade, with no filing type, completes only Complete filing modules — not a skeleton Part 1 or Part 2 module.
- A filing recorded as filed outside Glade completes the module only when a case number is recorded with it.
- The eFile module cannot be skipped. The step waits until a matching filing succeeds.
- A failed filing never completes the module or advances the workflow.

## Related Features

- [Payment Gates](./payment-gates.md) — another step module that holds the workflow until a condition is met.
- [Task Templates](./task-templates.md)
- [Triggers](./triggers.md)
- [Status Tracking](status-tracking/README.md)
- [eFiling](../integrations/efiling/README.md)
- [Required documents and skeleton filings](../integrations/efiling/pre-filing-review/required-documents.md#skeleton-filings)
