# genai_agent_rules

**Current release:** [v1.0.0](https://github.com/ola-mobility/genai_agent_rules/releases/tag/v1.0.0)

Organization-wide **Cursor agent workflow** rules and subagent definitions for AI-assisted feature delivery.

## Overview

This repository provides:

- **Workflow rules** (`.cursor/rules/`) — agent lifecycle, planning doc structure, and documentation sync
- **Subagent definitions** (`.cursor/agents/`) — requirement refinement, planning, execution, testing, and doc sync roles

Agent guidance is **tech-stack agnostic**. Language and runtime standards (Node.js 24, TypeScript, JavaScript) live in sibling repos — install those separately when your stack needs them.

## When to use this repo vs standards repos

| Need | Repository |
|------|------------|
| Subagent chain (plan → execute → test → doc sync) | **genai_agent_rules** (this repo) |
| Node.js 24 coding, architecture, lint, security, testing | [genai_node_rules](https://github.com/ola-mobility/genai_node_rules) |
| TypeScript-only conventions | [genai_ts_rules](https://github.com/ola-mobility/genai_ts_rules) |
| JavaScript / Node baseline | [genai_js_rules](https://github.com/ola-mobility/genai_js_rules) |

Use **genai_agent_rules** when your team runs the requirement → investigate → plan → execute → verify agent chain with `docs/feature/` plans and `docs/test-reports/`.

Use **genai_node_rules** (and siblings) for how code is written — ESM, `node:test`, layered architecture, ESLint, and related rules. Some agents (e.g. `phase-executor`, `test-runner`) reference stack rules by path when both repos are merged into the same `.cursor/` tree.

## Repository structure

```txt
genai_agent_rules/
│
├── README.md
├── CONTRIBUTING.md
├── CHANGELOG.md
├── OWNERS.md
│
└── .cursor/
    ├── rules/
    │   ├── agent-workflow-boundaries.mdc
    │   ├── planning-documents.mdc
    │   └── documentation-sync.mdc
    └── agents/
        ├── requirement-refinement.mdc
        ├── code-investigator.mdc
        ├── architect-planner.mdc
        ├── phase-executor.mdc
        ├── doc-sync.mdc
        ├── test-runner.mdc
        └── rule-feedback-writer.mdc
```

## Installation

Copy or symlink into your project (merge with any existing `.cursor/` content):

```bash
# From a clone of this repo
cp -r .cursor/rules/*   /path/to/your-project/.cursor/rules/
cp -r .cursor/agents/*  /path/to/your-project/.cursor/agents/
```

Or add as a submodule and link both `rules` and `agents` directories.

**Node.js 24 services:** also install [genai_node_rules](https://github.com/ola-mobility/genai_node_rules) so `phase-executor` and `test-runner` can resolve `node24-*` rule paths.

```bash
# Example: both repos into one project
cp -r /path/to/genai_agent_rules/.cursor/agents /path/to/your-project/.cursor/
cp -r /path/to/genai_agent_rules/.cursor/rules/* /path/to/your-project/.cursor/rules/
cp -r /path/to/genai_node_rules/.cursor/rules/*   /path/to/your-project/.cursor/rules/
```

In Cursor, subagents are available when `.cursor/agents/*.mdc` is present; workflow rules with `alwaysApply: true` apply to every agent session.

## Workflow rules

| Rule | Focus |
|------|-------|
| `agent-workflow-boundaries.mdc` | Subagent lifecycle, handoffs, parallelisation |
| `planning-documents.mdc` | Feature plans under `docs/feature/` |
| `documentation-sync.mdc` | Sync plan docs after implementation and verification |

## Subagents

| Agent | Role |
|-------|------|
| `requirement-refinement` | Clarify requirements before planning |
| `code-investigator` | Trace flows; write investigation reports |
| `architect-planner` | Phased plans; no product code |
| `phase-executor` | Implement one approved phase per pass |
| `doc-sync` | Update planning docs after execute/verify |
| `test-runner` | Tests, command evidence, test reports |
| `rule-feedback-writer` | Persist durable guidance from user feedback |

## Versioning

See [CHANGELOG.md](./CHANGELOG.md) for release history. Pin consuming repos to git tags (`vMAJOR.MINOR.PATCH`); see [CONTRIBUTING.md](./CONTRIBUTING.md) for how to cut a release.


## Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md). Maintainers are listed in [OWNERS.md](./OWNERS.md).
