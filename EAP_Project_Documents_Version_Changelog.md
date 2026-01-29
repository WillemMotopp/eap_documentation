# EAP Project Documents - Version Changelog

**Last Updated:** 2026-01-06

---

## Version 1.1 Updates (2026-01-06)

### EAP_Intern_Onboarding_Guide v1.0 → v1.1

**Changes in v1.1:**
- Added **"Available tooling and infrastructure"** section with:
  - GitHub (private repositories, Git Flow)
  - Jira (paid license)
  - GitHub Actions (CI/CD)
  - TransIP VPS (Linux deployment)
  - Microsoft Teams (communication)
- Added **"Development responsibility"** subsection under team roles
- Added **"Architecture and technical decisions"** section with:
  - When to write ADRs
  - ADR process overview
  - Architecture governance (prescribed vs. team decisions)
- Updated **Definition of Ready** to include "architectural impact is identified"
- Updated **Definition of Done** to include "architectural decisions documented"
- Added **"First week checklist"** for onboarding
- **Added GDPR awareness to first week checklist**
- **Added Product Owner specific GDPR checklist items**

**Reason for updates:**
- Feedback from kickoff indicated need for concrete tooling information
- Architecture governance approach needs to be communicated
- Provide clearer onboarding structure
- **GDPR awareness from day 1 - Product Owner must receive requirements from staff**

---

### Definition_of_Done_Template v1.0 → v1.2

**Changes in v1.1:**
- Added **"Architecture"** section with:
  - Architectural impact documentation requirement
  - ADR writing and review requirement
  - Architecture diagram updates
- Added **"Notes on 'if applicable'"** section explaining when requirements apply
- Enhanced **"Testing"** section with "Test coverage is adequate" requirement
- Enhanced **"Code"** section with "Code follows agreed coding standards"

**Changes in v1.2:**
- Added **"Privacy & Data Protection"** section with:
  - Personal data handling review
  - No sensitive data in logs or error messages
  - Data retention implications
  - Access control requirements
  - Privacy by design principles

**Reason for updates:**
- v1.1: Align with architecture documentation expectations, clarify selective application
- v1.2: GDPR compliance is legal requirement - must be checkpointed in every feature

---

## New Documents (2026-01-06)

### Architecture_Decision_Record_Template v1.0

**Purpose:**
- Provide standard template for documenting architectural and technical decisions
- Explain when and how to write ADRs
- Include complete example ADR
- Provide guidance on ADR categories, numbering, and best practices
- **Explain multi-repository ADR organization and numbering strategy**
- **Include GDPR as key example requiring ADR**

**Contents:**
- What is an ADR and why use them (including Git storage rationale)
- When to write an ADR (with examples **including GDPR compliance**)
- ADR process (6 steps with Git workflow)
- Complete template in markdown format with Repository field
- Example ADR (database schema versioning)
- **Multi-repository numbering explanation** (sequential per repo, not global or prefixed)
- **ADR organization by repository** (which ADR goes in which repo)
- **Cross-repository reference guidelines**
- File naming conventions
- **GDPR examples in Platform and Application Decision categories**
- Tips for writing good ADRs
- FAQ section (including multi-repo questions)

**Rationale:**
- Architecture decisions need to be documented for future reference
- Team needs clear guidance on decision documentation
- Standard format ensures consistency
- **Multi-repo setup requires clear conventions for ADR organization**
- Sequential numbering per repo is industry standard and simplest for team
- **GDPR requires architectural decision - must be explicit example**

---

### EAP_Repository_Structure_Guide v1.0

**Purpose:**
- Comprehensive guide for working with multi-repository structure
- Explain structure, rationale, and conventions for 4 repositories
- Provide practical workflows for cross-repo coordination
- **Clarify staff responsibilities including GDPR consultation**

**Contents:**
- Overview of 4 repositories (eap-architecture, eap-backend, eap-frontend, eap-qa)
- Detailed structure for each repository
- Why multi-repository was chosen (references ADR-001)
- Working across repositories (Git workflow, feature development, commit conventions)
- API contract management (OpenAPI in eap-architecture)
- Cross-repository ADR references
- ADR decision matrix (which repo for which decision)
- Versioning and synchronized releases
- CI/CD per repository
- Coordination tools (Jira, Teams, standups) - Updated with two separate Teams for staff/trainee separation
- Common pitfalls and solutions
- First week checklist **with staff GDPR consultation checklist**

**Rationale:**
- Multi-repo structure needs clear documentation
- Team needs practical guidance on cross-repo workflows
- Prevents common coordination issues
- Complements ADR template with organizational context
- **Staff GDPR responsibilities must be explicit and scheduled**

---

### EAP_Product_Vision v1.1

**Purpose:**
- Comprehensive product vision document for the Enterprise Application Project
- Define what the EAP system does and who it serves
- Provide context for all development work
- **Include GDPR compliance requirements and privacy by design**

**Contents:**
- Executive summary and vision statement
- Problem statement (current state vs. future state)
- Core workflow (Submit → Approve → Fulfill)
- User roles (Requester, Approver, Admin) with detailed capabilities
- Request types (hardware, software, access, services)
- Key features for MVP (organized by user role)
- Non-functional requirements (performance, security, usability, reliability)
- **Privacy & GDPR Compliance section** (lawful basis, user rights, technical implementation, staff/team responsibilities)
- Example user stories for each epic
- Out of scope (what's NOT in MVP)
- Success metrics (usage, performance, quality, process)
- Technology constraints (references tech stack ADR)
- Product roadmap (tentative sprint breakdown)
- Design principles
- Product Owner responsibilities
- Q&A section for clarifications

**Changes from v1.0:**
- Added comprehensive Privacy & GDPR Compliance section
- Clarified staff responsibilities (DPO/legal consultation)
- Added privacy by design requirements
- Included GDPR-driven user stories examples

**Rationale:**
- Team needs clear understanding of what they're building
- Product Owner needs foundation document to refine
- Prevents scope creep and misaligned expectations
- Provides context for all user stories and technical decisions
- **GDPR compliance is legal requirement - must be clear from day 1**
- Expands on high-level vision from kickoff presentation

---

### EAP_Kickoff_Presentation v1.0 → v1.1

See **EAP_Kickoff_Presentation_CHANGELOG.md** for details.

---

## Baseline v1.0 Documents (2026-01-05)

The following documents remain at v1.0 and are **frozen** per Cohort Baseline Archive policy:

**Strategy & Governance:**
- Cohort_Baseline_Archive_README_v1.0.md
- EAP_Project_Initiation_Document_Product_Focused_v1.0.md

**Intern-Facing:**
- EAP_Sprint_Guide_Interns_v1.0.md
- Definition_of_Ready_Template_v1.0.md (superseded by v1.1)

**Staff-Only:**
- EAP_Operational_Execution_Planning_v1.0.md
- EAP_Staff_Kickoff_Briefing_Script_v1.0.md
- EAP_Coach_Program_Manager_Guide_v1.0.md
- EAP_Assessment_Framework_Per_Sprint_v1.0.md
- EAP_Incident_Observation_Reflection.md (no version)

---

## Document Status Summary

| Document | v1.0 Status | v1.1 Status | Current Version |
|----------|-------------|-------------|-----------------|
| Cohort Baseline Archive README | ✓ Frozen | - | v1.0 |
| Project Initiation Document | ✓ Frozen | - | v1.0 |
| Intern Onboarding Guide | ✓ Superseded | ✓ Current | **v1.1** |
| Sprint Guide for Interns | ✓ Current | - | v1.0 |
| Definition of Ready Template | ✓ Current | - | v1.0 |
| Definition of Done Template | ✓ Superseded | ✓ Current | **v1.1** |
| Operational Execution Planning | ✓ Current | - | v1.0 |
| Staff Kickoff Briefing Script | ✓ Current | - | v1.0 |
| Coach & Program Manager Guide | ✓ Current | - | v1.0 |
| Assessment Framework | ✓ Current | - | v1.0 |
| Incident Observation | ✓ Current | - | (no version) |
| **ADR Template** | - | **✓ New** | **v1.0** |
| **Kickoff Presentation** | ✓ Superseded | ✓ Current | **v1.1** |

---

## Version Control Policy

### Frozen Documents
Documents marked as "Baseline v1.0" are **frozen** for this cohort:
- Cannot be changed during cohort execution
- Changes for future cohorts require new baseline version
- Any necessary clarifications should be communicated separately

### Active Documents
Documents at v1.1 or newly created:
- Can be updated during cohort if needed
- Updates require version increment and changelog entry
- Must maintain backwards compatibility where possible

### Superseded Documents
- Superseded versions remain available for reference
- Teams should migrate to latest version
- Old versions clearly marked as "Superseded by vX.X"

---

## Future Updates

### Under Consideration

**EAP_Sprint_Guide_Interns → v1.1** (Priority: Low)
- Add brief mention of architecture documentation expectations
- Reference ADR Template

**EAP_Operational_Execution_Planning → v1.1** (Priority: Low)
- Add architecture governance details once finalized
- Add tooling setup checklist for staff

**Definition_of_Ready_Template → v1.1** (Priority: Medium)
- Currently unchanged, but could add architecture considerations
- Alignment with DoD v1.1

---

## Change Request Process

To request a document update:
1. Identify specific need and affected document
2. Propose changes to staff
3. Staff reviews against baseline policy
4. If approved: update version, add to changelog, communicate to team
5. Update document inventory

---

**Document Control**
- Created: 2026-01-06
- Owner: Motopp Staff
- Review: As needed
