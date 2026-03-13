# project-memory-skill

[中文介绍](README.zh-CN.md)

## 1. One-Line Summary

`project-memory` is a Codex skill that gives a repository persistent project memory, so the agent can reuse context across sessions instead of rebuilding it from scratch every time.

## 2. What Problem It Solves

When an agent re-enters the same repository, a large amount of token usage often comes from repeated context rebuilding:

- understanding what the project does
- locating real entrypoints
- identifying important modules
- rediscovering conventions and architecture constraints
- scanning large parts of the repo again just to regain context

`project-memory` converts that repeated project comprehension cost into reusable repository knowledge stored inside the repo itself.

## 3. Core Features

- Maintain persistent project memory inside the repository
- Generate project summaries, feature indexes, and development playbooks
- Track current focus, milestones, and architectural decisions
- Separate refreshable context from durable project history
- Reuse `.project-memory` before broad repository scanning in later sessions
- Reduce repeated large-scale scanning and lower token consumption
- Keep project documents in Chinese by default while preserving code identifiers and paths

## 4. Workflow

```text
session 1
   ↓
scan repository
   ↓
generate project memory
   ↓
save into .project-memory/

later session
   ↓
read .project-memory/
   ↓
skip unnecessary repo scanning
   ↓
start coding faster
```

Recommended revisit order:

1. Read `AGENTS.md`
2. Read `.project-memory/README.md`
3. Read `generated/project-summary.md`
4. Read `generated/development-playbook.md`
5. Read `generated/feature-index.md`
6. Read relevant files in `memory/`
7. Only then decide whether broad code scanning is still needed

## 5. Safety Design

- Project memory is stored in plain Markdown files inside the repository
- Refreshable context and durable history are split into different directories
- Curated history under `.project-memory/memory/` should not be overwritten during refresh
- The manual section in `generated/development-playbook.md` is preserved
- All stored context remains reviewable, editable, and auditable by humans

## 6. Technical Implementation

`project-memory` uses a text-first design:

- `.project-memory/generated/` stores refreshable context
- `.project-memory/memory/` stores long-lived project history
- `.project-memory/README.md` acts as the reading entry for future sessions
- `project-memory/templates/` provides default file shapes
- `project-memory/references/file-guides.md` defines update rules and file responsibilities

Repository memory layout:

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

This repository also includes `project-init`, but only as a setup helper. It extends the normal Codex initialization flow by also preparing `.project-memory` during first-time setup.

## 7. Quick Start

Install the skills:

```text
~/.codex/skills/project-memory
~/.codex/skills/project-init
```

Use them like this:

1. For a new repository, run `project-init` once.
2. Let it create or refresh `AGENTS.md` and initialize `.project-memory/`.
3. In later sessions, use `project-memory` as the default entry for repository context.
4. Before scanning large parts of the codebase, read `.project-memory` first.
5. After substantial work, refresh generated context or update curated memory.
