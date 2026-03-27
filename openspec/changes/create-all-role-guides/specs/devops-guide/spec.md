## ADDED Requirements

### Requirement: DevOps Engineer role guide exists
The repository SHALL contain `roles/Role_Guide_DevOps_v1.0.md` as a standalone guide for trainees assigned to DevOps/infrastructure responsibilities in the EAP program.

#### Scenario: File is present
- **WHEN** a trainee navigates to the `roles/` directory
- **THEN** `Role_Guide_DevOps_v1.0.md` is present and readable

### Requirement: Guide covers role identity
The guide SHALL clarify that the DevOps Engineer is responsible for CI/CD pipelines, VPS infrastructure, deployment reliability, and monitoring — not for writing application features. It SHALL note that EAP uses a TransIP VPS (documented in `vps/TransIP_VPS_Configuration.md`).

#### Scenario: Role identity clarity
- **WHEN** a trainee reads the Role Overview
- **THEN** they understand they own the pipeline and infrastructure, not feature delivery

### Requirement: Guide describes CI/CD pipeline responsibilities
The guide SHALL describe the DevOps Engineer's ownership of: GitHub Actions workflows, build/test/deploy pipeline stages, environment configuration, and secrets management. It SHALL reference the four EAP repositories and their individual pipelines.

#### Scenario: Pipeline ownership
- **WHEN** a developer asks "who fixes the broken pipeline?"
- **THEN** the DevOps guide identifies the DevOps Engineer as first responder and describes escalation steps if the fix requires application changes

### Requirement: Guide describes VPS and deployment responsibilities
The guide SHALL describe the DevOps Engineer's responsibility for: SSH access management, Nginx configuration, SSL certificate renewal (Certbot), firewall rules, and deployment scripts. It SHALL cross-reference `vps/TransIP_VPS_Configuration.md` for configuration details.

#### Scenario: VPS cross-reference
- **WHEN** a DevOps trainee needs to renew an SSL certificate
- **THEN** the guide directs them to the VPS configuration document for step-by-step instructions

### Requirement: Guide describes monitoring and alerting responsibilities
The guide SHALL specify that the DevOps Engineer monitors application uptime, pipeline health, and disk/CPU usage, and SHALL describe how to escalate incidents to staff.

#### Scenario: Incident escalation path
- **WHEN** the application is unreachable during a sprint
- **THEN** the guide provides the escalation checklist: check pipeline logs → check VPS logs → notify team in Standup → notify staff if not resolved within 2 hours

### Requirement: Guide provides Sprint 0 concrete task checklist
The guide SHALL provide a day-by-day Sprint 0 checklist: verify VPS SSH access, review existing pipelines, set up deployment environments for dev/test/prod, confirm secrets are in GitHub and not in code, and document the deployment process for the team.

#### Scenario: Sprint 0 infrastructure ready
- **WHEN** a DevOps trainee completes Sprint 0 tasks
- **THEN** all four pipelines run successfully and team members know how to trigger a deployment

### Requirement: Guide provides per-sprint task checklists
The guide SHALL include sprint checklists for: pipeline health checks (start of sprint), deployment of each completed story, Sprint Review environment preparation, and end-of-sprint pipeline report.

#### Scenario: Sprint Review environment check
- **WHEN** a DevOps trainee follows the Sprint Review checklist
- **THEN** they have verified that the demo environment is deployed and accessible before the Sprint Review begins

### Requirement: Guide contains three good-practice scenarios
The guide SHALL contain exactly three worked scenarios: one for setting up a new pipeline step, one for diagnosing and resolving a broken deployment mid-sprint, and one for hardening secrets management after a near-miss.

#### Scenario: Scenario presence
- **WHEN** a trainer counts the good-practice scenarios
- **THEN** exactly three are present with context, actions taken, and "Why this is good" explanation

### Requirement: Guide contains four anti-patterns
The guide SHALL describe four anti-patterns: the "It Deploys Manually" DevOps (skips automation), the Secrets-in-Code DevOps, the "Deploy and Forget" DevOps (no monitoring or rollback plan), and the Overengineered Pipeline (builds tooling the team doesn't understand or need).

#### Scenario: Anti-pattern completeness
- **WHEN** a trainer reviews the Anti-Patterns section
- **THEN** each pattern has narrative, why it's bad, symptoms, and how to fix it

### Requirement: Guide covers security and access control
The guide SHALL include a section on infrastructure security: SSH key management, firewall rules, no root login, and the DevOps Engineer's responsibility to ensure no credentials appear in Git history or CI logs.

#### Scenario: Security checklist
- **WHEN** a DevOps trainee onboards a new team member
- **THEN** the guide provides an access checklist: SSH key added, GitHub access granted, secrets NOT shared in chat

### Requirement: Guide structure matches PO guide
The guide SHALL use the same top-level section order as `Role_Guide_Product_Owner_v1.0.md`.

#### Scenario: Section order validation
- **WHEN** a reviewer compares section headers in the DevOps guide to the PO guide
- **THEN** the section order and naming are identical
