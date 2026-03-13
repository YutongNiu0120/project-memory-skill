# project-memory-skill

[中文介绍](README.zh-CN.md)

`project-memory` is a text-first Codex skill for building repository-level memory that survives across sessions.

It helps the agent understand a project faster, keep stable project knowledge in one place, and avoid wasting tokens on repeated large-scale scans of the same codebase.

This repository is centered on `project-memory`. `project-init` is included as a lightweight companion only to make first-time setup easier.

## What `project-memory` Does

`project-memory` maintains a repo-local `.project-memory/` directory with a clear split between:

- rebuildable project context
- durable project history
- ongoing focus and decisions

The goal is simple:

- make the agent more project-aware
- let useful project knowledge accumulate over time
- reduce repeated exploration cost
- give future sessions a faster, lower-token starting point

## Why It Is Useful

When an agent re-enters a repository, the expensive part is usually not editing code. It is rebuilding context:

- what this project does
- which modules matter
- where the real entrypoints are
- which conventions are actually used
- which decisions and constraints already exist

`project-memory` turns that repeated rediscovery into maintained project memory.

Instead of re-scanning large areas every time, the agent can read `.project-memory` first and then go straight to the code paths that matter.

## Core Features

- Project-level memory stored directly in Markdown
- Separate generated context from curated historical notes
- Preserve durable knowledge such as decisions, milestones, and current focus
- Revisit a repository by reading `.project-memory` before broad code scanning
- Reduce token waste caused by repeated large-scale exploration
- Default project documents to Chinese while preserving code identifiers and paths

## Memory Structure

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

How the layers work:

- `generated/`: rebuildable summaries and navigation docs
- `memory/`: durable project history that should survive refreshes
- `README.md`: the read order for future sessions

## Revisit Workflow

When the agent comes back to the same repository in a later session:

1. Read `AGENTS.md`
2. Read `.project-memory/README.md`
3. Read `generated/project-summary.md`
4. Read `generated/development-playbook.md`
5. Read `generated/feature-index.md`
6. Read relevant curated files in `memory/`
7. Only then decide whether broader code scanning is still needed

This is the key behavior of the skill, and the main source of token savings.

## Included Companion: `project-init`

This repository also includes `project-init`, but it is intentionally a supporting skill.

Use `project-init` only when a repository is new or not yet prepared for Codex. Its job is to:

- create or refresh `AGENTS.md`
- initialize `.project-memory`
- align the managed project-memory block inside `AGENTS.md`

After initialization, ongoing usage should mainly rely on `project-memory`.

## Repository Layout

```text
.
├── project-init/
│   ├── agents/
│   │   └── openai.yaml
│   └── SKILL.md
└── project-memory/
    ├── agents/
    │   └── openai.yaml
    ├── references/
    │   └── file-guides.md
    ├── templates/
    │   ├── README.md
    │   ├── agents-block.md
    │   ├── generated/
    │   └── memory/
    └── SKILL.md
```

## Install

Copy the skill folders into your Codex skills directory:

```text
~/.codex/skills/project-memory
~/.codex/skills/project-init
```

## Usage

1. Use `project-init` once for a new repository.
2. Let it create or refresh `AGENTS.md` and `.project-memory/`.
3. In later sessions, use `project-memory` as the default entry for project context.
4. Before scanning large parts of the repo, read `.project-memory` history first.
5. Update generated context or curated notes after substantial work.

## Main Advantages

- Helps the agent understand the project faster
- Builds repo-level memory that can keep accumulating
- Reduces repeated large-scale scanning and token waste
- Keeps project knowledge transparent and editable
- Makes later sessions more repo-native and less exploratory

## Read First

- `project-memory/SKILL.md`
- `project-memory/references/file-guides.md`
- `project-memory/templates/`
- `project-init/SKILL.md`
