# Custom Terms

## Overview

Custom terms are agreement templates — such as retainer agreements and engagement letters — that clients must read and accept as a step in a workflow. Firms create and maintain custom terms templates; Glade presents the terms to clients at the designated point in their workflow.

## Key Behaviors

- Custom terms templates are written using a markdown-based editor with two tabs: **Edit** for drafting the content and **Preview** for reviewing the rendered result before saving.
- Variable references in the template (placeholders such as `{{PrincipalAttorney}}` or `{{invoice:RetainerFee}}`) are validated when you publish the template. If any reference cannot be resolved — for example, a typo in the variable name or a case mismatch — publishing is blocked and every invalid reference is listed in one error message so you can correct them in a single pass. This prevents broken placeholders from reaching client-facing retainers.
- Valid references include static fields like client name, attorney name, signature blocks, and case number; workflow context variables defined on any of your workflows; typed dynamic variables registered on the template; and `invoice:<name>` references that match a line item on one of your invoice templates. Variable names are case-sensitive — `principalAttorney` and `PrincipalAttorney` are not interchangeable.
- A formatting toolbar provides one-click actions for: bold, italic, underline, links, bulleted lists, ordered lists, paragraph breaks, and page breaks. Toolbar actions insert formatting at the current cursor position without repositioning you in the document.
- The **Preview** tab renders the terms in Times New Roman, matching exactly what clients see when they review and accept the agreement.
- Page breaks inserted in the editor are preserved in the preview and in the final client-facing document.
- When clients encounter a custom terms step in a workflow, the document is displayed in the same Times New Roman rendering as the editor preview.
- Clients must actively accept the terms to complete the workflow step.

## Configuration

Custom terms templates are created and managed from the firm's template library. Each template requires a name and a body. Once created, a template can be referenced as a step in a workflow template.

## Edge Cases & Limitations

- Custom terms content is read-only for clients — they can accept the presented terms but cannot edit the text.

> TODO: Confirm whether editing a custom terms template affects clients who are already mid-workflow, or only affects new workflow instances started after the edit.

## Related Features

- [Automation Rules](./automation-rules.md)
- [Task Templates](./task-templates.md)
