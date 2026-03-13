# Project Memory File Guides

## Read This File When

- You are creating `.project-memory` for the first time.
- You are refreshing generated project memory after substantial repo changes.
- You are updating curated project memory after a substantial task.
- You need a reminder of which file should contain which kind of information.

## File Purposes

### `.project-memory/README.md`

Use as the entry page and read order.

This file is managed and may be refreshed directly by the agent to keep links and read order aligned.

Keep it short:

- what `.project-memory` is for
- which files to read first
- which files are generated vs curated

### `.project-memory/generated/project-summary.md`

Use for rebuildable project description.

Include:

- what the repository appears to do
- the main technology or build hints
- top-level module and directory map
- key entrypoints or code roots worth reading

Do not store milestone history or architectural justification here.

### `.project-memory/generated/feature-index.md`

Use as a navigation-first index.

Include:

- feature or area name
- why that area matters
- which paths, classes, or folders to inspect first
- extra notes about entrypoints, handlers, jobs, pages, or integrations

This file can start as code-navigation heuristics and become more accurate over time.

### `.project-memory/generated/development-playbook.md`

Use for reusable development methodology, example code paths, and high-value implementation patterns.

Rules:

- keep the auto-managed section current with what the repo actually shows
- preserve the manual accumulation section
- prefer examples that reduce future re-scanning cost

### `.project-memory/memory/milestones.md`

Use for completed or committed stage-level outcomes.

Each milestone should capture:

- date or period
- milestone name
- what changed
- impact scope
- key code paths
- follow-up or remaining work

### `.project-memory/memory/decisions.md`

Use for durable decisions and non-obvious constraints.

Record:

- decision or gotcha
- reasoning
- impact on future changes
- where the rule shows up in code

### `.project-memory/memory/current.md`

Use for short- to medium-term focus.

Record:

- current focus
- in-progress areas
- next steps
- files to read first next time

## Generated vs Curated

Generated files:

- `.project-memory/generated/project-summary.md`
- `.project-memory/generated/feature-index.md`
- `.project-memory/generated/development-playbook.md`

Curated files:

- `.project-memory/memory/milestones.md`
- `.project-memory/memory/decisions.md`
- `.project-memory/memory/current.md`

Rules:

- initialization may create curated files when they are missing
- refresh may rewrite generated files
- refresh must not overwrite curated files
- unless the user explicitly requests another language, generated text and newly created templates should use Chinese
- `generated/development-playbook.md` may preserve a manual accumulation section even though its auto-managed section is refreshed

## Suggested Templates

### `README.md`

Use `templates/README.md`.

### `generated/project-summary.md`

Use `templates/generated/project-summary.md`.

### `generated/feature-index.md`

Use `templates/generated/feature-index.md`.

### `generated/development-playbook.md`

Use `templates/generated/development-playbook.md`.

### `memory/milestones.md`

Use `templates/memory/milestones.md`.

### `memory/decisions.md`

Use `templates/memory/decisions.md`.

### `memory/current.md`

Use `templates/memory/current.md`.

### `AGENTS.md` Block

Use `templates/agents-block.md`.

## Refresh Heuristics

When refreshing generated files:

1. Re-read the current repo structure instead of trusting stale summaries.
2. Keep generated files concise and navigation-oriented.
3. Prefer path references that help the next task start faster.
4. Do not rewrite curated history unless the user explicitly asks.
5. When updating `development-playbook.md`, rewrite only the auto-managed section and preserve the manual section anchors.
