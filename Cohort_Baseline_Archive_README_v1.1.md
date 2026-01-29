---
Document: Cohort_Baseline_Archive_README
Version: 1.1
Status: Approved
Audience: Staff only
Approval required: No
Changes from v1.0: Updated for post-kickoff enhancements (tooling, architecture, GDPR)
---

# Cohort Baseline Archive (CBA) – README

## Purpose of the Cohort Baseline Archive

The **Cohort Baseline Archive (CBA)** contains the complete and approved documentation set that defines the rules, expectations, and governance for a specific cohort of the **Enterprise Application Project (EAP)**.

The CBA exists to:
- ensure fairness and transparency for interns;
- guarantee consistency and discipline among staff;
- provide traceability for assessment, evaluation, and audits;
- enable safe improvement between cohorts without retroactive changes.

Once frozen, the CBA represents the **authoritative baseline** for the cohort.

---

## What "baseline" means

A baseline means that:
- all documents in this archive are approved;
- the content applies to the entire cohort;
- no silent or informal changes are allowed during execution.

A baseline does **not** mean:
- teams cannot adapt their working agreements;
- learning and reflection stop;
- improvements are forbidden.

It means that **governance, roles, and expectations remain stable**.

---

## Baseline Evolution During Cohort Setup

This cohort's baseline evolved in two phases:

### Phase 1: Initial Baseline (v1.0)
Frozen before kickoff with core governance and process documents.

### Phase 2: Enhanced Baseline (v1.1/v1.2)
Updated immediately after kickoff based on:
- Concrete tooling decisions (GitHub, Jira, TransIP VPS)
- Architecture documentation requirements
- GDPR compliance integration (legal requirement)

These updates were made **before Sprint 1** to ensure the team starts with complete information.

**Rationale:** Post-kickoff enhancements provide necessary detail without changing governance principles. The baseline is now frozen for the cohort execution phase.

---

## When this archive is frozen

This archive reached final frozen state:
- Initial freeze: After document approval, before kickoff
- Enhancement phase: Immediately after kickoff (tooling, architecture, GDPR)
- Final freeze: Before Sprint 1 Planning
- Once all required documents have been approved

After final freezing:
- documents may be referenced and enforced;
- changes require a new major version and apply only to future cohorts;
- minor clarifications may be added to separate FAQ documents (not retroactive changes).

---

## Contents of this archive

This Cohort Baseline Archive contains the following approved documents.

### 1. Strategy and Governance

**Stable (v1.0):**
- Project Initiation Document (PID) – v1.0

**Enhanced (v1.1):**
- **Product Vision** – v1.1 (Draft - awaiting Product Owner approval)
  - Added: GDPR compliance requirements
  - Added: Concrete feature descriptions
  - Reason: Team needs clear product understanding from day 1

### 2. Intern-Facing Documents

**Stable (v1.0):**
- Sprint Guide for Interns – v1.0
- Definition of Ready (Template) – v1.0

**Enhanced:**
- **Intern Onboarding Guide** – v1.1
  - Added: Concrete tooling infrastructure (GitHub, Jira, TransIP, Teams)
  - Added: Architecture documentation expectations
  - Added: GDPR awareness in first week checklist
  - Reason: Post-kickoff feedback indicated need for concrete tooling details

- **Definition of Done (Template)** – v1.2 (Draft - team customizes)
  - v1.1: Added architecture documentation checkpoint
  - v1.2: Added privacy & data protection checkpoint
  - Reason: GDPR compliance is legal requirement, must be checkpointed

**New:**
- **Architecture Decision Record Template** – v1.0
  - Purpose: Standard for documenting architectural decisions
  - Includes: Multi-repository numbering strategy, GDPR as key example
  - Reason: Architecture decisions need consistent documentation

- **Repository Structure Guide** – v1.0
  - Purpose: Multi-repository workflows and coordination
  - Includes: 4-repo structure, Git workflow, staff GDPR checklist
  - Reason: Team needs clear guidance on repository organization

### 3. Staff-Only Execution & Governance

**Stable (v1.0):**
- Operational Execution Planning – v1.0
- Staff Kickoff Briefing Script – v1.0
- Coach & Program Manager Guide – v1.0

### 4. Staff-Only Assessment & Reflection

**Stable (v1.0):**
- Assessment Framework per Sprint – v1.0
- Incident Observation & Reflection – (no version)

---

## GDPR Integration

**Legal Context:**
GDPR compliance is a legal requirement for any system processing personal data in the EU. The EAP system processes employee names, email addresses, and request details.

**Staff Responsibilities (documented in multiple locations):**
- Consult with DPO/legal before Sprint 1
- Define lawful basis for data processing
- Set retention policies
- Provide GDPR requirements to Product Owner
- Review team's GDPR compliance ADR

**Team Responsibilities (documented in multiple locations):**
- Product Owner receives GDPR requirements from staff
- Team writes ADR for GDPR compliance approach (Sprint 1)
- Privacy by design implemented from Sprint 1
- Privacy checkpoint in every feature (Definition of Done)

**Documentation Locations:**
- Product Vision v1.1: Comprehensive Privacy & GDPR Compliance section
- Definition of Done v1.2: Privacy & Data Protection checkpoint
- ADR Template: GDPR as platform decision example
- Onboarding Guide v1.1: GDPR awareness checklist
- Repository Structure Guide: Staff GDPR consultation checklist

---

## Document Status Summary

| Document | Version | Status | Frozen |
|----------|---------|--------|--------|
| Project Initiation Document | v1.0 | Approved | Yes |
| **Product Vision** | **v1.1** | **Draft** | **Awaiting PO approval** |
| Sprint Guide for Interns | v1.0 | Approved | Yes |
| Definition of Ready Template | v1.0 | Approved | Yes |
| **Intern Onboarding Guide** | **v1.1** | **Approved** | **Yes** |
| **Definition of Done Template** | **v1.2** | **Draft** | **Team customizes** |
| **ADR Template** | **v1.0** | **Approved** | **Yes** |
| **Repository Structure Guide** | **v1.0** | **Approved** | **Yes** |
| Operational Execution Planning | v1.0 | Approved | Yes |
| Staff Kickoff Briefing Script | v1.0 | Approved | Yes |
| Coach & Program Manager Guide | v1.0 | Approved | Yes |
| Assessment Framework | v1.0 | Approved | Yes |
| Incident Observation | (no version) | Approved | Yes |

---

## Precedence and Hierarchy

In case of questions or conflicts:
1. The **PID** takes precedence over all other documents.
2. **Product Vision** defines what we're building (Product Owner owns, staff approves GDPR).
3. Approved staff governance documents define boundaries and posture.
4. Operational Execution Planning enables execution within those boundaries.
5. Intern-facing documents define how the team works day to day.

No document in this archive may contradict a higher-level document.

**GDPR Exception:** GDPR requirements are non-negotiable regardless of document hierarchy. Legal compliance overrides all other considerations.

---

## Use During the Cohort

During the cohort:
- staff refer to this archive when coaching, observing, or assessing;
- interns are guided based on the approved intern-facing documents;
- discussions about expectations should always reference this baseline;
- **GDPR requirements** must be followed in all features.

If something is unclear, the archive is the **first point of reference**.

**For GDPR questions:**
1. Check Product Vision v1.1 (Privacy & GDPR Compliance section)
2. Check Definition of Done v1.2 (Privacy & Data Protection checkpoint)
3. Consult staff if requirements are unclear
4. Staff consults DPO/legal for legal interpretation

---

## Document Versions - What Changed and Why

### v1.0 → v1.1/v1.2 Updates

**Reason for Updates:**
Post-kickoff feedback revealed that interns needed:
1. Concrete tooling information (not just "we'll use version control")
2. Clear architecture documentation expectations
3. GDPR compliance awareness from day 1 (legal requirement)

**Changes Made:**
- Added concrete tooling details (GitHub private repos, Jira paid, TransIP VPS)
- Created architecture documentation templates (ADR, Repository Structure)
- Integrated GDPR across 5 documents
- Updated checklists for first week awareness

**Governance Principles Unchanged:**
- Team autonomy (application decisions)
- Staff boundaries (platform decisions)
- Scrum framework (sprints, events, roles)
- Assessment criteria (sprint framework)

**These updates provide necessary detail without changing the fundamental EAP approach.**

---

## Why These Updates Are Part of Baseline

**Q: Why not wait until Sprint 1 to provide tooling details?**  
A: Team needs to know what tools they'll use to plan Sprint 1 effectively. Uncertainty about tooling prevents effective planning.

**Q: Why not wait to add GDPR?**  
A: GDPR is a legal requirement. If the team designs database schema without GDPR in mind, it's expensive to fix later. Privacy by design means from Sprint 1, not bolt-on.

**Q: Doesn't this violate the baseline freeze?**  
A: No. The initial baseline was governance and process. These updates add necessary implementation detail before the cohort execution phase begins (Sprint 1). The final freeze is before Sprint 1 Planning.

**Q: What if we need to change something during the cohort?**  
A: Significant changes require new major versions and apply only to future cohorts. Minor clarifications can be added to FAQ documents without retroactive changes.

---

## After the Cohort

After the cohort:
- reflections and lessons learned may be documented separately;
- proposed changes are collected outside this archive;
- a new baseline is created for the next cohort if needed.

The CBA itself remains unchanged as a historical record.

**Lessons to Consider for Next Cohort:**
- Should GDPR be included in initial baseline (v1.0)?
- Should tooling be decided earlier?
- Should Product Vision be created before kickoff?

---

## Baseline Archive Location

**Physical Location:** `/cohort_baseline_archive/[cohort-id]/`

**Contents:**
- All v1.0 documents (initial baseline)
- All v1.1/v1.2 documents (enhanced baseline)
- This README (explains evolution)
- Version changelog (detailed change history)

**Access:**
- Staff: Full access
- Interns: Access to intern-facing documents only
- Read-only for all (no modifications during cohort)

---

## Final Note

> The Cohort Baseline Archive protects both interns and staff  
> by making expectations explicit, stable, and defensible.

This README defines how the archive should be understood and used.

**Key Principle:** Baseline stability serves fairness. Updates made before Sprint 1 ensure the team starts with complete information. Once Sprint 1 begins, the baseline is frozen.

---

## Related Documents

- **EAP_Project_Documents_Inventory.md** - Master list of all documents
- **EAP_Project_Documents_Version_Changelog.md** - Detailed version history
- **EAP_Final_Summary_with_GDPR.md** - Summary of today's work

---

**End of Cohort Baseline Archive README v1.1**

**Archive Status:** Frozen for cohort execution (before Sprint 1)  
**Last Update:** 2026-01-06  
**Next Baseline:** After cohort completion, for future cohorts
