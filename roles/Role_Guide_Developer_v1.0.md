# Developer Role Guide

**Version:** 1.0
**Date:** 2026-03-26
**Audience:** Trainees (Developer role)
**Purpose:** Clear expectations, responsibilities, and practical guidance

---
[TOC]
---

## Role Overview

### What is a Developer?

The Developer is **responsible for building the product** — writing clean, tested, reviewed code that meets acceptance criteria and Definition of Done.

**You are NOT:**
- ❌ The person who decides WHAT gets built (that's the PO)
- ❌ Solely responsible for quality (Tester is your partner)
- ❌ Working alone — collaboration is part of the job
- ❌ Done when code is written — done means deployed, tested, and reviewed

**You ARE:**
- ✅ The person who decides HOW things are built
- ✅ Co-responsible for quality alongside the Tester
- ✅ An active participant in refinement, planning, and review
- ✅ Responsible for following the API contract workflow across the 4-repo structure

### Core Responsibility

**One sentence:** You build the product — backend, frontend, or both — by writing clean, tested, reviewed code that meets acceptance criteria and Definition of Done, within the constraints of the multi-repo architecture.

---

## Key Responsibilities

### 1. Feature Implementation

**You turn user stories into working software.** This means:

**Building:**
- Implement stories from acceptance criteria — not from your own interpretation
- Write backend endpoints (FastAPI) and/or frontend components (React v19 TypeScript) as required by the story
- Write unit tests alongside your code, not after

**Communicating:**
- Mark stories "Ready for Testing" as soon as they work at a basic level — don't wait for the end of the sprint
- Raise technical risks in Sprint Planning before committing to a story
- Keep Jira up to date — the board must reflect reality

**Finishing:**
- "Done" means every item on the Definition of Done is checked — not just "I finished coding it"
- Do not mark a story Done until tests pass, CI is green, and the Tester has signed off

### 2. API Contract Workflow

**The API contract is the foundation of multi-repo collaboration.** This means:

**Backend-first specification:**
- Backend developer writes the OpenAPI spec in `eap-architecture` FIRST, before writing implementation code
- The spec defines the endpoint path, HTTP method, request body, response shape, and error codes
- Implementation follows the spec — not the other way around

**Frontend-against-spec:**
- Frontend developer implements components against the agreed OpenAPI spec
- Do not call endpoints that are not yet specified
- If the spec is missing something you need: raise it before coding, not during integration

**Never simultaneously without a spec:**
- Backend and frontend must never implement both sides of a feature at the same time without an agreed spec
- This causes integration failures, rework, and conflicting assumptions
- The spec takes 1-2 hours to write. The integration pain from skipping it takes days to resolve.

**Spec changes:**
- If the spec needs to change mid-sprint, both sides must agree before either changes their implementation
- Small spec changes: raise in standup, get verbal agreement, update the spec, then code
- Large spec changes: may require a new ADR — check with the team

### 3. Code Review

**Code review is not optional.** This means:

**As reviewer:**
- Review assigned PRs within 24 hours — not reviewing is blocking your teammate
- Use the Definition of Done as your reference, not personal style preferences
- Give constructive, specific feedback: "This query will load all rows without pagination — see `GET /api/v1/requests` in the spec, it should be paginated" not "This is wrong"
- Approve when satisfied; request changes with clear explanation

**As author:**
- Get at least one approval before merging
- Respond to review comments promptly — a PR waiting for your response is blocking a teammate
- Do not merge with unresolved review comments
- Do not merge with failing CI

**What to check in a review:**
- Does the code implement the acceptance criteria?
- Are unit tests added or updated?
- Is CI passing?
- Are there any GDPR concerns (personal data in logs, missing access control)?
- Is the code readable by a teammate with no prior context?
- Does it follow the agreed coding standards?

### 4. Architecture Decision Records (ADRs)

**When you make a significant technical choice, write an ADR.** This means:

**When to write an Application Decision ADR:**
- Choosing a library, framework, or tool that affects the codebase in a meaningful way
- Making a technical trade-off that a future developer needs to understand
- Any decision that is hard to reverse (e.g., choosing a caching approach, a data model, a state management pattern)
- Rule of thumb: if you'd need to explain your choice in a code review, it belongs in an ADR

**When to write a Platform Decision ADR (requires staff review):**
- Decision affects more than one repository
- Decision impacts learning goals of the program
- Decision has significant security or GDPR implications
- Decision changes how the four repos interact (e.g., API versioning strategy, authentication mechanism)

**How to write an ADR:**
- Use the template in `Architecture_Decision_Record_Template_v1.0.md`
- File naming: `ADR-XXX-short-descriptive-title.md` (three-digit zero-padded, lowercase, hyphens)
- Numbering: sequential per repository — each repo has its own sequence
- Status: start with "Proposed", move to "Accepted" after team agrees
- Once "Accepted": content is frozen — only the `Status` field and `Status History` table may be updated

**What not to do:**
- Do not skip writing an ADR because "the team knows why we did it" — future developers do not
- Do not write an ADR after the implementation is already merged and unchangeable — propose it first
- Do not supersede or delete an ADR — create a new one and mark the old one "Superseded"

### 5. GDPR Coding Obligations

**Personal data handling is a technical responsibility.** This means:

**No personal data in logs:**
- Never log employee names, email addresses, leave dates, IP addresses, or any other personal data
- Error messages must not include personal data — return a generic error to the client
- Log IDs (e.g., `user_id=42`) not values (e.g., `user_email=j.doe@example.com`)

**Access control:**
- Users must only be able to access their own data — implement this check in your code, not just in the UI
- "Employee can view their own leave requests" means a request for `user_id=43` must return only user 43's data, even if the caller is authenticated as a different user
- Test access control explicitly: log in as user A, try to access user B's data — this must fail

**Data minimization:**
- Return only the fields the client needs — do not expose full database rows in API responses
- Use response schemas (Pydantic models in FastAPI, TypeScript interfaces in React) to explicitly define what is returned

**Escalate uncertainty immediately:**
- If you are unsure whether something is a GDPR issue: stop and ask the PO or staff before implementing
- GDPR issues discovered after implementation are much harder to fix than GDPR questions asked before coding
- "I wasn't sure if this was allowed" is not acceptable — ask first

### 6. CI/CD Participation

**The CI/CD pipeline is shared infrastructure — treat it accordingly.** This means:

**Keep pipelines green:**
- Run tests locally before every push (`pytest` for backend, `npm test` for frontend)
- If your push breaks CI: fix it before working on anything else
- A broken pipeline blocks the entire team from deploying

**Fix before adding:**
- Never add new code to a codebase with failing tests — fix the tests first
- If tests are failing because they are flaky (not because your code is wrong): raise it as a bug, don't ignore it

**Coordinate on deployment:**
- Check with DevOps before adding new environment variables, secrets, or infrastructure dependencies
- Document new configuration requirements in the relevant README or configuration guide
- Never hardcode environment-specific values (URLs, credentials, ports) in code

---

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

---

## Good Practice Scenarios

### Scenario 1: API Contract Collaboration

**Context:** Sprint Planning. PO has story "Employee can view their leave request history." Backend developer and frontend developer are both in the sprint.

**What happens:**

After Sprint Planning ends, backend developer raises it immediately:

> **Backend Dev:** "Before either of us starts coding, let me write the OpenAPI spec for the history endpoint. Give me a few hours."

Backend developer opens `eap-architecture` and writes:

```yaml
GET /api/v1/requests
Query parameters:
  - page (integer, default 1)
  - page_size (integer, default 20)
Response:
  200 OK:
    items: array of RequestSummary
    total: integer
    page: integer
    page_size: integer
```

> **Frontend Dev:** "I reviewed your spec. One thing — I'll need to filter by status (pending, approved, rejected) in the UI. Can we add a `status` query parameter?"

> **Backend Dev:** "Good catch. Adding it now."

Both developers review the updated spec together, agree it covers everything they need, and then start coding independently:

- Backend implements the `GET /api/v1/requests` endpoint against the spec
- Frontend implements the `RequestHistoryPage` component against the spec

On integration day, both sides connect and the integration test passes on the first attempt.

> **Tester:** "API contract tests are all green. Moving on to acceptance criteria."

**Why this is good:**
- No back-and-forth during implementation — both sides had a clear contract
- The frontend developer's input (status filter) improved the spec before any code was written
- Integration was smooth because both sides built to the same spec
- The spec is now in `eap-architecture` for future reference and for the QA team to use in API contract tests

---

### Scenario 2: Writing and Getting an ADR Accepted

**Context:** Sprint 2. Developer wants to add caching to the backend to reduce database load on the `GET /api/v1/requests` endpoint. Unsure if they need an ADR.

**What happens:**

Developer thinks it through:

> **Developer (to self):** "Does this affect multiple repos?" → No, just `eap-backend`.
> "Is it hard to reverse?" → Somewhat — if we pick a specific caching library, removing it later takes effort.
> "Would a future developer need to understand why we did this?" → Yes.

Decision: **Application Decision ADR needed.**

Developer writes `ADR-002-backend-caching-strategy.md` in `eap-backend/adr/`, status: "Proposed".

In standup:

> **Developer:** "I want to add caching to the requests endpoint. I've written ADR-002. Can the team review it today? I want to start implementing tomorrow."

Team reviews async. Backend dev gets this comment:

> **Teammate:** "ADR-002 proposes Redis. Why not in-memory cache first? Redis adds infrastructure complexity. We haven't set it up on the VPS yet."

Developer updates the ADR:

- Adds "Alternatives Considered" section with Redis vs. in-memory cache
- Changes recommendation to: use Python `functools.lru_cache` initially; evaluate Redis if performance testing shows it's insufficient
- Updates status: "Accepted" after team verbal agreement in standup

Developer implements the in-memory cache and references the ADR in the commit message:

```
feat(api): add in-memory caching for requests endpoint (EAP-67)

See ADR-002 in eap-backend/adr/ for decision rationale.
```

**Why this is good:**
- The decision was made visible before implementation — the team had a chance to improve it
- Team input changed the recommendation from Redis (complex, new infrastructure) to in-memory cache (simple, reversible)
- The ADR explains the "why" for future developers — the commit message alone would not
- The implementation is easier, and the team can escalate to Redis later if needed, with ADR-002 as the baseline

---

### Scenario 3: Incremental Development with Tester Feedback

**Context:** Sprint 2, Day 3. Developer has finished the basic leave request form — it submits to the backend, stores the data, and shows a confirmation message. Validation is not yet complete.

**What happens:**

Developer could wait and deliver everything at the end of the sprint. Instead:

> **Developer:** "The basic form flow works end-to-end. I'm marking it 'Ready for Testing' now. Validation still needs work — I'll have that tomorrow."

Tester picks it up on Day 3 afternoon:

> **Tester:** "Form submits without required fields filled in — that's a High severity bug. Also, no error shown if end date is before start date."

Developer fixes both issues Day 4 morning — the context is still fresh:

> **Developer:** "Fixed. Added required field validation and date order check. Re-marking Ready for Testing."

Tester re-tests Day 4 afternoon:

> **Tester:** "Required fields are validated. Date check works. Found one more edge case: if you enter the same start and end date, it accepts it. Is that valid?"

Developer asks PO:

> **PO:** "Same-day leave should be allowed — that's a single day off."

> **Developer:** "Got it — no change needed. Adding a comment in the code so future developers know this is intentional."

Story is fully Done by end of Day 5, giving the Tester two full days before Sprint Review.

**Why this is good:**
- Bugs were found and fixed while the code was fresh in the developer's mind
- Tester had enough time to do a thorough job — not a one-hour rush at the end
- An edge case question was resolved with the PO before implementation rather than guessed at
- The story was Done by Day 5 of 10 — reducing sprint-end risk significantly

---

## Anti-Patterns (What Goes Wrong)

### Anti-Pattern 1: Solo Developer

**What it looks like:**

Developer works alone, makes no progress updates, and marks everything Done in the last two days of the sprint:

**Days 1-8:** All stories stay in "In Progress." Standup updates: "Still working on it."

**Day 9:**

> **Developer:** "I'm done. Marking everything Done."
>
> **Tester:** "I just got all of this to test — an hour before Sprint Review?"
>
> **Scrum Master:** "How are we going to demo untested features?"

**Sprint Review:**

> **Stakeholder:** "The form crashes when I try to submit."
>
> **Developer:** "It worked on my machine..."

**Why it's bad:**
- No time to fix bugs before Sprint Review — untested code is not Done code
- Tester is overwhelmed and cannot do a proper job in one hour
- Team has no visibility into sprint health — no one knows if you are on track or blocked
- Sprint Review becomes a bug showcase instead of a value demonstration

**Symptoms:**
- Stories all move from "In Progress" to "Done" in the last two days of the sprint
- Tester says "I got everything to test yesterday"
- Sprint Review shows bugs that would have been caught in Day 3 if testing had started earlier
- Standup updates never change: "still working on it"

**How to fix it:**

**Immediate:**
- Mark stories "Ready for Testing" as soon as the core flow works — even without all edge cases handled
- Give specific progress updates in standup: "Leave request form is 80% done — should have it ready for testing tomorrow morning"
- Communicate blockers immediately: "I'm stuck on the authentication middleware. I've been stuck since yesterday. Can someone help?"

**Long-term:**
- Break your work into small, testable increments — aim to have something for the Tester every 2 days
- Think of the Tester as your quality partner, not someone who checks your work at the end
- Understand that sprint-end surprises are a team problem, not just your problem

---

### Anti-Pattern 2: Gold-Plater

**What it looks like:**

Story: "Employee can submit a leave request using a form."

Acceptance criteria: start date, end date, leave type, submit button, confirmation message.

Developer's interpretation:

> **Developer (to self):** "I'll build a proper form. Animated transitions, custom date picker, full WCAG 2.1 accessibility, reusable component library, dark mode support..."

**Day 6 of Sprint:**

> **Scrum Master:** "How is the leave request form going?"
>
> **Developer:** "I'm still building the date picker component. It's almost done."
>
> **Scrum Master:** "The acceptance criteria say 'start date and end date inputs.' Did the PO ask for a custom date picker?"
>
> **Developer:** "No, but a native date input looks bad. I wanted to do it right."

**Sprint Review:**

> **PO:** "The form isn't done. We committed to this story."
>
> **Developer:** "The date picker alone took three days. I thought it was important."

**Why it's bad:**
- Sprint commitment was missed — the team cannot rely on your estimates if you regularly add unasked-for scope
- PO's priorities are ignored — they decided what to build, you built something else
- Sprint Goal may be missed because a story the team depended on isn't done
- Future stories that depended on this one are now blocked

**Symptoms:**
- Stories regularly take 2-3x their estimate
- Developer says "I wanted to do it right" or "I was adding value"
- Team regularly misses Sprint Goal
- PO is surprised by what was built

**How to fix it:**

**Immediate:**
- Build exactly what the acceptance criteria say. Nothing more.
- Before adding anything: "Is this in the acceptance criteria?" If no → stop, add a story to the backlog
- Ask the PO if additional scope is genuinely needed before building it: "I could add a custom date picker — is that something you want? It would add 2 days."

**Mindset shift:**
- The acceptance criteria define what Done looks like — they are not a minimum, they are the target
- "Good enough to ship" is a real engineering value — you can always improve later
- New ideas belong in the backlog, not in the current sprint

**When you see a genuinely valuable improvement:**
- Tell the PO: "I noticed we could improve X. It would take Y hours. Should I add a story?"
- Let the PO decide — that's their job

---

### Anti-Pattern 3: "It Works on My Machine" Developer

**What it looks like:**

Developer finishes the leave request endpoint, tests it locally, everything works. Marks story "Ready for Testing."

CI fails:

> **GitHub Actions:** Tests: 3 failed. Build: FAILED.

> **Tester:** "I can't test this — CI is red and the deployment failed."

> **Developer:** "It works perfectly on my machine though. The CI must be broken."

> **DevOps:** "CI is not broken. Your test is importing a module that doesn't exist in the test environment."

> **Developer:** "I'll look at it later — I'm working on a new story."

**Next day:** CI is still red. Two other PRs are blocked waiting to merge.

> **Scrum Master:** "The pipeline has been red for 24 hours. Nobody can deploy."

**Why it's bad:**
- Broken CI blocks the entire team from deploying — one person's broken pipeline stops everyone
- "Done" stories may not actually work in the shared environment — they just work locally
- DevOps and teammates waste time investigating a problem that should have been caught before push
- Trust in the team's ability to ship erodes

**Symptoms:**
- CI is frequently red
- Team can't deploy to the test environment
- Tester can't test because the shared environment is broken
- "It works on my machine" becomes a running team joke

**How to fix it:**

**Before every push:**
- Run the full test suite locally: `pytest` (backend), `npm test` (frontend)
- Check that your code runs with the same environment variables that CI uses — not just your local `.env`
- Never push code you haven't run

**After every push:**
- Check CI status — within 10 minutes of pushing
- If CI breaks: fix it before starting any new work

**General rules:**
- Never merge a PR with failing CI — no exceptions
- Test against the shared test environment, not just localhost
- If you add a new dependency: check that it is in `requirements.txt` or `package.json` — not just installed locally

---

### Anti-Pattern 4: Scope Ignorer

**What it looks like:**

PO defined acceptance criteria for "Employee can submit a leave request":
- Form with start date, end date, leave type
- Validation of dates
- Confirmation message on submission

Developer thinks:

> **Developer (to self):** "I'll also add manager approval while I'm in this code — it's closely related. And email notifications. And a status badge on the list view."

**Day 8:** Developer opens a PR. The PR adds 1,200 lines of code.

> **Reviewer:** "Wait — there's an approval workflow in here. That wasn't in the story."
>
> **Developer:** "I thought it made sense to add it — we'd have to touch this code anyway."

> **PO:** "We have a separate story for approval — and it has different acceptance criteria. Now I don't know what's in the sprint and what isn't."

> **Another Developer:** "My approval workflow story is 80% done. Now yours conflicts with mine."

**Why it's bad:**
- Undisclosed changes hide complexity and make reviews harder
- May conflict with other stories being built simultaneously by teammates
- PO loses control over what is and isn't in the sprint
- The extra work is unestimated — nobody accounted for the time, so estimates are meaningless

**Symptoms:**
- PRs include features not in the story description
- Conflicts with other team members' work during integration
- PR reviews surface surprising additions
- Estimates become meaningless because developers regularly add unplanned scope

**How to fix it:**

**Immediate:**
- Acceptance criteria = scope boundary. Period.
- If you see related work that would be valuable: "PO, I could also implement manager approval while I'm in this code — it would take an extra day. Should I, or do you want it in its own story?"
- Implement only what was agreed. Save everything else for the backlog.

**Practice:**
- Before opening a PR: re-read the acceptance criteria. Does your PR implement all of them? Does it implement anything beyond them?
- If yes to the second question: remove the extra work into a separate branch and create a backlog story

---

## Common Challenges & Solutions

### Challenge 1: "I don't know how to estimate this story"

**Example:** PO presents a story: "Employee receives a push notification when their leave request is approved." You have never implemented push notifications before.

**The problem:**
Giving a confident estimate for something you've never done is guessing. Guessing leads to wrong sprint commitments, missed sprints, and team frustration.

**Solution:**

Say so in refinement — out loud, to the team:

> **Developer:** "I'm not sure how long this takes — I've never implemented browser push notifications. I could spike it: spend a day exploring how it works and what the implementation would look like, then give a proper estimate."

A **spike** is a short (typically 1-2 day) exploration task whose goal is to reduce uncertainty, not to produce shippable code.

- Spikes are legitimate sprint items — add them to the backlog as a task
- After the spike, re-estimate the story with real knowledge
- Never pretend you know when you don't — the team needs honest estimates to plan realistically

**What not to say:**
- ❌ "I'll estimate 3 points" (when you have no idea — this is false confidence)
- ❌ "I'll estimate 13 points to be safe" (padding estimates is dishonest and wastes sprint capacity)
- ✅ "I don't know yet. Can we spike it?"

---

### Challenge 2: "The API spec isn't agreed yet and we're already in the sprint"

**Example:** Sprint 2 starts. Backend and frontend both have stories for the manager approval feature. No one wrote the API spec in Sprint 0. Both developers want to start coding.

**The problem:**
If backend and frontend implement the same feature without an agreed spec, they will make different assumptions. Integration will fail. One or both sides will need to rework their code.

**Solution:**

Stop. Write the spec first — even a rough version — before anyone writes implementation code.

> **Backend Dev:** "Before we start coding, let's write the spec together. It'll take 30 minutes."
>
> **Frontend Dev:** "Agreed. Let's do it now."

In 30 minutes, they write:

```yaml
POST /api/v1/requests/{id}/approve
Request body: { "comment": string (optional) }
Response 200: { "id": integer, "status": "approved", "approved_at": datetime }
Response 403: { "error": "not authorized" }
Response 404: { "error": "request not found" }
```

Both developers review it, agree, and then code independently.

**If one developer is blocked waiting for the other to write the spec:**
- Pair program the spec together — this is exactly the right use of pairing
- 30 minutes of pairing > 2 days of integration debugging

**Rule:** No implementation without an agreed spec. Even a draft spec written in 30 minutes is better than no spec.

---

### Challenge 3: "My code touches personal data — is this a GDPR issue?"

**Example:** Implementing `GET /api/v1/requests/{id}` — returns a leave request including employee name, email, and dates. You are adding a debug log line that includes the response.

**The problem:**
Logging personal data (name, email, leave dates) is a GDPR violation. Personal data in logs can be accessed by anyone with log access — not just the intended recipient of the data.

**Solution:**

Check the GDPR Coding Checklist (see Quick Reference Checklists below) before writing the code.

For the specific log line question:

> **Developer (to self):** "I want to log the full response for debugging. But the response includes employee name and email. That's personal data. I should not log the full response."

Instead, log only non-personal identifiers:

```python
# ✅ GOOD: log IDs, not personal data
logger.info(f"Request {request_id} retrieved for user {user_id}")

# ❌ BAD: log personal data
logger.info(f"Returned request: {response_body}")  # Contains name, email, dates
```

**When in doubt, ask before coding:**

> **Developer:** "PO, this endpoint returns user email addresses in the response. Is that intentional? The frontend is showing them in the request history list."
>
> **PO:** "Good catch — the list view shouldn't show email. Only the detail view should. I'll update the acceptance criteria."

**GDPR Coding Checklist:**
- [ ] No personal data (name, email, dates, IP) in log messages
- [ ] Access control: verify user can only access their own data
- [ ] No sensitive data in error messages returned to the client
- [ ] Data minimization: return only the fields needed, not all fields in the database row
- [ ] If unsure: stop and ask PO or staff before implementing

**Never** assume GDPR compliance is someone else's problem — it is a coding responsibility.

---

### Challenge 4: "My PR has been waiting for review for 2 days"

**Example:** You opened a PR on Monday morning. It's Wednesday afternoon. No one has reviewed it. You can't merge, and you're blocked.

**The problem:**
If the team agreed in the Definition of Done that code review should happen within 24 hours, this is a broken team agreement — not just an inconvenience.

**Solution:**

**Step 1:** Ping the reviewer directly in Teams — do not wait for them to notice:

> "Hey, can you review PR #42 today? I've been waiting since Monday and I'm blocked on the next story."

**Step 2:** If no response by end of day: raise it in standup the next morning:

> "I'm blocked on PR #42 — it's been waiting for review for 2 days. Can someone pick it up today?"

**Step 3:** If the team is consistently slow at reviews: raise it in the Retrospective:

> "PR reviews took an average of 3 days this sprint. Our DoD says 24 hours. Can we talk about how to fix this?"

**Prevention:**
- When you open a PR: immediately ping your reviewer in Teams with the link — do not assume they will notice
- Make PRs small — a 50-line PR gets reviewed faster than a 500-line PR
- Offer to pair review: "I'll review yours if you review mine"

**What not to do:**
- ❌ Merge without review ("I'll ask for review after merge") — this defeats the purpose of code review
- ❌ Wait silently for 3 days before saying anything — you are blocked, say so

---

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

**END OF DEVELOPER ROLE GUIDE**
