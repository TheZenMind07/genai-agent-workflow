# Software design documents (SDDs)

Feature design specs and verification reports for the agent workflow live under **`docs/sdd/`**.

## SDD (plan)

One markdown file per feature:

```txt
docs/sdd/<feature-slug>.md
```

An SDD is the single planning artifact for a feature: requirements (actors, functional and
non-functional requirements, acceptance criteria), scope, phased delivery, API and storage
notes, sequence diagrams, and phase status. Structure and required sections are defined in
`.cursor/rules/planning-documents.mdc`.

## Test reports

Verification reports from `test-runner` live under:

```txt
docs/sdd/test-reports/<feature-slug>.md
```

Use the same slug as the matching SDD when verifying phased work. Structure and required
sections are defined in `.cursor/rules/test-reports.mdc`. See `docs/sdd/test-reports/README.md`.

## SDD vs ADR

| Artifact | Location | Purpose |
|----------|----------|---------|
| **SDD** | `docs/sdd/<slug>.md` | What to build and how to deliver it in phases |
| **Test report** | `docs/sdd/test-reports/<slug>.md` | Command evidence and coverage for verification |
| **ADR** | `.cursor/adr/NNNN-*.md` | Durable cross-cutting decisions and trade-offs |

Do not store ADRs under `docs/sdd/`. Link from the SDD to relevant **Accepted** ADRs and test
reports instead of duplicating full decision or verification narratives.

## Migrating older layouts

- **`docs/feature/`** — move plans to `docs/sdd/<slug>.md` and update links in ADRs and test reports.
- **`docs/test-reports/`** (repo root) — move reports to `docs/sdd/test-reports/<slug>.md`.
- **`docs/requirements/`** — merge each `docs/requirements/<slug>.md` into the matching SDD under
  `docs/sdd/<slug>.md` using the requirements sections in `planning-documents.mdc`, then retire the
  separate file. Do not maintain parallel requirements and SDD files for the same feature.
