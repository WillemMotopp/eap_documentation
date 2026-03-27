# Developer — Role Overview

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
