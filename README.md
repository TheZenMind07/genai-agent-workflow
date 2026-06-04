# genai_agent_rules

**Current release:** [v1.1.0](https://github.com/ola-mobility/genai_agent_rules/releases/tag/v1.1.0)

Organization-wide **Cursor agent workflow** rules and subagent definitions for AI-assisted feature delivery.

Published as an **extendable plugin marketplace** under [`.cursor-plugin/marketplace.json`](./.cursor-plugin/marketplace.json) — see [MARKETPLACE.md](./MARKETPLACE.md) and [plugins/README.md](./plugins/README.md).

## Overview

| Piece | Location |
|-------|----------|
| **Workflow plugin** (agents, rules, hooks) | [`plugins/genai-agent-workflow/`](./plugins/genai-agent-workflow/) |
| **JS standards plugin** | [`plugins/genai-js-rules/`](./plugins/genai-js-rules/) — *planned* |
| **TS standards plugin** | [`plugins/genai-ts-rules/`](./plugins/genai-ts-rules/) — *planned* |
| **ADR scaffold** (manual copy) | [`scaffold/adr/`](./scaffold/adr/) |
| **Doc conventions** (repo guides) | [`docs/`](./docs/) |

Agent guidance is **framework-agnostic**. JavaScript and TypeScript rule plugins will be added in this same repo later; until then, use sibling repos or merge rules manually.

## When to use this repo vs standards

| Need | Source |
|------|--------|
| Subagent chain (plan → execute → test → doc sync) | **genai-agent-workflow** plugin (this repo) |
| JavaScript baseline | **genai-js-rules** plugin here *(planned)* or [genai_js_rules](https://github.com/ola-mobility/genai_js_rules) |
| TypeScript conventions | **genai-ts-rules** plugin here *(planned)* or [genai_ts_rules](https://github.com/ola-mobility/genai_ts_rules) |
| Node.js coding, architecture, lint, security | [genai_node_rules](https://github.com/ola-mobility/genai_node_rules) *(optional)* |

Use **genai_agent_rules** when your team runs the investigate → plan → execute → verify chain with `docs/investigation/`, SDDs under `docs/sdd/`, and test reports under `docs/sdd/test-reports/`.

## Repository structure

```txt
genai_agent_rules/
├── .cursor-plugin/
│   └── marketplace.json          # indexes plugins (workflow now; JS/TS later)
├── plugins/
│   ├── README.md                 # how to add plugins
│   ├── genai-agent-workflow/     # agents, rules, hooks
│   ├── genai-js-rules/           # planned
│   └── genai-ts-rules/           # planned
├── scaffold/adr/                 # copy to consuming .cursor/adr/
├── assets/ola.svg
└── docs/                           # SDD, investigation, test-report guides
```

## Installation

### Cursor Marketplace (recommended)

1. Open **Cursor → Settings → Plugins**.
2. Install **GenAI Agent Workflow** (`genai-agent-workflow`) from the **ola-genai-plugins** marketplace (this repo).
3. When **genai-js-rules** / **genai-ts-rules** are published, install them from the same marketplace as needed.
4. Copy ADR scaffold: `cp -r scaffold/adr /path/to/your-project/.cursor/adr`

### Manual copy (workflow plugin)

```bash
REPO=/path/to/genai_agent_rules
DEST=/path/to/your-project/.cursor
PLUGIN=genai-agent-workflow

mkdir -p "$DEST/agents" "$DEST/rules" "$DEST/hooks"
cp -r "$REPO/plugins/$PLUGIN/agents/"* "$DEST/agents/"
cp -r "$REPO/plugins/$PLUGIN/rules/"*  "$DEST/rules/"
cp "$REPO/plugins/$PLUGIN/hooks/"*.sh   "$DEST/hooks/"
chmod +x "$DEST/hooks/"*.sh

# Project-level hooks.json (paths relative to project root)
cat > "$DEST/hooks.json" <<'EOF'
{
  "version": 1,
  "hooks": {
    "subagentStop": [
      {
        "command": ".cursor/hooks/invoke-doc-sync-after-phase-executor.sh",
        "matcher": "phase-executor",
        "loop_limit": 3
      },
      {
        "command": ".cursor/hooks/invoke-doc-sync-after-test-runner.sh",
        "matcher": "test-runner",
        "loop_limit": 3
      }
    ]
  }
}
EOF

cp -r "$REPO/scaffold/adr" "$DEST/adr"
```

Optional stack rules (until JS/TS plugins ship):

```bash
cp -r /path/to/genai_node_rules/.cursor/rules/* "$DEST/rules/"
```

### Local plugin development

```bash
ln -sf "$(pwd)/plugins/genai-agent-workflow" ~/.cursor/plugins/local/genai-agent-workflow
```

Reload Cursor (**Developer: Reload Window**).

## Workflow rules

Shipped in `plugins/genai-agent-workflow/rules/` (installed to `.cursor/rules/` in consuming repos).

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

See [CHANGELOG.md](./CHANGELOG.md). Pin consuming repos to git tags (`vMAJOR.MINOR.PATCH`).

## Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md). To add a plugin (e.g. JS/TS), follow [plugins/README.md](./plugins/README.md).
