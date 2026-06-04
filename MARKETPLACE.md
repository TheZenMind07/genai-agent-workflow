# Cursor Marketplace

This repository is packaged as a **Cursor plugin** for the [Cursor Marketplace](https://cursor.com/marketplace).

## Plugin manifest

| File | Purpose |
|------|---------|
| `.cursor-plugin/plugin.json` | Plugin metadata and component paths |
| `.cursor/rules/` | Workflow rules (installed by the plugin) |
| `.cursor/agents/` | Subagent definitions |
| `.cursor/hooks.json` | Optional `subagentStop` doc-sync handoffs |
| `assets/ola.svg` | Marketplace listing logo (Ola) |

Component paths in `plugin.json` point at the existing `.cursor/` tree so manual copy-install and marketplace install stay aligned.

## Install from the marketplace

1. Open **Cursor Settings → Plugins** (or search the marketplace panel).
2. Find **GenAI Agent Workflow** (`genai-agent-workflow`) or install from this repo after it is published.
3. Enable the plugin for your workspace.

After install, create project doc folders as needed (`docs/sdd/`, `docs/investigation/`, etc.) — see [README.md](./README.md).

### ADR scaffold (manual)

The plugin ships rules and agents only. Copy the ADR template into consuming projects when you use architectural decisions:

```bash
cp -r /path/to/genai_agent_rules/.cursor/adr /path/to/your-project/.cursor/
```

## Publish / update listing

1. Ensure [plugin.json](./.cursor-plugin/plugin.json) `version` matches [CHANGELOG.md](./CHANGELOG.md).
2. Validate locally: rules and agents have frontmatter; hook scripts are executable.
3. Submit or update at [cursor.com/marketplace/publish](https://cursor.com/marketplace/publish) with the public Git URL:

   `https://github.com/ola-mobility/genai_agent_rules`

4. Wait for Cursor’s manual review.

### Submission checklist

- [ ] Valid `.cursor-plugin/plugin.json` with unique `name` (`genai-agent-workflow`)
- [ ] `description`, `version`, `author`, `repository`, `license` set
- [ ] Logo committed at `assets/ola.svg` and referenced in manifest
- [ ] All rules and agents have valid frontmatter
- [ ] Hook script paths in `.cursor/hooks.json` are relative (no `..`)
- [ ] `README.md` documents usage and optional ADR copy step
- [ ] Plugin tested in a sample project before submit

## Maintainer notes

- **Single-plugin repo** — no root `marketplace.json` (that format is for multi-plugin monorepos).
- Bump `plugin.json` `version` when cutting a release tag.
- Do not add stack-specific rules here; pair with [genai_node_rules](https://github.com/ola-mobility/genai_node_rules) and siblings in consuming repos.
