# Cursor Marketplace

This repository is an **extendable plugin marketplace** for GenAI Cursor standards.

## Marketplace manifest

| File | Purpose |
|------|---------|
| [`.cursor-plugin/marketplace.json`](./.cursor-plugin/marketplace.json) | Indexes all plugins in this repo |
| [`plugins/<name>/`](./plugins/) | One directory per plugin |
| [`plugins/<name>/.cursor-plugin/plugin.json`](./plugins/genai-agent-workflow/.cursor-plugin/plugin.json) | Per-plugin metadata and component paths |
| [`assets/genai.svg`](./assets/genai.svg) | Shared marketplace logo (referenced by plugins) |

### Plugins today and planned

| Plugin | Status |
|--------|--------|
| `genai-agent-workflow` | **Available** — agents, rules, hooks |
| `genai-js-rules` | **Planned** — JavaScript rules only |
| `genai-ts-rules` | **Planned** — TypeScript rules only |

Add JS/TS by creating `plugins/genai-js-rules/` (or `-ts-`) with a manifest and registering in `marketplace.json`. See [plugins/README.md](./plugins/README.md).

## Install from the marketplace

1. Open **Cursor Settings → Plugins**.
2. Find plugins from this repo (marketplace id: **genai-plugins**).
3. Install **genai-agent-workflow**; add JS/TS plugins when listed.
4. Bootstrap [`docs/adr/`](./docs/adr/) in your project when using ADRs (`mkdir -p docs/adr` and copy the template).

## Publish / update listing

1. Bump each plugin’s `version` in `plugins/<name>/.cursor-plugin/plugin.json` and [CHANGELOG.md](./CHANGELOG.md).
2. Update `.cursor-plugin/marketplace.json` when adding plugins.
3. Submit at [cursor.com/marketplace/publish](https://cursor.com/marketplace/publish):

   `https://github.com/genai/genai_agent_rules`

4. Wait for Cursor’s manual review.

### Submission checklist

- [ ] Root `.cursor-plugin/marketplace.json` with unique marketplace `name`
- [ ] Each plugin has `plugins/<name>/.cursor-plugin/plugin.json` and valid component paths
- [ ] `genai-agent-workflow`: rules, agents, hooks; hook scripts executable; paths relative (no `..`)
- [ ] Logo at `assets/genai.svg` referenced from plugin manifest
- [ ] [README.md](./README.md) and [plugins/README.md](./plugins/README.md) document install and planned JS/TS plugins
- [ ] Tested locally via `~/.cursor/plugins/local/<plugin-name>` symlink

## Local testing

```bash
ln -sf "$(pwd)/plugins/genai-agent-workflow" ~/.cursor/plugins/local/genai-agent-workflow
chmod +x plugins/genai-agent-workflow/hooks/*.sh
```

Reload Cursor, enable the plugin on a sample app repo, run a subagent and check the **Hooks** output channel.

Hook smoke test:

```bash
echo '{"status":"completed"}' | plugins/genai-agent-workflow/hooks/invoke-doc-sync-after-phase-executor.sh
```

## Maintainer notes

- **Extendable monorepo** — new plugins = new folder under `plugins/` + `marketplace.json` entry.
- Keep **genai-agent-workflow** framework-agnostic; put JS/TS (and later Node) rules in separate plugins.
- ADR template stays under `docs/adr/` (not installed by plugins automatically).
