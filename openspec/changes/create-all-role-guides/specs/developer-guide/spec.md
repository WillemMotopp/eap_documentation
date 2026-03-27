## ADDED Requirements

### Requirement: Developer role guide exists
The repository SHALL contain `roles/Role_Guide_Developer_v1.0.md` as a standalone guide for trainees assigned to backend and/or frontend development in the EAP program.

#### Scenario: File is present
- **WHEN** a trainee navigates to the `roles/` directory
- **THEN** `Role_Guide_Developer_v1.0.md` is present and readable

### Requirement: Guide covers role identity
The guide SHALL define what the Developer is and is not in the EAP context. It SHALL clarify that developers decide HOW things are built, work within the multi-repo structure, and are co-responsible for quality alongside the Tester.

#### Scenario: Role clarity
- **WHEN** a trainee reads the Role Overview
- **THEN** they can distinguish their "how" responsibility from the PO's "what" responsibility

### Requirement: Guide describes multi-repo workflow responsibilities
The guide SHALL explain that the EAP codebase is split across four repositories (eap-architecture, eap-backend, eap-frontend, eap-qa) and describe the developer's obligation to follow the API contract workflow: backend defines the OpenAPI spec first, frontend implements against the spec.

#### Scenario: API contract awareness
- **WHEN** a developer reads the Key Responsibilities section
- **THEN** they understand that OpenAPI spec changes must be committed in eap-architecture before frontend implementation begins

### Requirement: Guide describes ADR responsibilities
The guide SHALL explain when a developer MUST write an Architecture Decision Record (ADR), referencing the ADR template and the Platform Decision vs Application Decision distinction from the repository structure guide.

#### Scenario: ADR trigger awareness
- **WHEN** a developer reads the ADR section
- **THEN** they can identify at least two conditions that require a Platform Decision ADR vs two that require an Application Decision ADR

### Requirement: Guide provides Sprint 0 concrete task checklist
The guide SHALL provide a day-by-day Sprint 0 checklist covering: cloning all four repositories, setting up local dev environments, reading the OpenAPI spec, reviewing the DoD with a testing perspective, and attending refinement to estimate stories.

#### Scenario: Sprint 0 setup complete
- **WHEN** a developer completes all Sprint 0 checklist items
- **THEN** they can run the backend and frontend locally and have reviewed the existing API contract

### Requirement: Guide provides per-sprint task checklists
The guide SHALL include checklists for: Sprint Planning (technical feasibility input), daily development work (PR checklist, branch naming, commit format), review/refinement support, and Sprint Review demo preparation.

#### Scenario: PR checklist presence
- **WHEN** a developer looks up the PR process in the guide
- **THEN** they find a checklist including: branch naming convention, commit message format, DoD items to verify, and code review requirements

### Requirement: Guide contains three good-practice scenarios
The guide SHALL contain exactly three worked scenarios: one for backend-frontend API contract collaboration, one for writing and getting an ADR accepted, and one for incremental development with continuous tester feedback.

#### Scenario: Scenario presence
- **WHEN** a trainer counts the good-practice scenarios
- **THEN** exactly three are present with context, dialogue, and "Why this is good" explanation

### Requirement: Guide contains four anti-patterns
The guide SHALL describe four anti-patterns: the Solo Developer (doesn't share progress, surprises team at review), the Gold-Plater (over-engineers beyond story requirements), the "It Works on My Machine" Developer (skips CI/environment testing), and the Scope Ignorer (implements beyond acceptance criteria without PO consent).

#### Scenario: Anti-pattern completeness
- **WHEN** a trainer reviews the Anti-Patterns section
- **THEN** each pattern includes: narrative, why it's bad, symptoms, and how to fix it

### Requirement: Guide covers GDPR coding obligations
The guide SHALL include a section or callout on the developer's GDPR responsibilities: no personal data in logs, access control implementation, data-at-rest encryption awareness, and when to escalate a privacy concern to the PO or staff.

#### Scenario: GDPR coding checklist
- **WHEN** a developer implements a feature involving personal data
- **THEN** the guide provides a checklist of GDPR coding checks to perform before marking the story done

### Requirement: Guide structure matches PO guide
The guide SHALL use the same top-level section order as `Role_Guide_Product_Owner_v1.0.md`.

#### Scenario: Section order validation
- **WHEN** a reviewer compares section headers in the Developer guide to the PO guide
- **THEN** the section order and naming are identical
