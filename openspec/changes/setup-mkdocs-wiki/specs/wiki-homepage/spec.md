## ADDED Requirements

### Requirement: docs/index.md is the wiki home page
The repository SHALL contain `docs/index.md` as the wiki landing page, listed first in `mkdocs.yml` nav as `- Home: index.md`.

#### Scenario: Home page loads at site root
- **WHEN** a user navigates to the wiki root URL
- **THEN** `docs/index.md` is displayed as the home page

### Requirement: Home page contains role quick-start links
`docs/index.md` SHALL contain direct links to all five role guide overview pages: Product Owner, Scrum Master, Tester/QA, Developer, and DevOps Engineer.

#### Scenario: Role links work
- **WHEN** a trainee clicks their role link on the home page
- **THEN** they are taken to the corresponding role overview page

### Requirement: Home page explains version scheme
`docs/index.md` SHALL describe the versioning scheme: `2026-01` (ITNL01/02, January–June 2026), `2026-02` (ITNL03, July–December 2026, future), and `latest` (development), with instructions to use the version selector in the header.

#### Scenario: Version information visible on home page
- **WHEN** a trainee opens the home page
- **THEN** the version scheme and purpose of each version is explained

### Requirement: Home page links to key onboarding document
`docs/index.md` SHALL link to `getting-started/onboarding-overview.md`.

#### Scenario: Onboarding link present
- **WHEN** a new trainee opens the home page
- **THEN** there is a visible link to the Onboarding Overview
