## ADDED Requirements

### Requirement: GitHub Actions workflow deploys latest on push to main
The repository SHALL contain `.github/workflows/deploy-docs.yml` that triggers on push to `main` when files under `docs/**`, `mkdocs.yml`, or `.github/workflows/deploy-docs.yml` change. The workflow SHALL install `mkdocs-material` and `mike`, configure git identity, run `mike deploy latest`, set `latest` as default, and push to the `gh-pages` branch. The workflow SHALL NOT use any stored secrets or PATs — authentication is handled by the built-in `GITHUB_TOKEN` via `permissions: contents: write`.

#### Scenario: Push to main triggers wiki update
- **WHEN** a commit touching `docs/**` or `mkdocs.yml` is pushed to `main`
- **THEN** the `deploy-docs` workflow runs and updates the `latest` version on GitHub Pages

#### Scenario: Push without docs changes does not trigger workflow
- **WHEN** a commit touching only non-docs files (e.g., `roles/*.md`) is pushed to `main`
- **THEN** the `deploy-docs` workflow is NOT triggered

### Requirement: Workflow uses pinned action versions
All `uses:` entries in the workflow SHALL reference a specific version tag (e.g., `actions/checkout@v4`, `actions/setup-python@v4`), not a branch name like `@main`.

#### Scenario: Pinned versions in workflow
- **WHEN** the workflow file is read
- **THEN** every `uses:` line specifies a version tag, not `@main` or `@latest`

### Requirement: Workflow fetches full git history
The checkout step in the workflow SHALL use `fetch-depth: 0` so Mike has access to the full git history needed to manage the `gh-pages` branch.

#### Scenario: Full history fetch
- **WHEN** the workflow runs
- **THEN** the checkout step includes `fetch-depth: 0`

### Requirement: 2026-01 version is deployed once and frozen
The `2026-01` version SHALL be deployed manually with `mike deploy 2026-01 -t "Cohort 2026-01 (ITNL01/02)"` and SHALL NOT be redeployed by the automated workflow. Only `latest` is redeployed automatically.

#### Scenario: 2026-01 visible in version selector
- **WHEN** the deployed site's version selector is opened
- **THEN** both `2026-01` and `latest` appear as selectable versions
