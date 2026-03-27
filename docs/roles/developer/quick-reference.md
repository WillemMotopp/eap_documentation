# Developer — Quick Reference

## Quick Reference Checklists

### Sprint 0 Checklist

- [ ] Clone `eap-architecture`, `eap-backend`, `eap-frontend`, `eap-qa`
- [ ] Read all four READMEs
- [ ] Set up local backend development environment (Python venv, FastAPI running on localhost)
- [ ] Set up local frontend development environment (`npm install`, React app running on localhost)
- [ ] Read the existing OpenAPI spec in `eap-architecture`
- [ ] Run backend and frontend locally and verify they connect to each other
- [ ] Read the Product Vision (`EAP_Product_Vision_v1.1.md`) — understand what you are building
- [ ] Participate in DoD creation — add developer perspective (tests, code review, CI, GDPR)
- [ ] Attend all refinement sessions and estimate stories using Planning Poker
- [ ] Set up local test environment (`eap-qa`) — verify you can run E2E tests
- [ ] Identify Sprint 1 stories that might require an ADR before implementation
- [ ] Read the ADR template (`Architecture_Decision_Record_Template_v1.0.md`)

---

### Sprint Planning Checklist

- [ ] Estimate stories honestly — say when you are uncertain
- [ ] Raise technical risks before committing: schema changes, new infrastructure, unfamiliar technology
- [ ] Ask "Do I understand how to build this?" for every story before committing
- [ ] Help split stories that are too large
- [ ] Ensure Sprint commitment is realistic — based on last sprint's velocity, not on optimism
- [ ] Identify stories that need an API spec written before implementation can start

---

### Daily Development Checklist

- [ ] Attend standup — report yesterday/today/blockers specifically
- [ ] Check CI status of your open PRs — fix before starting new work
- [ ] If story is working at a basic level: mark "Ready for Testing" (do not wait)
- [ ] Review assigned PRs within 24 hours
- [ ] Check Jira board — are your stories accurate?
- [ ] Communicate blockers in standup — do not sit on them

---

### PR Checklist (Before Opening)

- [ ] Branch named correctly: `feature/EAP-XXX-short-description`
- [ ] Commit messages follow format: `type(scope): description (EAP-XXX)`
- [ ] Unit tests added or updated for changed code
- [ ] Full test suite passes locally: `pytest` (backend) or `npm test` (frontend)
- [ ] CI passing — check after push, before requesting review
- [ ] All DoD items checked against the story's acceptance criteria
- [ ] PR description explains what changed and why — not just "implemented EAP-42"
- [ ] No personal data (names, emails, dates) in log statements
- [ ] No sensitive data in error messages returned to the client
- [ ] No secrets, API keys, tokens, or credentials in code or configuration files
- [ ] If new environment variable needed: documented in README or configuration guide

---

### GDPR Coding Checklist

- [ ] No personal data (name, email, leave dates, IP address) in log messages
- [ ] Access control: endpoint verifies user can only access their own data
- [ ] Error messages returned to the client contain no personal data
- [ ] Response schema returns only the fields the client needs (data minimization)
- [ ] If storing or processing personal data: reviewed against Privacy & GDPR section in Product Vision
- [ ] If unsure: stopped and asked PO or staff before implementing

---

### Code Review Checklist (As Reviewer)

- [ ] Does the code implement the acceptance criteria?
- [ ] Are unit tests added or updated?
- [ ] Is CI passing?
- [ ] Any GDPR concerns? (personal data in logs, missing access control, over-exposed response fields)
- [ ] Is the code readable by a teammate who has not seen it before?
- [ ] Does it follow the agreed coding standards?
- [ ] If a new significant technical decision was made: is there an ADR?
- [ ] Are there any obvious performance concerns? (e.g., loading all database rows without pagination)

---

### ADR Decision Checklist

Use this when you are wondering "Should I write an ADR?"

- [ ] Does this decision affect more than one repository? → Platform Decision ADR (requires staff review)
- [ ] Does this decision impact learning goals of the program? → Platform Decision ADR (requires staff review)
- [ ] Does this decision change how the four repos interact? → Platform Decision ADR (requires staff review)
- [ ] Is this a significant technical choice that is hard to reverse? → Application Decision ADR
- [ ] Would a future developer need to understand why this decision was made? → Application Decision ADR
- [ ] Is this decision within established constraints and easy to change later? → No ADR needed (but document in code comments)

---

## Tips for Success

### 1. Mark Stories "Ready for Testing" Early

Do not hoard stories. The Tester needs time to do their job well. Mark a story "Ready for Testing" as soon as the core flow works — even if you know there are edge cases left to handle. The Tester's feedback will tell you what to fix next.

**If you are unsure:** Ask yourself — "Can the Tester start testing the main acceptance criteria right now?" If yes, mark it ready.

### 2. When Uncertain, Ask — A 10-Minute Conversation Prevents 2 Days of Rework

Do not guess at requirements, do not assume you understand a GDPR question, do not implement an API without agreeing on the spec. A quick conversation with the PO, the Tester, or a teammate is almost always faster than discovering you built the wrong thing.

**Ask the PO:** "Is this in scope? Should I also implement X?"
**Ask the Tester:** "How should I set up test data for this? What edge cases should I cover?"
**Ask a teammate:** "Does this approach look right to you? I'm not sure about X."

### 3. Write the OpenAPI Spec Before Writing Implementation Code

This is the single most important workflow rule in the multi-repo structure. Backend writes the spec first, frontend and QA build against it. Skipping the spec does not save time — it causes integration failures that cost far more time to fix.

**Rule:** No implementation without an agreed spec. Even a draft spec is better than no spec.

### 4. Write Tests While You Code, Not After

Writing tests after you finish the implementation is harder and catches fewer issues. Tests written alongside the code are faster to write (you know what the code should do), catch bugs immediately, and give you confidence to refactor.

**Practical habit:** For every function or endpoint you write, write at least one unit test before marking the story "Ready for Testing."

### 5. Keep CI Green — a Broken Pipeline Blocks the Whole Team

When CI is red, the team cannot deploy. When the team cannot deploy, the Tester cannot test in the shared environment. When the Tester cannot test, stories cannot be Done.

**Rule:** If you break CI, fix it before starting any new work. This is not negotiable.

### 6. Read the Acceptance Criteria Twice Before You Start Coding

Read the acceptance criteria before you start. Then read them again. Build exactly what they say. If anything is unclear: ask the PO before you start, not in the middle of the implementation.

**Common mistake:** Starting to code immediately after Sprint Planning, before reading the acceptance criteria carefully — then building the wrong thing.

### 7. "Done" Means Deployed and Tested, Not Just Coded

Code that is finished but not tested is not Done. Code that is tested locally but failing in CI is not Done. Code that passes CI but has not been reviewed is not Done. Code that is reviewed and merged but not deployed is not Done.

**Definition of Done is your checklist** — use it, every story, every time.

---

## Getting Help

### When to Ask the Tester

- "How should I set up the test data for this story? What do you need to be able to test it?"
- "What edge cases should I be testing in my unit tests?"
- "I'm about to mark this Ready for Testing — is there anything specific you need from me first?"
- "The CI test environment is different from my local setup — can you help me understand what I need to configure?"

### When to Ask the Product Owner

- "Is this in scope? Should I also implement X, or should that be a separate story?"
- "The acceptance criteria say Y — does that mean Z is also expected, or only Y?"
- "I could build this two ways — one is simpler but has less flexibility. Which do you prefer?" (when scope is the question, not technical approach)
- "This feature touches personal data — is that intentional? What exactly should be accessible to which user?"

**Remember:** Technical decisions are yours. Scope decisions are the PO's. If you are not sure which one you are facing: ask.

### When to Ask the DevOps (or a Teammate with DevOps Responsibilities)

- "How do I deploy this to the test environment?"
- "I need a new environment variable — how do I add it to the pipeline?"
- "My code works locally but fails in CI — can you help me understand the environment difference?"
- "I want to add a new service dependency — how does that work with our VPS setup?"

### When to Ask the Scrum Master

- "I'm blocked and I cannot unblock myself — can you help remove this impediment?"
- "I've been waiting 3 days for a PR review — can you help me get the team's attention on this?"
- "I'm not sure how to handle a situation with a teammate — can we talk?"
- "I think our sprint commitment was unrealistic — can you help us have a conversation about it?"

### When to Ask Staff

- **GDPR uncertainty:** If you are not sure whether a technical implementation is GDPR-compliant, stop and ask staff. Do not guess.
- **Architectural decisions that feel too big:** If a technical choice feels like it will affect the whole project or multiple repos in a significant way, ask staff before writing the ADR
- **Major technical risks:** If you discover a risk in Sprint Planning that could impact the entire sprint or project, raise it with staff
- **Learning goals:** If you feel you are not getting exposure to something important in the program (e.g., you have only worked on frontend and want to understand backend), talk to staff

---

## Remember

**You are learning.** Nobody expects perfect code in Sprint 1.

**Good Developers:**
- Communicate progress daily — no surprises at Sprint Review
- Test before marking Done — coding is not the last step
- Write clean code that teammates can read without a tour guide
- Respect the API contract — spec first, implementation second
- Keep CI green — a broken pipeline is a team problem, not just yours
- Ask when uncertain — a question asked early prevents rework

**You don't need to:**
- Build everything perfectly the first time — iterative improvement is real engineering
- Know every technology in advance — ask for help, spike to learn, be honest about uncertainty
- Work alone — the Tester is your quality partner, the team is your support system
- Solve every problem yourself before mentioning it — blockers mentioned early get resolved early

**Your success = Team delivers working, tested software that meets acceptance criteria and Definition of Done.**

---

**Questions?** Ask your Scrum Master, Tester, or staff coach.
