# Test reports

Verification reports from `test-runner` live here as **one markdown file per feature or
verification scope**:

```txt
docs/sdd/test-reports/<feature-slug>.md
```

Use the same kebab-case slug as the matching SDD under `docs/sdd/<feature-slug>.md` when the
report verifies phased feature work. For ad-hoc fixes without an SDD, derive a descriptive slug
from the change scope.

Each report documents diff review, executed tests, command output, coverage when available, and
residual risk. Structure and required sections are defined in `.cursor/rules/test-reports.mdc`.

`doc-sync` links reports from the SDD phase status table; do not mark a phase `Verified` without
a report path and command evidence.

## Migrating older layouts

- **`docs/test-reports/`** (repo root) — move reports to `docs/sdd/test-reports/<slug>.md` and
  update links in SDDs and ADRs.
- **`docs/feature/`** — feature plans belong under `docs/sdd/`; move any feature-scoped test
  reports here with a matching slug.
