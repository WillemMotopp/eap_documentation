## ADDED Requirements

### Requirement: Each role guide is split into 6 files
All five role guide source files SHALL be split into exactly 6 Markdown files each, placed under `docs/roles/<role>/`:
- `overview.md` — Role Overview + Key Responsibilities sections
- `tasks.md` — Concrete Tasks section (Sprint 0 + per-sprint checklists)
- `good-practices.md` — Good Practice Scenarios section (all 3 scenarios)
- `anti-patterns.md` — Anti-Patterns section (all 4 anti-patterns)
- `challenges.md` — Common Challenges & Solutions section
- `quick-reference.md` — Quick Reference Checklists + Tips for Success + Getting Help + Remember sections

The five roles and their source files are:
- `product-owner` ← `roles/Role_Guide_Product_Owner_v1.0.md`
- `scrum-master` ← `roles/Role_Guide_ScrumMaster_v1.0.md`
- `tester` ← `roles/Role_Guide_Tester_v1.0.md`
- `developer` ← `roles/Role_Guide_Developer_v1.0.md`
- `devops` ← `roles/Role_Guide_DevOps_v1.0.md`

#### Scenario: All 30 role guide files exist
- **WHEN** the `docs/roles/` directory is listed
- **THEN** exactly 5 subdirectories exist, each containing exactly 6 Markdown files

### Requirement: Split files preserve all content
Each split file SHALL contain all content from the corresponding sections of the source file. No content SHALL be omitted, paraphrased, or summarised during splitting. Each file SHALL begin with an H1 heading derived from the role name and section name.

#### Scenario: Content integrity after split
- **WHEN** the 6 split files for a role are concatenated
- **THEN** the result contains all content from the original source file (minus only the top-level file header, which is redistributed across files)

### Requirement: Split files use MkDocs admonition formatting where appropriate
Where source files contain checklist items, each split file SHALL preserve the `- [ ]` checkbox format. Anti-pattern and scenario sections MAY use MkDocs admonition blocks (`!!! warning`, `??? example`) to improve readability, but this is optional for the initial migration.

#### Scenario: Checkboxes render correctly
- **WHEN** a tasks page is viewed in the wiki
- **THEN** checkbox items render as interactive task list items (via pymdownx.tasklist)
