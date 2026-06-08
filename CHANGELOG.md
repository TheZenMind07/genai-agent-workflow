# Changelog

All notable changes to the Cursor agent workflow rules and subagent definitions in this repository are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [Unreleased]

### Changed

- `agent-workflow-boundaries.mdc` — distinguish planned-work lifecycle from standalone subagent use; handoffs optional for standalone tasks when required
- **Breaking:** ADRs move from `.cursor/adr/` to **`docs/adr/`**; template under `docs/adr/` replaces `scaffold/adr/`; update links in consuming repos

### Added

- **Extendable plugin marketplace** — `.cursor-plugin/marketplace.json` indexes plugins; workflow under `plugins/genai-agent-workflow/`; placeholders for `genai-js-rules` and `genai-ts-rules`
- [plugins/README.md](./plugins/README.md) — how to add plugins (JS/TS later without a new repo submit)
- `assets/ola.svg`, `LICENSE`, [MARKETPLACE.md](./MARKETPLACE.md); `subagentStop` hooks and `workflow-hooks.mdc`

### Changed

- **Breaking (layout):** agents, rules, and hooks moved from repo-root `.cursor/` to `plugins/genai-agent-workflow/`; ADR scaffold to `scaffold/adr/`; update manual install paths and local symlinks
- Plugin hooks: `plugins/genai-agent-workflow/hooks/hooks.json` (paths relative to plugin root)
- Marketplace publish uses root `marketplace.json` (one repo URL for multiple plugins over time)

### Changed

- Merged **`requirement-refinement`** into **`architect-planner`** — one SDD under `docs/sdd/` now holds requirements and phased plan; removed `.cursor/agents/requirement-refinement.mdc`
- `planning-documents.mdc` — SDDs include actors, functional requirements, acceptance criteria, and non-functional requirements
- `agent-workflow-boundaries.mdc` — lifecycle no longer lists a separate requirements agent
- `rule-feedback-writer` — merged `config-writer` scope: skills placement and stack-rule extension; ADR vs rule guidance unchanged
- Feature design specs (SDDs) live under `docs/sdd/<slug>.md` instead of `docs/feature/<slug>.md`; see `docs/sdd/README.md`
- Test execution reports live under `docs/sdd/test-reports/<slug>.md` instead of `docs/test-reports/<slug>.md`; see `docs/sdd/test-reports/README.md`
- Investigation reports live under `docs/investigation/<slug>.md` instead of `investigation-<topic>.md` at the project root; see `docs/investigation/README.md`
- `code-investigator` — reports must include APIs involved, flow diagrams, code pointers, and reproduction scenarios per `investigation-reports.mdc`

### Removed

- `requirement-refinement` subagent and `docs/requirements/` as a separate artifact path

### Added

- `docs/sdd/README.md` — SDD location and relationship to ADRs
- `docs/sdd/test-reports/README.md` — test report location and migration from `docs/test-reports/`
- Workflow rule `test-reports.mdc` — required sections for test execution reports
- `docs/investigation/README.md` — investigation report location and migration from project root
- Workflow rule `investigation-reports.mdc` — required sections for investigation reports
- Architectural Decision Records under `.cursor/adr/` (README, `0000-template.md`) for consuming repos
- Workflow rule `architectural-decisions.mdc` — when to write ADRs, filename convention, sections, agent ownership
- Agent and boundary integration: `architect-planner` authors ADRs; `phase-executor` follows Accepted ADRs; `doc-sync` links only; `rule-feedback-writer` may persist durable arch feedback as ADRs

## [1.1.0] - 2026-06-03

### Changed

- Made agent workflow and subagent definitions framework-agnostic — no Node.js, TypeScript, or stack-specific rule paths in agents; optional sibling standards repos documented as merge-as-needed

## [1.0.0] - 2026-06-03

### Added

- Repository layout: `README.md`, `CONTRIBUTING.md`, `CHANGELOG.md`, `OWNERS.md`
- Workflow rules under `.cursor/rules/`:
  - `agent-workflow-boundaries.mdc` — subagent lifecycle, handoffs, parallelisation
  - `planning-documents.mdc` — feature plans under `docs/feature/`
  - `documentation-sync.mdc` — sync planning docs after implementation and verification
- Subagent definitions under `.cursor/agents/`:
  - `requirement-refinement`, `code-investigator`, `architect-planner`
  - `phase-executor`, `doc-sync`, `test-runner`, `rule-feedback-writer`
- Extracted from [genai_node_rules](https://github.com/ola-mobility/genai_node_rules) to keep Node standards focused on development conventions only

[Unreleased]: https://github.com/ola-mobility/genai_agent_rules/compare/v1.1.0...HEAD
[1.1.0]: https://github.com/ola-mobility/genai_agent_rules/compare/v1.0.0...v1.1.0
[1.0.0]: https://github.com/ola-mobility/genai_agent_rules/releases/tag/v1.0.0
