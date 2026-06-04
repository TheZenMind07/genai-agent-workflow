# Investigation reports

Code and flow investigations from `code-investigator` live here as **one markdown file per topic**:

```txt
docs/investigation/<topic-slug>.md
```

Each report documents how something works, where behaviour lives, or how an incident reproduces:
APIs involved, Mermaid flow diagrams, code pointers, and reproduction scenarios when applicable.

Structure and required sections are defined in `.cursor/rules/investigation-reports.mdc`.

## Migrating from project root

Teams that wrote `investigation-<topic>.md` at the repository root should move files here and
update links in SDDs, test reports, or requirements docs.
