# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This is a **documentation-only repository** for the Enterprise Application Project (EAP) — an internship/training program run by Motopp. It contains no application code, build system, or test suite. All documents are Markdown (with paired PDF exports where applicable).

## Project Context

The EAP is a web-based request management system. The actual code lives in four separate repositories:
- **eap-architecture** — Platform decisions, OpenAPI specs, C4 diagrams, deployment docs
- **eap-backend** — Python/FastAPI application
- **eap-frontend** — React v19 (TypeScript) application
- **eap-qa** — End-to-end and performance tests

This `eap_documentation` repo holds staff-authored project documents (onboarding guides, templates, ADR template, sprint guides, etc.) that are distributed to trainees and staff.

## Document Conventions

### Naming
Files follow the pattern `DocumentName_vX.Y.md` for versioned documents, or `DocumentName.md` for unversioned ones. PDF exports share the same base name (e.g., `EAP_Product_Vision_v1.1.md` + `EAP_Product_Vision_v1.1.pdf`).

### Version Control Policy
- **Frozen documents** (baseline v1.0): cannot be changed during a cohort. These are staff-owned and represent the cohort baseline.
- **Active documents** (v1.1+): can be updated; changes require a version increment and an entry in `EAP_Project_Documents_Version_Changelog.md`.
- **Superseded versions** are kept in the repo for historical reference.

### Document Ownership
- **Staff-owned (frozen):** governance, assessment, staff-only, and baseline template documents.
- **Team-owned (living):** `EAP_Product_Vision`, `Definition_of_Done_Template`, `Definition_of_Ready_Template`, and ADRs written by trainees.

## Architecture Decision Records (ADRs)

ADRs in this repo live in the `adr/` directory. Use the template in `Architecture_Decision_Record_Template_v1.0.md`.

Key ADR rules:
- **File naming:** `ADR-XXX-short-descriptive-title.md` (three-digit zero-padded, lowercase, hyphens)
- **Numbering:** Sequential per repository — each of the four code repos maintains its own sequence independently
- **Immutability:** Content is frozen once status is "Accepted"; only the `Status` field and `Status History` table may be updated afterward
- **Superseding:** Never delete ADRs — create a new ADR and set the old one's status to "Superseded"
- **Cross-repo references:** Always include the repository name and a full GitHub link (e.g., `[eap-architecture ADR-003](...)`)

ADR categories:
- **Platform Decision** — affects multiple repos, hard to reverse, or impacts learning goals; requires staff review
- **Application Decision** — within established constraints, team-owned

## Git Workflow

Branch strategy (Git Flow):
- `main` — production-ready docs
- `dev` — integration branch
- `feature/EAP-XXX-description` — per-ticket branches

Commit message format: `type(scope): description (EAP-XXX)`

Types: `feat`, `fix`, `docs`, `test`, `refactor`, `chore`, `ci`

Example: `docs(adr): add ADR-003 React version decision (EAP-42)`

## Key Documents Index

| Document | Purpose |
|----------|---------|
| `EAP_Product_Vision_v1.1.md` | What the system does; user roles; GDPR requirements |
| `EAP_Intern_Onboarding_Guide_v1.1.md` | Roles, tooling, Scrum events, first-week checklist |
| `EAP_Repository_Structure_Guide_v1.0.md` | Multi-repo workflow, API contract management, ADR matrix |
| `Architecture_Decision_Record_Template_v1.0.md` | Full ADR template, numbering guide, examples |
| `Definition_of_Done_Template_v1.2.md` | DoD including architecture and GDPR/privacy checklist |
| `EAP_Project_Documents_Version_Changelog.md` | Version history for all documents |
| `EAP_Project_Documents_Inventory.md` | Master inventory with audience and status |
| `vps/TransIP_VPS_Configuration.md` | VPS setup, SSH, Nginx, SSL, firewall |

## GDPR Considerations

GDPR compliance is a recurring theme throughout the documentation. When editing or adding documents that touch data handling, user rights, or system behavior, ensure alignment with the Privacy & GDPR Compliance section in `EAP_Product_Vision_v1.1.md`. GDPR-impacting architectural choices require a Platform Decision ADR (with DPO/legal consultation by staff).
