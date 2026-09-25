# Agents

Instructions for AI agents filling in or updating feature documentation.

## Feature file structure

Every feature file must contain these sections in order:

```markdown
# Feature Name

## Overview
One paragraph. What this feature does and who uses it.

## Key Behaviors
Bulleted list of the most important things the feature does. Focus on observable behavior, not implementation.

## Configuration
Options, settings, or inputs that affect how the feature works. Omit if not applicable.

## Edge Cases & Limitations
Known constraints, unsupported scenarios, or gotchas.

## Related Features
Links to other feature files that are closely related.
```

## One topic per doc — split and sub-folder

Docs are read by people (and the Glade MCP `docs_*` tools) looking for one specific answer — "how does the exemptions calculator work?" — so each file covers **one topic**. A reader should never have to scroll a 1,000-line page to find it.

**Layout.** A simple feature is a single file: `<domain>/<feature>.md`. A feature with several distinct topics is a folder:

```
workflows/questionnaires/
  README.md                 # feature overview: Overview + a "## Topics" list linking every sub-doc
  exemptions-calculator.md  # one topic, using the section structure below
  petition/                 # optional group folder (max one extra level) when 3+ topics cluster
    README.md               # short overview + Topics list
    draft-petition.md
```

- The folder's `README.md` is the feature's entry point (MCP path `workflows/questionnaires`); each sibling is a topic (MCP path `workflows/questionnaires/exemptions-calculator`).
- Every topic file uses the feature file structure below.
- Filenames are kebab-case and descriptive.

**When to split.** Promote a single-file feature to a folder (move `<feature>.md` → `<feature>/README.md`, then move topics out) when **any** of these is true:
- the file exceeds ~250 lines or ~20KB;
- it has 3+ `###` sections that each describe a distinct capability (a calculator, a report, an import flow) rather than facets of one;
- you are about to add a new, distinct capability to it.

**Adding to an existing feature.** A new capability gets its **own topic file** in the feature folder — do not append another `###` section to the bottom of a long doc. Only edit an existing topic file when the change is about that same topic. Before creating a file, check whether the topic already has one (including in other domains) and update it instead of duplicating it.

**Keep indexes current.** Every new file is linked from its parent: a topic from its folder `README.md` "Topics" list, a single-file feature or a feature folder from the domain `README.md`. Relative links must match the file's depth (`../../payments/invoices.md` from inside `workflows/questionnaires/`).

## Sources of truth

When filling in a feature file, draw from:
- Merged pull requests that touch the relevant code
- Linear issues and project descriptions
- Existing code behavior (read the code, don't guess)

Do not invent behaviors. If something is unclear, leave a `> TODO:` blockquote instead of guessing.

## Updating existing docs

When a merged PR changes a feature:
1. Update only the sections affected by the change.
2. In the PR description, add a changelog block between `<!-- changelog -->` and `<!-- /changelog -->`. Use **one sub-section per domain/feature** (e.g. `### payments/invoices` then bullets; `### other/feature` then bullets). Content is free-form (summary, source PRs, Linear, Notion — whatever you used). **Both tags are required**; the workflow inserts only the content between them into CHANGELOG when the PR is merged. Do not edit CHANGELOG.md in the branch. A PR check requires both tags and non-empty content between them; if the block is missing or incomplete, the check fails and the merged CHANGELOG would show "no details available".
3. Do not rewrite sections that were not affected.

## Tone

- Technical, factual, concise.
- Present tense: "The form validates..." not "The form will validate..."
- No marketing language.

## What not to do

- Do not describe internal implementation details (database schema, function names) unless directly relevant to behavior.
- Do not copy-paste PR descriptions verbatim — summarize the resulting behavior.
- Do not add sections beyond the structure above without a clear reason.

<!-- shared-begin: pr-creation -->
## Pull requests

- Create as a **draft** (`--draft`) until ready for review
- Default to `--label release-minor`; use `release-patch` for fixes/docs only, `release-major` for breaking changes
- PR description must explain **why** — the motivation behind the change, not just what changed
- CI requires exactly one release label (`release-patch`, `release-minor`, or `release-major`) or checks will fail
<!-- shared-end: pr-creation -->
