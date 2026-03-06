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

## Sources of truth

When filling in a feature file, draw from:
- Merged pull requests that touch the relevant code
- Linear issues and project descriptions
- Existing code behavior (read the code, don't guess)

Do not invent behaviors. If something is unclear, leave a `> TODO:` blockquote instead of guessing.

## Updating existing docs

When a merged PR changes a feature:
1. Update only the sections affected by the change.
2. Add a `CHANGELOG.md` entry.
3. Do not rewrite sections that were not affected.

## Tone

- Technical, factual, concise.
- Present tense: "The form validates..." not "The form will validate..."
- No marketing language.

## What not to do

- Do not describe internal implementation details (database schema, function names) unless directly relevant to behavior.
- Do not copy-paste PR descriptions verbatim — summarize the resulting behavior.
- Do not add sections beyond the structure above without a clear reason.
