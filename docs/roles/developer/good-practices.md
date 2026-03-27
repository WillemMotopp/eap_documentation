# Developer — Good Practice Scenarios

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
