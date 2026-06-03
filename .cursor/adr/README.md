# Architectural Decision Records

This directory holds **Architectural Decision Records (ADRs)** for the consuming repository.

ADRs capture durable, cross-cutting choices (patterns, boundaries, stack and workflow trade-offs)
so future agents and humans do not rediscover them from code or chat history alone.

## Usage

1. Copy this folder into your project when installing **genai_agent_rules** (see repo README).
2. For each new decision, add `NNNN-short-slug.md` using the next free four-digit prefix.
3. Start from [0000-template.md](./0000-template.md) (copy and rename; do not commit `0000` as a real decision unless you use it intentionally).
4. Follow [.cursor/rules/architectural-decisions.mdc](../rules/architectural-decisions.mdc) for when to write an ADR and required sections.

Feature-specific delivery detail stays in `docs/sdd/<slug>.md`. ADRs explain **why** the
architecture is shaped as it is across features.

## Status lifecycle

- **Proposed** — under discussion; implementers should treat as tentative.
- **Accepted** — active; `phase-executor` and reviewers should follow it.
- **Deprecated** — no longer recommended; may remain for history.
- **Superseded by NNNN** — replaced by a newer ADR; link to the successor file.
