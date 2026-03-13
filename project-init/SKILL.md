---
name: project-init
description: Initialize or bootstrap a coding project for Codex by creating or refreshing repo guidance and project memory. Use when the user asks to 初始化项目、初始化仓库、给项目做初始化、project init、bootstrap a repository, create the first `AGENTS.md`, or make a newly opened repo ready for repeated development work.
---

# Project Init

## Overview

Use this skill to perform first-time project bootstrap for Codex in the current repository.

The goal is to make the repository immediately reusable across future sessions by ensuring `AGENTS.md` and `.project-memory` both exist and stay aligned.

This version is text-first. Do not rely on Python scripts. Create or refresh repository guidance and project memory by directly editing Markdown files.

## Workflow

1. Locate the repository root and inspect whether `AGENTS.md` and `.project-memory/` already exist.
2. If `AGENTS.md` is missing, create it from verified repository facts only.
3. If `AGENTS.md` already exists, refresh it only when the user explicitly wants initialization or when the file is obviously stale. Preserve existing human-authored project guidance.
4. After `AGENTS.md` exists, initialize `.project-memory/` directly if it is missing.
5. If `.project-memory/` already exists, refresh only the generated files and keep curated memory untouched.
6. Keep the managed `AGENTS.md` project-memory block aligned with the current `.project-memory` layout.
7. Summarize what was initialized, what was refreshed, and what could not be inferred reliably.

## AGENTS Guidance

When creating or refreshing `AGENTS.md`:

- Inspect build files, top-level modules, docs, and existing code structure before writing guidance.
- Record only verified commands, architecture constraints, naming conventions, and repository-specific gotchas.
- Prefer concise, high-signal guidance over generic boilerplate.
- Preserve existing project-specific instructions unless the user explicitly asks for a rewrite.
- Keep any existing managed `project-memory` block aligned instead of duplicating it.

If the repository is too sparse to infer detailed guidance, create a minimal but accurate `AGENTS.md` rather than inventing commands or conventions.

## Project-Memory Integration

- Treat `project-memory` as the canonical follow-up step after `AGENTS.md` exists.
- Create `.project-memory/README.md`, `.project-memory/generated/*.md`, and `.project-memory/memory/*.md` directly as Markdown files.
- Do not overwrite `.project-memory/memory/` during initialization or refresh.
- If initialization happens after major repository changes, prefer refreshing generated context so it matches the latest layout.
- Preserve the manual section in `.project-memory/generated/development-playbook.md` when refreshing it.

## Recommended File Layout

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

Unless the user explicitly requests another language, generated project-memory documents should use Chinese.

## Working Style

- Use direct Markdown editing instead of helper scripts.
- Reuse the companion `project-memory` templates and file guides when shaping files.
- Separate rebuildable context from curated historical notes.
- Prefer refresh over rewrite when the repository already contains useful guidance.

## Important Limitation

Codex does not currently expose a user-configurable hook that makes the built-in `/init` slash command automatically call a skill afterward.

When the user asks to initialize a project, use this skill to perform the combined workflow manually inside the current session instead of relying on slash-command chaining.
