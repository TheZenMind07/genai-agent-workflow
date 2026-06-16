# Architectural Decision Records

ADRs capture durable, cross-cutting choices (patterns, boundaries, stack and workflow trade-offs)
so future agents and humans do not rediscover them from code or chat history alone.

## Location

All ADRs live under **`docs/adr/`** in the consuming repository:

```txt
docs/adr/0001-short-slug.md
docs/adr/0002-another-topic.md
```

## Usage

1. Bootstrap from this folder when starting a new project, or create `docs/adr/` on first decision.
2. For each new decision, add `NNNN-short-slug.md` using the next free four-digit prefix.
3. Start from [0000-template.md](./0000-template.md) (copy and rename; do not commit `0000` as a real decision unless you use it intentionally).
4. Follow the **architectural-decisions** rule from the **genai-agent-workflow** plugin (or
   `.cursor/rules/architectural-decisions.mdc` in your project after install) for when to write
   an ADR and required sections.

Feature-specific delivery detail stays in `docs/sdd/<slug>.md`. ADRs explain **why** the
architecture is shaped as it is across features.

## Status lifecycle

- **Proposed** — under discussion; implementers should treat as tentative.
- **Accepted** — active; `phase-executor` and reviewers should follow it.
- **Deprecated** — no longer recommended; may remain for history.
- **Superseded by NNNN** — replaced by a newer ADR; link to the successor file.

## Migrating from `.cursor/adr/`

If your project used ADRs under `.cursor/adr/`, move files to `docs/adr/` and update links in
SDDs, test reports, and investigation docs. Do not maintain both locations.
