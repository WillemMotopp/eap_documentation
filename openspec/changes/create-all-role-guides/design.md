## Context

The EAP documentation repository contains staff-authored guides for trainees. Two role guides already exist (`Role_Guide_Product_Owner_v1.0.md`, `Role_Guide_Tester_v1.0.md`) and serve as the canonical reference format. Three roles — Scrum Master, Developer, and DevOps Engineer — currently have no dedicated guide; trainees in these roles rely on the generic `EAP_Intern_Onboarding_Guide_v1.1.md`, which describes roles only at a high level.

This change is documentation-only. There are no code dependencies, APIs, or data models involved.

## Goals / Non-Goals

**Goals:**
- Produce three new role guides matching the structure and depth of the existing PO guide
- Cover EAP-specific context (multi-repo workflow, VPS on TransIP, FastAPI/React stack, Jira, GDPR obligations) in each guide
- Register new documents in the inventory and changelog
- Each guide is self-contained: a trainee with no other context can use it from day one

**Non-Goals:**
- Rewriting or versioning the existing Tester or PO guides
- Creating Dutch (NL) translations (those can follow as a separate change)
- Generating PDF exports (done manually or via a separate CI step)
- Defining new Scrum processes — guides describe the EAP process as it already exists

## Decisions

### D1: Match PO guide structure exactly

**Decision:** All three new guides use the identical top-level section order as `Role_Guide_Product_Owner_v1.0.md`.

**Rationale:** Trainees switching between role guides should find the same navigation landmarks. Structural consistency also makes future NL translations straightforward.

**Alternatives considered:** Free-form structure per role — rejected because it would force readers to learn a new layout for each guide.

### D2: Single English file per role at v1.0

**Decision:** Each guide ships as `Role_Guide_<Role>_v1.0.md` with version 1.0, frozen for the current cohort.

**Rationale:** Matches the version control policy in CLAUDE.md. Frozen baseline prevents mid-cohort drift that would confuse trainees already using the guide.

**Alternatives considered:** Starting at v1.1 (living document) — rejected; v1.0 signals a stable, reviewed baseline.

### D3: DevOps guide covers both pipeline and VPS operations

**Decision:** The DevOps guide combines CI/CD pipeline responsibilities with VPS/infrastructure responsibilities under one document.

**Rationale:** In EAP cohorts, one trainee typically holds both responsibilities. A single guide avoids artificial splits. Sections are clearly labelled so future cohorts with split roles can read only the relevant part.

**Alternatives considered:** Separate `Role_Guide_Pipeline_v1.0.md` and `Role_Guide_VPS_v1.0.md` — rejected; adds inventory complexity for a single-person role.

### D4: Developer guide covers both backend and frontend

**Decision:** `Role_Guide_Developer_v1.0.md` covers both backend (FastAPI/Python) and frontend (React/TypeScript) responsibilities in a unified guide with clearly marked sub-sections.

**Rationale:** Most EAP trainees contribute to both layers; separating the guides would require trainees to read two documents. Role-specific callouts (e.g., "Backend: write OpenAPI spec first") make specialization visible without splitting the guide.

## Risks / Trade-offs

- **Risk: Guide is too long to read** → Mitigation: Each section has a one-sentence summary at the top; Quick Reference checklists allow skimming.
- **Risk: EAP-specific details become stale** → Mitigation: Frozen at v1.0 for the cohort; staff can bump to v1.1 next cohort via the standard version control process.
- **Risk: Overlap between Developer and DevOps guides on deployment steps** → Mitigation: Developer guide defers deployment detail to the DevOps guide by name; cross-references are explicit.

## Open Questions

- None blocking implementation. Staff should review and approve all three guides before distributing to trainees.
