# Codex Project Bootstrap Skills

[中文介绍](README.zh-CN.md)

Two text-first Codex skills for turning a repository into a reusable, cross-session workspace:

- `project-init`: bootstrap a repo for Codex by creating or refreshing `AGENTS.md` and `.project-memory`
- `project-memory`: maintain repo-local project memory with clear separation between generated context and curated history

No Python runtime. No helper backend. No hidden state machine. Just Markdown that the model can read and maintain directly.

If this saves you from re-scanning the same repo every session, give it a star.

## Why This Repo Exists

Many agent skills become heavier than the problem they solve. They ship scripts, local CLIs, or mini backends just to manage a handful of project documents.

This repo takes the opposite approach:

- Keep the workflow text-first
- Let the model work on files it can inspect directly
- Make all state transparent to the user
- Preserve human-written context instead of overwriting it

The result is easier to understand, easier to audit, and easier to adapt to your own setup.

## What's Inside

### `project-init`

Use this when you open a repo for the first time and want Codex to make it ready for repeated work.

Highlights:

- Creates or refreshes `AGENTS.md` from verified repo facts
- Initializes `.project-memory` without requiring scripts
- Keeps the managed `AGENTS.md` memory block aligned
- Prefers refresh over destructive rewrite

### `project-memory`

Use this to maintain repo-local memory that survives across conversations.

Highlights:

- Splits rebuildable context from curated historical notes
- Keeps generated files in `.project-memory/generated/`
- Keeps durable notes in `.project-memory/memory/`
- Preserves manual sections during refresh
- Defaults project-memory documents to Chinese unless the user asks otherwise

## Key Advantages

- Zero runtime dependency: no Python required for normal use
- Text-first by design: the agent reads and edits Markdown directly
- Human-auditable: all memory lives in plain files
- Safer refresh model: generated context can evolve without overwriting curated notes
- Repo-native workflow: optimized for real coding repositories, not toy demos
- Chinese-friendly output: ideal for teams that want Chinese repo guidance without translating code identifiers

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
~/.codex/skills/project-init
~/.codex/skills/project-memory
```

Or symlink them if you prefer to keep a single working copy.

## Suggested Workflow

1. Use `project-init` when a repo is new or not yet Codex-ready.
2. Let it create or refresh `AGENTS.md`.
3. Let it initialize `.project-memory/`.
4. Use `project-memory` during later tasks to refresh generated context and accumulate durable project knowledge.

## Who This Is For

- Engineers using Codex across many repositories
- Teams who want persistent repo guidance without adding tooling overhead
- Users who prefer transparent Markdown over opaque automation
- Chinese-speaking workflows that still need code and paths preserved in original form

## Design Principles

- Verified facts over invented boilerplate
- Refresh over overwrite
- Generated context separate from curated memory
- Markdown first
- Chinese by default for project docs, unless the user switches language

## Related Files Worth Reading

- `project-init/SKILL.md`
- `project-memory/SKILL.md`
- `project-memory/references/file-guides.md`
- `project-memory/templates/`

## Star-Worthy, In Practice

These skills are small on purpose. That is the advantage.

- You can understand the whole system in minutes
- You can review every stored rule in plain text
- You can customize the templates without touching code
- You do not need to debug a local backend just to keep repo notes current

If you want Codex skills that stay lightweight while becoming more useful over time, this repo is built for that.
