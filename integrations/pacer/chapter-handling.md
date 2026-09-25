# Chapter Handling

## Overview

The chapter a case is filed under drives which forms go into the petition and filing packet. This page covers switching a case between Chapter 7 and Chapter 13 before filing, how Glade handles a matter that holds workflows for both chapters, and a Chapter 7-specific means-test behavior.

## Key Behaviors

### Changing the chapter at petition compile time

When a case switches between Chapter 7 and Chapter 13 mid-workflow, the petition must be re-compiled against the new chapter so the schedules and forms match. The pre-compile modal (Documents → **Compile Petition**) makes this switch visible at the moment of filing.

- If the case's district supports more than one chapter, a **Chapter** selector appears in the compile modal next to the filing district banner. Picking a different chapter updates the case data immediately, so the next compile run uses the new chapter.
- After changing the chapter, a **"Chapter changed. Recompile to refresh the petition."** note reminds you to click **Compile** so the regenerated petition reflects the new chapter. The note clears as soon as the new petition finishes compiling.
- If the district only supports a single chapter, or the case is already filed, the selector is read-only and shows the current chapter as a chip — you can see the chapter at a glance but cannot change it.

### Chapter on a matter that holds both a Chapter 7 and a Chapter 13 workflow

A matter can carry workflows for both chapters at once — most often when a case converts, and the original workflow is kept alongside the new one. Each workflow now uses **its own chapter** when Glade builds the filing packet and runs the pre-filing review.

- Previously a single chapter was resolved for the whole group, so one workflow's chapter was applied to the other. A Chapter 13 workflow sitting alongside a Chapter 7 could be prepared against the Chapter 7 template for the district — pulling in Form 122A-1, which the case does not need, and offering no slot for the Chapter 13 Plan.
- The packet preview, the filing packet checklist, and the pre-filing review all read the chapter from the workflow you are working in.
- Submission to the court was already taking the chapter from the case's Schedules questionnaire and was not affected. It was the packet and the review that could disagree with it.
- Closed workflows on the same matter — archived, canceled, or completed — are ignored when Glade works out which chapters a matter currently holds. A workflow that finished as a Chapter 7 no longer makes a live Chapter 13 matter look like a mixed one.

Cases prepared before this was corrected are not rebuilt on their own. If a packet was assembled against the wrong chapter, recompile the petition on the affected workflow and re-run the pre-filing review.

### Chapter 7 individual presumption-of-abuse page

When a Chapter 7 individual case explicitly indicates "no presumption" on B122A-1 line 14, Glade now fills the matching presumption fields on B122A-1 lines 40 and 42 with that same answer instead of leaving them blank. Because the lines are populated, PACER no longer renders the standalone "Presumption of Abuse" page during filing — the filing proceeds without that extra interstitial. Other income and expense fields wiped by the no-presumption answer continue to be cleared as before. The override applies only to Chapter 7 filings; cases on other chapters that carry stale prior answers from an earlier Chapter 7 session are not affected.

## Related Features

- [PACER Integration](./README.md)
- [Pre-filing review](../efiling/pre-filing-review/README.md) — how the review works out a case's chapter.
- [Filing packet](../efiling/filing-packet/README.md)
- [Case numbers](./case-numbers.md) — how a converted case's number is shared across workflows.
