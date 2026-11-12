# Workflow Cards

## Overview

The workflows widget and the custom-report widget can show cases as cards. Two of the figures on each card measure real case progress: documents outstanding and questionnaire completion.

## Key Behaviors

- **Documents outstanding** shows how many of the files a case's checklists require are still not complete, out of the total required — for example, 3 of 7. It counts required file slots across the case's active checklists. A file still marked incomplete or needing action counts as outstanding.
  - Skipped checklists, checklists still waiting on their workflow step, and optional file slots are not counted.
  - Checklists built from a template your firm has since archived are still counted, because they still appear in the case's checklist panel. The card and the panel therefore agree.
  - Previously this figure showed the client's pending task count.
- **Questionnaire** shows how far along the questionnaire the petition is generated from is — the bankruptcy schedules, or the emergency filing questionnaire. The percentage is required visible questions answered out of required visible questions. This is the same rule the questionnaire uses for its section progress, so the card matches what you see when you open the questionnaire.
  - A case linked to another case in the same group, such as a retainer case linked to the petition case, shows the petition case's questionnaire.
  - Skipped questionnaires are not counted.
  - Previously this figure showed overall task progress.

## Edge Cases & Limitations

- The **Documents outstanding** and **Questionnaire** figures on workflow cards appear only to firm staff. If the checklist counts can't be loaded, the cards show "—" for that figure and the rest of the list still loads.
- The **Questionnaire** percentage is only available for questionnaires on Glade's current questionnaire engine. For other questionnaires, or before progress has been calculated, the card shows the questionnaire's status instead of a percentage. Progress updates shortly after answers are saved, not instantly.

## Related Features

- [Dashboards](./README.md)
- [Custom Reports](../custom-reports/README.md)
