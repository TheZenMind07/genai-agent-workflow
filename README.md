# genai_agent_rules

**Current release:** [v1.1.0](https://github.com/ola-mobility/genai_agent_rules/releases/tag/v1.1.0)

Organization-wide **Cursor agent workflow** rules and subagent definitions for AI-assisted feature delivery.

## Overview

This repository provides:

- **Workflow rules** (`.cursor/rules/`) — agent lifecycle, SDD structure under `docs/sdd/`, ADRs, and documentation sync
- **Subagent definitions** (`.cursor/agents/`) — planning (including requirements), execution, testing, and doc sync roles
- **ADR scaffold** (`.cursor/adr/`) — template and README for architectural decision records in consuming repos

Agent guidance is **framework-agnostic** (tech-stack neutral). It does not assume Node.js, Express, TypeScript, or any specific language, runtime, or test runner. Pair this repo with language/runtime standards repos when your stack needs them.

## When to use this repo vs standards repos

| Need | Repository |
|------|------------|
| Subagent chain (plan → execute → test → doc sync) | **genai_agent_rules** (this repo) |
| Node.js coding, architecture, lint, security, testing | [genai_node_rules](https://github.com/ola-mobility/genai_node_rules) *(optional)* |
| TypeScript conventions | [genai_ts_rules](https://github.com/ola-mobility/genai_ts_rules) *(optional)* |
| JavaScript baseline | [genai_js_rules](https://github.com/ola-mobility/genai_js_rules) *(optional)* |

Use **genai_agent_rules** when your team runs the investigate → plan → execute → verify agent chain with `docs/investigation/`, SDDs under `docs/sdd/`, and test reports under `docs/sdd/test-reports/`.

Use optional sibling standards repos for how code is written in a given stack — coding style, architecture patterns, linting, security, and testing conventions. Merge only the repos your project needs into the same `.cursor/rules/` tree; agents follow whatever stack rules are present there.

## Combining repos

Install this repo first for workflow agents and rules, then merge optional stack-specific rules into the same `.cursor/` tree:

```bash
# Agent workflow (required for the subagent chain)
cp -r /path/to/genai_agent_rules/.cursor/agents /path/to/your-project/.cursor/
cp -r /path/to/genai_agent_rules/.cursor/rules/* /path/to/your-project/.cursor/rules/
cp -r /path/to/genai_agent_rules/.cursor/adr /path/to/your-project/.cursor/
cp /path/to/genai_agent_rules/.cursor/hooks.json /path/to/your-project/.cursor/
cp -r /path/to/genai_agent_rules/.cursor/hooks /path/to/your-project/.cursor/
chmod +x /path/to/your-project/.cursor/hooks/*.sh

# Optional: stack-specific coding standards (example — use only what your stack needs)
cp -r /path/to/genai_node_rules/.cursor/rules/* /path/to/your-project/.cursor/rules/
```

Teams on other stacks can substitute their own standards repo or project-local rules under `.cursor/rules/` instead of the Node/TS/JS siblings above.

## Repository structure

```txt
genai_agent_rules/
│
├── README.md
├── CONTRIBUTING.md
├── CHANGELOG.md
├── OWNERS.md
│
├── docs/
│   ├── investigation/
│   │   └── README.md
│   └── sdd/
│       ├── README.md
│       └── test-reports/
│           └── README.md
│
└── .cursor/
    ├── hooks.json
    ├── hooks/
    │   ├── invoke-doc-sync-after-phase-executor.sh
    │   └── invoke-doc-sync-after-test-runner.sh
    ├── adr/
    │   ├── README.md
    │   └── 0000-template.md
    ├── rules/
    │   ├── agent-workflow-boundaries.mdc
    │   ├── architectural-decisions.mdc
    │   ├── planning-documents.mdc
    │   ├── investigation-reports.mdc
    │   ├── test-reports.mdc
    │   ├── documentation-sync.mdc
    │   └── workflow-hooks.mdc
    └── agents/
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
cp -r .cursor/adr       /path/to/your-project/.cursor/
# Optional: automate doc-sync handoffs after phase-executor and test-runner
cp .cursor/hooks.json   /path/to/your-project/.cursor/
cp -r .cursor/hooks     /path/to/your-project/.cursor/
chmod +x /path/to/your-project/.cursor/hooks/*.sh
```

Or add as a submodule and link both `rules` and `agents` directories.

In Cursor, subagents are available when `.cursor/agents/*.mdc` is present; workflow rules with `alwaysApply: true` apply to every agent session.

## Workflow rules

| Rule | Focus |
|------|-------|
| `agent-workflow-boundaries.mdc` | Subagent lifecycle, handoffs, parallelisation |
| `architectural-decisions.mdc` | ADRs under `.cursor/adr/` and agent ownership |
| `planning-documents.mdc` | Feature design specs (SDDs) under `docs/sdd/` |
| `investigation-reports.mdc` | Investigation reports under `docs/investigation/` |
| `test-reports.mdc` | Test execution reports under `docs/sdd/test-reports/` |
| `documentation-sync.mdc` | Sync plan docs after implementation and verification |
| `workflow-hooks.mdc` | Optional `subagentStop` hooks for doc-sync handoffs |

## Subagents

| Agent | Role |
|-------|------|
| `code-investigator` | Trace flows; write reports under `docs/investigation/` |
| `architect-planner` | Clarify requirements and write phased SDDs; no product code |
| `phase-executor` | Implement one approved phase per pass |
| `doc-sync` | Update planning docs after execute/verify |
| `test-runner` | Tests, command evidence, test reports under `docs/sdd/test-reports/` |
| `rule-feedback-writer` | Persist guidance to rules, agents, skills, ADRs, or `AGENTS.md` |

## Versioning

See [CHANGELOG.md](./CHANGELOG.md) for release history. Pin consuming repos to git tags (`vMAJOR.MINOR.PATCH`); see [CONTRIBUTING.md](./CONTRIBUTING.md) for how to cut a release.

## Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md). Maintainers are listed in [OWNERS.md](./OWNERS.md).
