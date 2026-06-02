# Contributing

Thank you for helping evolve org-wide agent workflow standards. Changes here should apply across stacks and consuming repositories.

## What belongs here

- **In scope** — Subagent roles, handoffs, planning doc structure, documentation sync, and workflow boundaries that are not tied to a single language or framework.
- **Out of scope** — Node/TypeScript/JavaScript coding standards, lint rules, or project-specific app configuration. Those belong in [genai_node_rules](https://github.com/ola-mobility/genai_node_rules), [genai_ts_rules](https://github.com/ola-mobility/genai_ts_rules), [genai_js_rules](https://github.com/ola-mobility/genai_js_rules), or the consuming repo.

## How to propose a change

1. Open an issue or discussion describing the workflow problem and proposed agent or rule text.
2. Open a pull request updating the relevant `.cursor/agents/*.mdc` or `.cursor/rules/*.mdc` file(s).
3. Update [CHANGELOG.md](./CHANGELOG.md) under `[Unreleased]` with a short, user-facing summary.
4. Request review from a maintainer in [OWNERS.md](./OWNERS.md).

## File guidelines

- Keep **agents** tech-stack agnostic; reference stack rules by path only when a consuming repo is expected to merge a standards repo into `.cursor/rules/`.
- Keep **workflow rules** focused on lifecycle, planning docs, and doc sync — one theme per file.
- Use frontmatter (`description`, `globs`, `alwaysApply`) consistently with existing files.
- Prefer imperative bullets; avoid duplicating guidance across agent and rule files.

## Review criteria

Maintainers check that the change:

- Applies broadly (not tied to one application repo)
- Does not contradict other agents or workflow rules
- Is clear for humans and Cursor subagents
- Includes a CHANGELOG entry when behaviour or guidance changes

## Versioning

We use [CHANGELOG.md](./CHANGELOG.md) for release notes and **git tags** (`vMAJOR.MINOR.PATCH`) for pinned versions.

### Cutting a release

1. Move changes from `[Unreleased]` into a new version section with today's date.
2. Merge to `main`.
3. Create and push the tag:

```bash
git tag -a v1.0.0 -m "v1.0.0"
git push origin v1.0.0
```

4. Optionally create a GitHub Release from that tag.

Downstream teams can pin to a tag (submodule, copy, or sync at `v*`).
