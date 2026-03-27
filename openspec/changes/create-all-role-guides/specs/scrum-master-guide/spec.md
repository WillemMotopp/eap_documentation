## ADDED Requirements

### Requirement: Scrum Master role guide exists
The repository SHALL contain `roles/Role_Guide_ScrumMaster_v1.0.md` as a standalone, self-contained guide for trainees assigned the Scrum Master role in the EAP program.

#### Scenario: File is present
- **WHEN** a trainee navigates to the `roles/` directory
- **THEN** `Role_Guide_ScrumMaster_v1.0.md` is present and readable

### Requirement: Guide covers role identity
The guide SHALL define what the Scrum Master is and is not in the EAP context, including a one-sentence core responsibility statement.

#### Scenario: Role clarity for new trainee
- **WHEN** a trainee reads the Role Overview section
- **THEN** they can identify at least three things the SM is NOT (e.g., project manager, secretary, team boss) and three things the SM IS

### Requirement: Guide lists key responsibilities
The guide SHALL enumerate 5–6 numbered key responsibilities: facilitation of Scrum events, impediment removal, coaching the team on Scrum, protecting the team from external interference, tracking progress, and supporting the PO.

#### Scenario: Complete responsibility list
- **WHEN** a trainer reviews the Key Responsibilities section
- **THEN** all six responsibilities are present with explanatory sub-bullets

### Requirement: Guide provides Sprint 0 concrete task checklist
The guide SHALL include a day-by-day checklist for Sprint 0 covering: setting up the Scrum board in Jira, scheduling all sprint ceremonies, facilitating the team's Definition of Done and Definition of Ready creation, and running the first team retrospective format.

#### Scenario: Sprint 0 readiness
- **WHEN** a trainee completes all Sprint 0 checklist items
- **THEN** they have a configured Jira board, scheduled ceremonies for Sprint 1, and a team-agreed DoD and DoR

### Requirement: Guide provides ongoing sprint task checklist
The guide SHALL include per-sprint checklists for: Sprint Planning facilitation, Daily Standup facilitation, mid-sprint refinement support, Sprint Review facilitation, and Sprint Retrospective facilitation.

#### Scenario: Sprint ceremony coverage
- **WHEN** a trainee checks the "During Each Sprint" section before a ceremony
- **THEN** they find a checklist specific to that ceremony

### Requirement: Guide contains three good-practice scenarios
The guide SHALL contain exactly three worked scenarios illustrating effective SM behavior: one for impediment removal, one for facilitating a difficult retrospective, and one for protecting the team from scope creep mid-sprint.

#### Scenario: Scenario presence
- **WHEN** a trainer counts the good-practice scenarios
- **THEN** exactly three are present, each with context, dialogue, and a "Why this is good" explanation

### Requirement: Guide contains four anti-patterns
The guide SHALL describe four anti-patterns with symptoms and remediation steps: the Absent SM, the Micromanaging SM, the Yes-Person SM (never pushes back), and the Process-Police SM (enforces rules robotically).

#### Scenario: Anti-pattern completeness
- **WHEN** a trainer reviews the Anti-Patterns section
- **THEN** each pattern has: a "what it looks like" narrative, a "why it's bad" explanation, "symptoms" list, and "how to fix it" steps

### Requirement: Guide structure matches PO guide
The guide SHALL use the same top-level section order as `Role_Guide_Product_Owner_v1.0.md`: Role Overview → Key Responsibilities → Concrete Tasks → Good Practice Scenarios → Anti-Patterns → Common Challenges → Quick Reference Checklists → Tips for Success → Getting Help.

#### Scenario: Section order validation
- **WHEN** a reviewer compares section headers in the SM guide to the PO guide
- **THEN** the section order and naming are identical
