# Contributing

## How docs stay current

A daily hook scans merged pull requests across the Glade codebase and raises a PR here for any feature docs that need updating. Manual edits are also welcome.

## Adding a new domain

1. Create a folder with a kebab-case name (e.g. `my-domain/`).
2. Add a `README.md` using the structure of an existing domain README.
3. Link the new domain in the root `README.md`.

## Adding a new feature

1. Create a `<feature-name>.md` file inside the relevant domain folder.
2. Use the section structure defined in `AGENTS.md` as a template.
3. Link the new file from the domain `README.md`.

## Promoting a feature to a folder

Each doc covers one topic. When a feature outgrows one page — over ~250 lines / ~20KB, or 3+ distinct capabilities — split it (see "One topic per doc" in `AGENTS.md` for the full rule):

1. Create a folder with the feature name.
2. Move the existing `.md` to `<feature>/README.md` and trim it to an overview plus a `## Topics` list.
3. Move each distinct topic into its own `<feature>/<topic>.md` alongside it. Group 3+ closely related topics into one sub-folder (with its own `README.md`) if it helps; don't nest deeper than that.
4. Update the domain `README.md` link to point to `<feature>/README.md`, and fix relative links in moved files.

New capabilities of an already-split feature get a new topic file, not a new section appended to an existing one.

## Changelog

CHANGELOG is updated automatically when a PR is merged. When you open a PR that changes doc content, include in the PR description a changelog block between `<!-- changelog -->` and `<!-- /changelog -->` with **one sub-section per domain/feature** (e.g. `### domain/feature` plus bullets). Both tags are required; content between them is inserted into CHANGELOG on merge. A PR check will fail if the block is missing or incomplete (e.g. missing closing tag or empty content). See the format at the top of `CHANGELOG.md`.

## Style

- Write for a technical audience (engineers and product managers).
- Present tense, active voice.
- Keep descriptions factual — no marketing language.
- Link to related features where relevant.
