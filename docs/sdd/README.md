# Software design documents (SDDs)

Feature design specs for the agent workflow live here as **one markdown file per feature**:

```txt
docs/sdd/<feature-slug>.md
```

An SDD is the phased implementation plan: goal, scope, phases, API and storage notes, sequence
diagrams, and phase status. Structure and required sections are defined in
`.cursor/rules/planning-documents.mdc`.

## SDD vs ADR

| Artifact | Location | Purpose |
|----------|----------|---------|
| **SDD** | `docs/sdd/<slug>.md` | What to build and how to deliver it in phases |
| **ADR** | `.cursor/adr/NNNN-*.md` | Durable cross-cutting decisions and trade-offs |

Do not store ADRs under `docs/sdd/`. Link from the SDD to relevant **Accepted** ADRs instead of
duplicating full decision narratives.

## Migrating from `docs/feature/`

Teams that adopted earlier guidance should rename or move plans from `docs/feature/<slug>.md` to
`docs/sdd/<slug>.md` and update any links in ADRs, test reports, or requirements docs.
