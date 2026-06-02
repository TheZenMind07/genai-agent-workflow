# Changelog

All notable changes to the Cursor agent workflow rules and subagent definitions in this repository are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [Unreleased]

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

[Unreleased]: https://github.com/ola-mobility/genai_agent_rules/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/ola-mobility/genai_agent_rules/releases/tag/v1.0.0
