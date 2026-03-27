## Context

The repo has ~30 Markdown files at the root plus `roles/`, `vps/`, `adr/` subdirectories. No MkDocs configuration exists. The briefing specifies MkDocs Material + Mike versioning deployed to GitHub Pages, with all trainee-facing content migrated into a `docs/` tree and role guides split from monolithic files (~800–1000 lines each) into 6 focused sub-pages per role.

## Goals / Non-Goals

**Goals:**
- Professional wiki at `https://willemmotopp.github.io/eap-docs/` with Material theme, search, dark/light mode
- Two initial Mike versions: `2026-01` (frozen for current cohort) and `latest` (development)
- All 5 role guides split into 6 files each: overview, tasks, good-practices, anti-patterns, challenges, quick-reference
- Full navigation matching the `mkdocs.yml` nav structure in the briefing
- GitHub Actions auto-deploy on push to `main` (docs/** or mkdocs.yml changes)

**Non-Goals:**
- Dutch (`docs-nl/`) tree — future change
- Scrum event and practices pages with real content — stubs only in this change
- Deleting original files from repo root/`roles/` — kept for now, cleanup is future
- Custom domain (`docs.motoppdemo.nl`) — future step
- Authentication on GitHub Pages

## Decisions

### D1: `docs/` directory with copied content (not `docs_dir: "."`)

**Decision:** Create a proper `docs/` directory and copy/split content into it. `mkdocs.yml` uses the default `docs_dir: docs`.

**Rationale:** The briefing explicitly specifies this structure. It also enables clean splitting of role guides into multiple files, allows MkDocs stub pages to exist without cluttering the repo root, and keeps the wiki's source tree isolated from the raw document archive.

**Alternatives considered:** `docs_dir: "."` with nav whitelist (simpler, no file duplication) — rejected per briefing requirements which call for the `docs/` structure and file splitting.

### D2: Material theme with Mike versioning

**Decision:** Use `mkdocs-material>=9.5.0` and `mike>=2.0.0` as specified in the briefing. Mike manages version directories in the `gh-pages` branch.

**Rationale:** Material provides the best out-of-box UX (search, dark mode, TOC integration, navigation tabs). Mike is the de-facto MkDocs versioning tool — it writes versioned subdirectories to `gh-pages` and maintains a `versions.json` that the Material version switcher reads.

**Alternatives considered:** Single-version MkDocs (no Mike) — rejected; briefing requires `2026-01` / `latest` version switching.

### D3: Role guides split into 6 files per role

**Decision:** Split each role guide along these section boundaries:
1. `overview.md` — Role Overview + Key Responsibilities
2. `tasks.md` — Concrete Tasks (Sprint 0 + per-sprint checklists)
3. `good-practices.md` — Good Practice Scenarios (all 3)
4. `anti-patterns.md` — Anti-Patterns (all 4)
5. `challenges.md` — Common Challenges & Solutions
6. `quick-reference.md` — Quick Reference Checklists + Tips for Success + Getting Help + Remember

**Rationale:** All role guides follow the same section structure. Split points are natural H2 boundaries. 6 files per role keeps each file to ~130–180 lines (readable in one sitting). MkDocs renders them as separate pages with individual URLs, enabling deep linking.

**Alternatives considered:** Keep each role as a single long page — rejected per briefing's content guidelines (split files >800 lines).

### D4: GitHub Actions deploys `latest` on every push; `2026-01` deployed manually once

**Decision:** The workflow deploys only `latest` on automated pushes. The `2026-01` version is deployed once manually with `mike deploy 2026-01 -t "Cohort 2026-01 (ITNL01/02)"` and then frozen.

**Rationale:** `2026-01` is a stable snapshot for the current cohort — it should not be overwritten by every push to `main`. `latest` is the development/preview version that always tracks `main`. Cohort versions are deployed explicitly by staff.

**Alternatives considered:** Deploy both versions on every push — rejected; would overwrite the frozen cohort version on every documentation update.

### D5: Stub pages for Scrum events, practices, infrastructure

**Decision:** Create stub `index.md`-style pages for nav sections that don't have content yet (scrum events, practices, infrastructure) so MkDocs builds without missing-file warnings.

**Rationale:** The `mkdocs.yml` nav references these files. Without them, `mkdocs build --strict` fails. Stubs prevent build failures while making clear these sections need content.

### D6: No manual authentication — local git credentials and built-in GITHUB_TOKEN

**Decision:** No PATs, SSH keys, or secrets are configured. Local `mike deploy` + `git push` commands use the developer's existing git credentials. The GitHub Actions workflow uses the built-in `${{ github.token }}` via `permissions: contents: write`.

**Rationale:** The briefing v1.1 explicitly removes all credential/token references. Built-in GITHUB_TOKEN is sufficient for pushing to `gh-pages` within the same repo. Local git credentials are already configured on the developer machine — no extra setup needed.

**Alternatives considered:** GitHub PAT stored as a repo secret — rejected; unnecessary for same-repo pushes and introduces credential management overhead.

## Risks / Trade-offs

- **Risk: GitHub Pages not enabled on repo** → Mitigation: task 4.7 includes the one-time manual step (repo Settings → Pages → gh-pages branch). Requires repo admin access.
- **Risk: `mike` rewrites `gh-pages` history** → Mitigation: workflow uses `fetch-depth: 0` to ensure full history is available, preventing force-push conflicts.
- **Risk: Splitting role guides introduces broken internal links** → Mitigation: role guide source files use no internal cross-links between sections; split is safe.
- **Risk: `requirements.txt` version drift** → Mitigation: pin minor versions (`>=9.5.0,<10` for material, `>=2.0.0,<3` for mike).

## Open Questions

- Should GitHub Pages be configured for the org URL or a custom domain (`docs.motoppdemo.nl`)? Custom domain requires DNS configuration by staff.
