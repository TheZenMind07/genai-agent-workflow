# Changelog

All notable changes to the Cursor agent workflow rules and subagent definitions in this repository are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [Unreleased]

### Added

- `.cursor/hooks.json` and `subagentStop` scripts to auto-invoke **doc-sync** after
  **phase-executor** and **test-runner** via `followup_message`
- `workflow-hooks.mdc` — hook installation, matchers, and requirements

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
