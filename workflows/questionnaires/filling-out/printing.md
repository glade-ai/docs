# Printing a Questionnaire

## Overview

A questionnaire can be printed to paper or to PDF from your browser's own print command, which is how firms produce a copy to read through with a client or keep in a paper file. Printing works on a questionnaire opened on its own page and on one open in a panel alongside the rest of the case.

## Key Behaviors

- **Every field in the section you are looking at prints**, including fields on subsections you do not currently have open. Previously the printout carried only the subsection tab that happened to be selected, so a checklist printed from one tab silently left the rest of its questions out.
- **The printout runs to as many pages as it needs.** It previously stopped at whatever fitted on one screen, so anything below the fold was missing. A questionnaire opened in a panel previously printed only what happened to be on screen — roughly one page of fields — or came out with none of the form's layout.
- **Only the questionnaire prints.** The dashboard around it, the navigation, the subsection tabs, and the PDF preview toggle are all left off the page. When the questionnaire is open in a panel, the panel's own surroundings — navigation, the close button, and the chrome around the form — are left off the printed pages too.
- **Printing a form opened over the case's workflow page.** When a questionnaire is open on top of the case's workflow page, pressing **Command+P** (Mac) or **Ctrl+P** (Windows) opens the questionnaire in a window of its own and prints it from there, with every subsection of the open section included. The window closes once you close the print dialog, and the form you were working in is left as it was. Previously the print command printed the workflow page behind the form — the workflow steps and dashboard navigation — instead of the answers.
- **Your place is kept.** Whichever subsection tab you had open is still open after you close or cancel the print dialog.
- Printing covers the **section currently open**. A questionnaire split across several sections prints one section at a time — open the next section and print again.
- This applies to submitted and completed questionnaires. A form your team is reviewing prints the same way as a completed one: a questionnaire a client has submitted for review can be printed by a team member who can edit it, which previously produced the same partial page.

## Edge Cases & Limitations

- A questionnaire still in progress prints the way it always did.

> TODO: The original doc described printing in two places — one scoped to submitted and completed questionnaires ("one still in progress prints the way it always did") and one stating a questionnaire can be printed from a panel without that restriction. Confirm whether the full-section printout now also applies to in-progress questionnaires.

## Related Features

- [Questionnaires](../README.md)
- [Filling Out Questionnaires](./README.md)
- [Layout and Navigation](./layout-and-navigation.md)
- [Generating a Draft Petition](../petition/draft-petition.md) — for a printable petition PDF
