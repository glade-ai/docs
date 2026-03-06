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

When a feature grows complex enough to need multiple pages:

1. Create a folder with the feature name.
2. Move the existing `.md` to `<feature>/README.md`.
3. Add sub-feature files alongside it.
4. Update the domain `README.md` link to point to `<feature>/README.md`.

## Changelog

Update `CHANGELOG.md` with every PR that changes doc content. Use the format defined at the top of that file.

## Style

- Write for a technical audience (engineers and product managers).
- Present tense, active voice.
- Keep descriptions factual — no marketing language.
- Link to related features where relevant.
