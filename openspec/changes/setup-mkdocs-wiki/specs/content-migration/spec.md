## ADDED Requirements

### Requirement: Onboarding guide migrated to docs/getting-started/
`EAP_Intern_Onboarding_Guide_v1.4.md` SHALL be copied to `docs/getting-started/onboarding-overview.md`. Content SHALL be preserved exactly; only the file name changes.

#### Scenario: Onboarding page accessible in wiki
- **WHEN** a user navigates to Getting Started → Onboarding Overview in the wiki
- **THEN** the full content of the onboarding guide is displayed

### Requirement: UI/UX boundaries doc migrated to docs/practices/
`Wie_doet_Wat_UI_UX_Boundaries_ITNL02_v1.0.md` SHALL be copied to `docs/practices/ui-ux-boundaries.md`. Content preserved exactly.

#### Scenario: UI/UX page accessible
- **WHEN** a user navigates to Best Practices → UI/UX Boundaries
- **THEN** the full content is displayed

### Requirement: VPS configuration migrated to docs/infrastructure/
`vps/TransIP_VPS_Configuration.md` SHALL be copied to `docs/infrastructure/vps-configuration.md`. Content preserved exactly.

#### Scenario: VPS page accessible
- **WHEN** a user navigates to Infrastructure → VPS Configuration
- **THEN** the full VPS configuration content is displayed

### Requirement: Stub pages exist for all nav entries without migrated content
All files referenced in `mkdocs.yml` nav that do not have migrated content SHALL contain a stub Markdown file with a heading and a "Coming soon" note, so `mkdocs build --strict` passes.

#### Scenario: Build succeeds with stubs
- **WHEN** `mkdocs build --strict` is run after migration
- **THEN** the build completes with exit code 0 and no missing-file warnings
