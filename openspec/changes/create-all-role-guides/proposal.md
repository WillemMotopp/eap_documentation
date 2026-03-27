## Why

The EAP documentation currently has role guides for Product Owner and Tester/QA, but Scrum Master, Developer, and DevOps Engineer — three of the five core EAP roles — have no dedicated guide. Trainees stepping into these roles have no structured reference for expectations, sprint ceremonies, anti-patterns, or daily tasks, forcing them to piece together guidance from the generic onboarding document alone.

## What Changes

- Add `roles/Role_Guide_ScrumMaster_v1.0.md` — full Scrum Master role guide
- Add `roles/Role_Guide_Developer_v1.0.md` — full Developer (backend/frontend) role guide
- Add `roles/Role_Guide_DevOps_v1.0.md` — full DevOps Engineer role guide
- Register all three new documents in `EAP_Project_Documents_Inventory.md`
- Add version entries in `EAP_Project_Documents_Version_Changelog.md`

Each guide follows the exact structure of `roles/Role_Guide_Product_Owner_v1.0.md`:
1. Role Overview (what you are / are not, core responsibility)
2. Key Responsibilities (5–6 numbered sections)
3. Concrete Tasks (Sprint 0 checklist + per-sprint checklist)
4. Good Practice Scenarios (3 worked examples)
5. Anti-Patterns (4 patterns with symptoms and fixes)
6. Common Challenges & Solutions (4 challenges)
7. Quick Reference Checklists
8. Tips for Success
9. Getting Help

## Capabilities

### New Capabilities
- `scrum-master-guide`: Role guide for the Scrum Master — ceremonies, impediment removal, facilitation, anti-patterns
- `developer-guide`: Role guide for the Developer — backend/frontend coding responsibilities, PR workflow, ADRs, anti-patterns
- `devops-guide`: Role guide for the DevOps Engineer — pipeline, VPS, deployment, monitoring, anti-patterns

### Modified Capabilities
- `document-inventory`: `EAP_Project_Documents_Inventory.md` gains three new rows (one per guide)
- `document-changelog`: `EAP_Project_Documents_Version_Changelog.md` gains three new entries

## Impact

- `roles/` directory: 3 new Markdown files (~900 lines each)
- `EAP_Project_Documents_Inventory.md`: 3 new rows
- `EAP_Project_Documents_Version_Changelog.md`: 3 new entries
- No code changes; documentation-only repository
