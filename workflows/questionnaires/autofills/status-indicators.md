# Autofill Status Indicators

## Overview

Fields populated by autofill show a status indicator so you can see where the value came from and whether it is current. This page covers each indicator state, what a field shows while a background autofill is still working, and how the indicator reads on fields that both sync with case data and autofill.

## Key Behaviors

### Indicator states

- **Synced** / **Synced with [source]** — The field value matches the source data and is up to date. Shown with a green checkmark (or the Glade AI icon for AI-sourced values).
- **Out of sync** — The source data has changed since the field was last filled, so the autofilled value may be stale. Shown with an amber warning icon. You can re-run the autofill to update the value.
- **Error** — The autofill encountered a problem and could not set the value. Shown with a red warning icon and a re-run button.
- **Edited** — You have manually changed the value after it was autofilled. Shown with a violet pencil icon and a re-run button if you want to restore the autofilled value.
- **Not yet run** — The autofill has not been applied yet. Shown as a blue **Import Autofill** pill. Click it to trigger the autofill immediately.

A locked field shows a lock icon instead — see [Locked Fields](./locked-fields.md).

### When an autofill is still working

Some autofills are worked out in the background rather than the moment you click, and the field marks itself as recalculating while that happens.

- **A background autofill that fails, or that finds nothing to fill the field with, now finishes.** It settles on the state that matches what happened — an error you can re-run, or a completed run that wrote no value. Previously a field in either position stayed marked as recalculating indefinitely. Reloading the questionnaire brought the same state back, there was no re-run control to click, and the only way past it was to type the value in by hand.
- **The recalculating state is visible to everyone working in the questionnaire**, not only the person whose edit set it off. Two people preparing the same form see the same field marked as still working, so neither types over a figure that is about to arrive.
- **The field marks itself as working as soon as the AI agent starts, not once the answer comes back.** Previously a field showed only its autofill label for the whole run and then jumped to its value with nothing in between. On a new questionnaire where several agents run one after another, that could be a minute or more with nothing on the form to say anything was happening — long enough for a preparer to read the field as stuck and type over it. This applies to a field that has never been answered as well as one that already holds a value.
- **A background run is no longer abandoned when the form reorganizes around it.** Editing a questionnaire while an agent is working rebuilds the form behind the scenes, and a run in flight used to be dropped each time. A field whose agent takes longer than the gap between edits could be left permanently blank — no value, no error, and no re-run control to click. The reported case was the filing-court question. A run now carries across and its answer is accepted when it arrives, unless the row it belongs to has been deleted or someone has since answered the field themselves.
- **The routine background lookups do not show a spinner**, because they re-attempt on every save and would flicker on many fields at once. A lookup you re-run yourself does show one on the field you clicked, and a lookup that fails records its reason either way.

> TODO: Confirm which questionnaire templates work their autofills out in the background. This section applies where values are calculated on Glade's side rather than in the form as you type, and the source change does not establish which templates are set up that way.

### Fields That Both Sync With Case Data and Autofill

Some fields are set up to sync with case data *and* to be populated by an autofill — most of the income lines on Schedule I are in this position, since they are filled from the Income Organizer. On these fields the indicator names the source the current value actually came from:

- A value that came from an autofill reads as populated from that source (for example, **Populated from Internal data**) and keeps its re-run control, so you can refresh it. Clicking the indicator opens the autofill's explanation panel.
- A value that case data genuinely produced still reads **Synced with case data** and opens the case data view, and a value you have typed over still reads **Manually overridden** with the option to revert.

Previously any field with a case data connection claimed to be synced with case data even when something else had filled it, and the re-run control was hidden — so on a Schedule I income line filled from the Income Organizer, there was no way to refresh the value and the stated source was wrong. Where the value is refreshed from and where edits are saved has not changed; only the reported source and the availability of the re-run control.

> TODO: Confirm the in-product wording of the "Populated from Internal data" label — the underlying source name may read differently to a preparer.

Schedule I and Means Test lines calculated by the Income Organizer name the calculator as their source — see [Manual Overrides](./manual-overrides.md#overriding-a-schedule-i-or-means-test-figure-the-calculator-produced).

## Edge Cases & Limitations

- A field that is connected to case data but has never been populated still reports itself as synced with case data and offers no re-run control, because there is no value on it whose source could say otherwise. Fill or autofill the field once and the indicator reports its real source.

## Related Features

- [Questionnaires](../README.md)
- [Autofills](./README.md)
- [How Autofills Work](./how-autofills-work.md)
- [AI Agents](./ai-agents.md) — the explanation beside an AI-filled answer
- [Case Data Sync](../case-data/case-data-sync.md)
