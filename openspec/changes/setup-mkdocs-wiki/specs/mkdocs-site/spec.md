## ADDED Requirements

### Requirement: mkdocs.yml exists with Material theme and Mike versioning
The repository SHALL contain `mkdocs.yml` at the root configured with: `site_name: EAP Documentation`, `site_url: https://willemmotopp.github.io/eap-docs/`, Material theme, light/dark palette toggle, navigation features (tabs, sections, expand, top), search plugin, markdown extensions (admonition, pymdownx.details, pymdownx.superfences, pymdownx.tabbed, pymdownx.tasklist, tables), and `extra.version.provider: mike`.

#### Scenario: MkDocs builds without errors
- **WHEN** `mkdocs build --strict` is run from the repo root
- **THEN** the build completes with exit code 0 and produces a `site/` directory

#### Scenario: Material theme renders
- **WHEN** the built site is opened in a browser
- **THEN** the Material theme is applied with a search bar, navigation tabs, and dark/light mode toggle visible

### Requirement: docs/ directory structure matches navigation
The `docs/` directory SHALL contain subdirectories: `getting-started/`, `roles/product-owner/`, `roles/scrum-master/`, `roles/tester/`, `roles/developer/`, `roles/devops/`, `scrum/events/`, `scrum/definitions/`, `practices/`, `infrastructure/` — each containing at minimum the files referenced in the `mkdocs.yml` nav.

#### Scenario: No missing files in build
- **WHEN** `mkdocs build --strict` is run
- **THEN** no warnings about missing nav files are produced

### Requirement: requirements.txt pins mkdocs-material and mike
A `requirements.txt` file SHALL exist at the repo root with: `mkdocs-material>=9.5.0,<10` and `mike>=2.0.0,<3`.

#### Scenario: Dependencies install cleanly
- **WHEN** `pip install -r requirements.txt` is run in a clean Python environment
- **THEN** both mkdocs-material and mike are installed without conflicts
