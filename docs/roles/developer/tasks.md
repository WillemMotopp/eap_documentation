# Developer — Concrete Tasks

## Concrete Tasks

### During Sprint 0 (Preparation Week)

**Your ONLY job this week: Understand the codebase and prepare for Sprint 1**

**Day 1:**
- [ ] Clone all four repositories: `eap-architecture`, `eap-backend`, `eap-frontend`, `eap-qa`
- [ ] Read the README of each repository — understand what each one does
- [ ] Set up local backend development environment: Python virtual environment, install dependencies, run FastAPI locally
- [ ] Set up local frontend development environment: `npm install`, run React app locally

**Day 2:**
- [ ] Read the existing OpenAPI spec in `eap-architecture` — understand what endpoints already exist
- [ ] Run the backend and frontend locally and verify they connect to each other
- [ ] Read the Product Vision (`EAP_Product_Vision_v1.1.md`) — understand what you are building and why
- [ ] Note: what problem does the system solve? Who are the users? What are the GDPR requirements?

**Day 3:**
- [ ] Attend the Definition of Done refinement session — add the developer perspective:
  - Unit tests must be added or updated
  - Code review by at least one teammate required
  - CI must be passing before merge
  - No personal data in logs or error messages
- [ ] Review the ADR template (`Architecture_Decision_Record_Template_v1.0.md`)
- [ ] Understand when to write an Application Decision ADR vs. a Platform Decision ADR (see Key Responsibilities section above)

**Day 3-4:**
- [ ] Attend backlog refinement sessions facilitated by the PO
- [ ] Estimate stories using Planning Poker — the team estimates, the PO facilitates
- [ ] For each story, ask yourself:
  - "Do I understand how to build this?"
  - "Are there any technical risks I should raise?"
  - "Does this story need a backend change, a frontend change, or both?"
  - "Do I need to write an ADR before implementing this?"

**Day 4-5:**
- [ ] Set up your local test environment (`eap-qa`) — understand how to run E2E tests
- [ ] Identify any story in the Sprint 1 candidate list that might require an ADR before implementation
- [ ] Raise these in refinement: "Story X requires a decision on Y — should we write an ADR first?"

**End of Sprint 0:**
- [ ] You can run all four repositories locally
- [ ] You have estimated Sprint 1 stories honestly
- [ ] You understand the API contract workflow
- [ ] You know where to write an ADR and when
- [ ] You understand the GDPR coding obligations

**Success criteria:** You can open your laptop, run the entire stack locally, and explain to a teammate what each repository does.

### During Each Sprint (Ongoing)

#### Sprint Planning

- [ ] Participate actively in estimating stories — use Planning Poker, give honest estimates
- [ ] Raise technical risks before committing: "This story needs a backend schema change — that's extra effort, our estimate should account for that"
- [ ] Help split stories that seem too large: "We could split this into backend-only (5 points) and frontend-only (3 points)"
- [ ] Commit to a realistic set of stories — never commit to more than the team can genuinely deliver
- [ ] For each committed story, confirm: "Do I understand how to build this? Are there any unknowns I should spike first?"

#### Daily Development Work

**Every day:**
- [ ] Attend standup — report what you finished yesterday, what you are working on today, and any blockers
- [ ] Check CI status of your open PRs — if CI is red, fix it before starting new work
- [ ] Check Jira — are your stories reflecting current reality?

**Branch and commit discipline:**
- Branch naming: `feature/EAP-XXX-short-description`
  - Example: `feature/EAP-42-leave-request-form`
- Commit messages: `type(scope): description (EAP-XXX)`
  - Example: `feat(api): add leave request endpoint (EAP-42)`
  - Example: `fix(frontend): validate end date after start date (EAP-43)`
  - Example: `test(backend): add unit tests for request creation (EAP-42)`
- Types: `feat`, `fix`, `docs`, `test`, `refactor`, `chore`, `ci`

**Marking stories ready:**
- Mark stories "Ready for Testing" as soon as the core functionality works — do not wait for the end of the sprint
- "Ready for Testing" does not mean perfect — it means the Tester can start, and you can fix bugs as they come in
- Giving the Tester early access = more time to find and fix bugs before Sprint Review

**PR Checklist — before opening every PR:**
- [ ] Branch named correctly: `feature/EAP-XXX-short-description`
- [ ] Commit messages follow format: `type(scope): description (EAP-XXX)`
- [ ] Unit tests added or updated
- [ ] CI passing locally (`pytest` for backend, `npm test` for frontend)
- [ ] All DoD items checked against the story
- [ ] PR description explains what changed and why (not just "implemented story")
- [ ] No personal data in logs or error messages
- [ ] No secrets, API keys, or credentials in code

#### Code Review

- [ ] Review assigned PRs within 24 hours — this is a commitment, not a suggestion
- [ ] Focus on: correctness (does it implement the acceptance criteria?), readability (can a teammate understand this?), DoD compliance (are tests there? Is CI green? Any GDPR concerns?)
- [ ] Do NOT focus on: personal style preferences, minor formatting nitpicks (let the linter handle those)
- [ ] Be specific and constructive in comments — a comment that says "this needs to be fixed" with no explanation is not helpful

#### Mid-Sprint Refinement

- [ ] Attend refinement — this is how the next sprint is prepared
- [ ] Estimate upcoming stories — use what you learned this sprint to give better estimates
- [ ] Raise technical questions early: "Story X says 'email notifications' — are we using a library for that? We should decide before we plan it in"
- [ ] If a story needs an ADR before it can be implemented: say so now, not in Sprint Planning

#### Sprint Review

- [ ] Help demo your work if asked — be prepared to show the feature working
- [ ] Explain technical decisions briefly if stakeholders ask: "We chose to paginate the response because the list could grow to thousands of records" — not jargon, plain explanation
- [ ] Listen to stakeholder feedback — if something needs changing, feed it back to the PO
