## Why

Trainee documentation currently lives as loose Markdown files scattered across the repo root and subdirectories. There is no navigable wiki, no search, and no versioning per cohort. A MkDocs Material site with Mike versioning gives every cohort a stable, searchable, versioned URL from day one — and auto-deploys on every push to `main`.

## What Changes

- Create `docs/` directory with a structured subdirectory layout for all trainee-facing content
- Migrate existing documentation files into `docs/` subdirectories
- Split each role guide (800+ lines) into 6 focused files per role
- Create `mkdocs.yml` with Material theme, full navigation, Mike versioning support
- Create `requirements.txt` with pinned `mkdocs-material` and `mike` versions
- Create `.github/workflows/deploy-docs.yml` for automated GitHub Pages deployment via Mike
- Create `docs/index.md` as the wiki homepage with role-based quick-start links
- Deploy two initial versions: `2026-01` (current cohort, stable) and `latest` (development)

**Not in scope:** Dutch translations (future `docs-nl/` tree), Scrum event stub pages, practices stub pages, infrastructure stub pages — these are created as stubs only and filled in later.

## Capabilities

### New Capabilities
- `mkdocs-site`: `mkdocs.yml`, `requirements.txt`, `docs/` directory structure, Material theme configuration with Mike versioning support
- `wiki-homepage`: `docs/index.md` — landing page with role quick-start table and version info
- `wiki-deploy`: `.github/workflows/deploy-docs.yml` — automated build and Mike deploy to `gh-pages` on push to `main`
- `content-migration`: copy and reorganise existing docs into `docs/` subdirectories
- `role-guide-splitting`: split all 5 role guide Markdown files (~800–1000 lines each) into 6 files per role under `docs/roles/<role>/`

### Modified Capabilities
<!-- None — original files in root and roles/ are not deleted in this change (cleanup is a separate future step) -->

## Impact

- New directory: `docs/` (~35+ new Markdown files after splitting)
- New files: `mkdocs.yml`, `requirements.txt`, `.github/workflows/deploy-docs.yml`
- New Python dependencies: `mkdocs-material>=9.5.0`, `mike>=2.0.0`
- GitHub repository: Pages must be enabled (Settings → Pages → source: `gh-pages` branch) — one-time manual step by staff
- Site URL: `https://willemmotopp.github.io/eap-docs/` (via `gh-pages` branch managed by Mike)
- Original files in repo root and `roles/` are preserved (not deleted) in this change
