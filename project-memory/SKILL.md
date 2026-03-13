---
name: project-memory
description: Maintain repo-local `.project-memory` context for code projects that opt in through `AGENTS.md`. Use when Codex needs to initialize or refresh project memory files, maintain `.project-memory` links inside `AGENTS.md`, or update curated project memory such as feature navigation, milestones, decisions, and current focus. If the current working project does not contain `AGENTS.md`, do not create `.project-memory`.
---

# Project Memory

## Overview

Use this skill to keep a repo-local project memory that survives across conversations without mixing rebuildable project description with curated historical notes.

This version is text-first. The agent should read and edit Markdown files directly instead of relying on Python scripts.

Treat `.project-memory/generated/` as rebuildable context and `.project-memory/memory/` as curated history that must survive refreshes.

## Language

- Unless the user explicitly requests another language, all `.project-memory` output documents should use Chinese.
- This applies to `.project-memory/README.md`, generated files under `.project-memory/generated/`, curated file templates created during initialization, and the managed `AGENTS.md` project-memory block.
- Keep code identifiers, file paths, commands, and configuration keys in their original language and wrap them in backticks when appropriate.
- Do not auto-translate existing curated memory during refresh; the Chinese-by-default rule applies to newly created or regenerated content.

## Entry Gate

1. Look for `AGENTS.md` in the current project root.
2. If `AGENTS.md` is missing, stop. Do not create `.project-memory`.
3. If `AGENTS.md` exists, ensure it contains links to the project memory files.

## Directory Model

Use this layout:

```text
.project-memory/
  README.md
  generated/
    project-summary.md
    feature-index.md
    development-playbook.md
  memory/
    milestones.md
    decisions.md
    current.md
```

Rules:

- `README.md` is the project-memory entry page and read order.
- `generated/project-summary.md` is a rebuildable description of the current repo shape.
- `generated/feature-index.md` is a rebuildable navigation index that points to code areas worth reading next.
- `generated/development-playbook.md` is a condensed development playbook. It should help Codex avoid re-scanning large parts of the repo by summarizing methodology, high-value example paths, and verified coding patterns.
- `memory/milestones.md`, `memory/decisions.md`, and `memory/current.md` are curated notes and must not be overwritten by generated refresh work.

Special rule for `generated/development-playbook.md`:

- The file may contain an auto-managed section and a preserved manual accumulation section.
- Refresh only the auto-managed section.
- Preserve the manual accumulation section so Codex can record reusable methodology, implementation heuristics, and example code references learned from real project work.

Read [references/file-guides.md](references/file-guides.md) when you need the file-by-file templates or update heuristics.

## Operations

### Initialize

Use initialization when the project has `AGENTS.md` but does not yet have `.project-memory`.

Initialization must:

- create the `.project-memory/` directories
- create `.project-memory/README.md`
- create the curated `memory/` files only when missing
- create `generated/project-summary.md`
- create `generated/feature-index.md`
- create `generated/development-playbook.md`
- inject or refresh the `AGENTS.md` project-memory block

Initialization must not overwrite existing curated memory.

### Refresh Generated Context

Use refresh when the project structure changed and the generated description needs to be updated.

Refresh must:

- require both `AGENTS.md` and `.project-memory/`
- refresh `.project-memory/README.md` to keep the read order aligned with the current layout
- refresh only `generated/project-summary.md`
- refresh only `generated/feature-index.md`
- refresh only the auto-managed section of `generated/development-playbook.md`, while preserving the manual accumulation section
- keep `memory/` untouched
- keep the `AGENTS.md` block aligned with the current layout

### Update Curated Memory

Use manual updates for information that should survive future refreshes.

Update `memory/` when the task introduces reusable knowledge such as:

- completed milestones or phase outcomes
- important architectural decisions
- non-obvious constraints or gotchas
- the current focus and next likely areas of work

Do not write low-value task residue such as one-off debugging trails or minor edits with no future navigation value.

After substantial repo work, also consider updating the manual accumulation section in `generated/development-playbook.md` when the task surfaced reusable:

- development methodology
- implementation heuristics
- common package usage shortcuts
- high-value example code paths

This file should help future Codex runs become faster and more repo-native over time.

## Direct Editing Pattern

Use direct file editing instead of helper scripts:

1. Read `AGENTS.md`.
2. Follow the links into `.project-memory/README.md` when it exists.
3. Create or refresh Markdown files directly.
4. Use `templates/` as a shape guide when files are missing or need normalization.
5. Keep generated and curated content separated.
6. Preserve manual sections and curated notes when refreshing generated context.

## Working Loop

For substantial repo work:

1. Read `AGENTS.md`.
2. Follow the links into `.project-memory/README.md`.
3. Read `generated/project-summary.md`.
4. Read `generated/development-playbook.md` before scanning large code areas or `common` packages.
5. Read `generated/feature-index.md` to navigate into concrete code paths.
6. Read curated memory only when the task touches ongoing milestones, decisions, or current focus.
7. After the task, decide whether the change affects generated context, curated memory, or both.

## AGENTS.md Rules

The managed `AGENTS.md` block should link to:

- `.project-memory/README.md`
- `.project-memory/generated/project-summary.md`
- `.project-memory/generated/feature-index.md`
- `.project-memory/generated/development-playbook.md`
- `.project-memory/memory/current.md`
- `.project-memory/memory/decisions.md`
- `.project-memory/memory/milestones.md`

It should also state that:

- `.project-memory/generated/` may be initialized or refreshed
- `.project-memory/memory/` must not be overwritten
- projects without `AGENTS.md` should not get `.project-memory`
- the managed labels and explanatory text should use Chinese by default

Use `templates/agents-block.md` as the default block shape.

## Resources

### `templates/`

Use these Markdown templates as the default starting point for `.project-memory` files and the managed `AGENTS.md` block.

### `references/file-guides.md`

Read this reference when you need the editing templates for `README.md`, the generated files, or the curated memory files.
