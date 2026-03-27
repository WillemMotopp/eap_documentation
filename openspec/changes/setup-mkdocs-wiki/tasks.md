## 1. Structure & Configuration

- [x] 1.1 Create `requirements.txt` with `mkdocs-material>=9.5.0,<10` and `mike>=2.0.0,<3`
- [x] 1.2 Create `mkdocs.yml` with Material theme, Mike versioning, full nav, and all markdown extensions per briefing
- [x] 1.3 Create `docs/index.md` homepage with role quick-start table, version scheme description, and onboarding link
- [x] 1.4 Create `.github/workflows/deploy-docs.yml` — triggers on `docs/**` / `mkdocs.yml` changes to `main`, installs dependencies, runs `mike deploy latest`, sets default, pushes `gh-pages`
- [x] 1.5 Create `docs/` subdirectory skeleton: `getting-started/`, `roles/product-owner/`, `roles/scrum-master/`, `roles/tester/`, `roles/developer/`, `roles/devops/`, `scrum/events/`, `scrum/definitions/`, `practices/`, `infrastructure/`

## 2. Content Migration

- [x] 2.1 Copy `EAP_Intern_Onboarding_Guide_v1.4.md` → `docs/getting-started/onboarding-overview.md`
- [x] 2.2 Copy `Wie_doet_Wat_UI_UX_Boundaries_ITNL02_v1.0.md` → `docs/practices/ui-ux-boundaries.md`
- [x] 2.3 Copy `vps/TransIP_VPS_Configuration.md` → `docs/infrastructure/vps-configuration.md`
- [x] 2.4 Create stub pages for all nav entries without real content: `scrum/events/` (5 files), `scrum/definitions/` (2 files), `practices/git-workflow.md`, `practices/code-review.md`, `practices/testing-strategy.md`, `infrastructure/deployment.md`

## 3. Role Guide Splitting

- [x] 3.1 Split `roles/Role_Guide_Product_Owner_v1.0.md` into 6 files under `docs/roles/product-owner/` (overview, tasks, good-practices, anti-patterns, challenges, quick-reference)
- [x] 3.2 Split `roles/Role_Guide_ScrumMaster_v1.0.md` into 6 files under `docs/roles/scrum-master/`
- [x] 3.3 Split `roles/Role_Guide_Tester_v1.0.md` into 6 files under `docs/roles/tester/`
- [x] 3.4 Split `roles/Role_Guide_Developer_v1.0.md` into 6 files under `docs/roles/developer/`
- [x] 3.5 Split `roles/Role_Guide_DevOps_v1.0.md` into 6 files under `docs/roles/devops/`

## 4. Build, Version & Deploy

> **Authentication note:** No manual auth setup needed. Local `git push` uses existing git credentials. GitHub Actions uses the built-in `GITHUB_TOKEN` — no secrets to configure.

- [x] 4.1 Install dependencies locally: `pip install -r requirements.txt`
- [x] 4.2 Build locally and verify: `mkdocs build --strict` (must exit 0 with no warnings)
- [ ] 4.3 Serve locally and verify: `mkdocs serve` — check homepage, role pages, navigation, search
- [ ] 4.4 Deploy version `2026-01` with Mike: `mike deploy 2026-01 -t "Cohort 2026-01 (ITNL01/02)"` then `git push origin gh-pages`
- [ ] 4.5 Deploy version `latest` with Mike: `mike deploy latest -t "Latest (Development)"` → `mike set-default latest` → `git push origin gh-pages`
- [ ] 4.6 Verify version switching locally: `mike serve` — confirm both `2026-01` and `latest` appear in selector
- [ ] 4.7 Enable GitHub Pages on repo (manual step): Settings → Pages → Source: `gh-pages` branch, root `/`
- [ ] 4.8 Commit all new files and push to `main` — verify GitHub Actions `deploy-docs` workflow runs successfully

## 5. Verification

- [ ] 5.1 Confirm site accessible at `https://willemmotopp.github.io/eap-docs/`
- [ ] 5.2 Confirm homepage renders with role links and version description
- [ ] 5.3 Confirm version selector shows `2026-01` and `latest`
- [ ] 5.4 Confirm switching between `2026-01` and `latest` works
- [ ] 5.5 Confirm navigation menu: all role guides accessible (30 pages total)
- [ ] 5.6 Confirm search finds content (e.g., search "Definition of Done")
- [ ] 5.7 Confirm Product Owner guide split correctly — all 6 sub-pages load
- [ ] 5.8 Confirm dark/light mode toggle works
- [ ] 5.9 Confirm GitHub Actions workflow shows green status after last push
