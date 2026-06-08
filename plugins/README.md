# Plugins

This repository is an **extendable Cursor plugin marketplace**. Each plugin lives in its own
subdirectory with a `.cursor-plugin/plugin.json` manifest.

The root [`.cursor-plugin/marketplace.json`](../.cursor-plugin/marketplace.json) indexes what is
published. Cursor loads plugins from `source` paths relative to the repository root.

## Available plugins

| Plugin | Directory | Status |
|--------|-----------|--------|
| **genai-agent-workflow** | [`genai-agent-workflow/`](./genai-agent-workflow/) | Available |
| **genai-js-rules** | [`genai-js-rules/`](./genai-js-rules/) | Planned |
| **genai-ts-rules** | [`genai-ts-rules/`](./genai-ts-rules/) | Planned |

Install **genai-agent-workflow** for the full agent chain. Add JS/TS plugins from this same repo
when they land (no separate marketplace submission required).

## Adding a new plugin later

1. Create `plugins/<plugin-name>/` with:
   - `.cursor-plugin/plugin.json` (`name` must be unique, kebab-case)
   - Component dirs (`rules/`, `agents/`, `hooks/`, etc.) per [Cursor Plugins reference](https://cursor.com/docs/reference/plugins)
2. Add an entry to `.cursor-plugin/marketplace.json`:
   ```json
   {
     "name": "genai-js-rules",
     "source": "plugins/genai-js-rules",
     "description": "JavaScript coding standards for Cursor."
   }
   ```
3. Bump the plugin `version` in its `plugin.json` and note the change in [CHANGELOG.md](../CHANGELOG.md).
4. Test locally:
   ```bash
   ln -sf "$(pwd)/plugins/<plugin-name>" ~/.cursor/plugins/local/<plugin-name>
   ```
5. Marketplace publish uses the **repository URL**; new plugins appear after review when
   `marketplace.json` is updated on the default branch.

## Manual install (consuming project)

Copy a plugin’s contents into the project `.cursor/` tree (paths are relative to the plugin root):

```bash
PLUGIN=genai-agent-workflow
REPO=/path/to/genai_agent_rules
DEST=/path/to/your-project/.cursor

cp -r "$REPO/plugins/$PLUGIN/agents/"*  "$DEST/agents/"  2>/dev/null || mkdir -p "$DEST/agents"
cp -r "$REPO/plugins/$PLUGIN/rules/"*   "$DEST/rules/"
cp -r "$REPO/plugins/$PLUGIN/hooks/"*   "$DEST/hooks/"   2>/dev/null || true
# hooks.json at project .cursor/hooks.json if your layout uses .cursor/hooks/
cp "$REPO/plugins/$PLUGIN/hooks/hooks.json" "$DEST/hooks.json" 2>/dev/null || \
  cp "$REPO/plugins/$PLUGIN/hooks/hooks.json" "$DEST/hooks/hooks.json"
chmod +x "$DEST/hooks/"*.sh 2>/dev/null || chmod +x "$DEST/"*.sh 2>/dev/null || true
```

ADR template (not part of the workflow plugin): bootstrap from [`../docs/adr/`](../docs/adr/) into
`your-project/docs/adr/`.

## Planned: JavaScript and TypeScript

`genai-js-rules` and `genai-ts-rules` will hold stack-specific `.mdc` rules only (no agents).
Content may be migrated from [genai_js_rules](https://github.com/ola-mobility/genai_js_rules) and
[genai_ts_rules](https://github.com/ola-mobility/genai_ts_rules) or maintained here directly.

Until those directories ship manifests, install workflow only or merge sibling repos manually per
the root [README.md](../README.md).
