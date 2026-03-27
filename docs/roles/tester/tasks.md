# Tester/QA — Concrete Tasks

## Concrete Tasks

### During Sprint 0 (Preparation Week)

**Your job this week: Prepare testing foundation**

**Day 1-2:**
- [ ] Read Product Vision and understand product goals
- [ ] Review user stories in Product Backlog
- [ ] Understand GDPR requirements (testing privacy features)
- [ ] Set up your test environment (access to VPS, test accounts)

**Day 2-3:**
- [ ] Participate in Definition of Done creation
- [ ] Add testing perspective: "When is something truly done?"
- [ ] Ensure DoD includes testing requirements
- [ ] Review Definition of Ready - add "testability" considerations

**Day 3-5:**
- [ ] Participate in backlog refinement sessions
- [ ] For each story, ask: "How will we test this?"
- [ ] Identify stories that need specific test data or setup
- [ ] Flag unclear or untestable acceptance criteria

**Day 4-5:**
- [ ] Help team estimate stories (testing effort is part of estimate)
- [ ] Create initial test plan template for Sprint 1
- [ ] Set up bug tracking approach in Jira
- [ ] Prepare test data for Sprint 1 stories

**End of Sprint 0:**
- [ ] You understand the product and its quality requirements
- [ ] You know which stories are in Sprint 1 and how to test them
- [ ] Test environment is ready
- [ ] Team understands your role and how you'll collaborate

### During Each Sprint (Ongoing)

**Beginning of Sprint (Sprint Planning):**
- [ ] Listen to user story discussions
- [ ] Identify testing approach for each story
- [ ] Note any testing dependencies or blockers
- [ ] Ensure testing effort is considered in team's commitment
- [ ] Ask clarifying questions about acceptance criteria

**During Sprint (Daily Work):**

**Daily:**
- [ ] Attend Daily Standup
- [ ] Report testing progress and any blockers
- [ ] Test completed features (don't wait until end of sprint!)
- [ ] Log bugs in Jira with clear reproduction steps
- [ ] Communicate findings to developers immediately

**Continuous Testing:**
- [ ] Test features as soon as developers mark them "ready for testing"
- [ ] Don't wait - test incrementally throughout sprint
- [ ] Verify bug fixes within 24 hours of developer marking "fixed"
- [ ] Perform quick regression tests when code changes
- [ ] Test on different browsers/devices if relevant

**Mid-Sprint:**
- [ ] Review sprint progress - are we on track for quality?
- [ ] Escalate quality concerns if sprint goal at risk
- [ ] Update test documentation for completed features
- [ ] Prepare any complex test scenarios for remaining work

**Collaboration:**
- [ ] Pair with developers on complex features (test while they code)
- [ ] Help developers write testable code
- [ ] Review Pull Requests from testing perspective (if time permits)
- [ ] Share test results and findings proactively

**End of Sprint (Sprint Review):**
- [ ] Verify all accepted work meets Definition of Done
- [ ] Test the integrated increment (full regression)
- [ ] Prepare quality report for Sprint Review
- [ ] Demo any testing tools or approaches used
- [ ] Document known issues that aren't fixed yet

**End of Sprint (Sprint Retrospective):**
- [ ] Share what worked/didn't work in testing process
- [ ] Suggest improvements to testing approach
- [ ] Discuss quality issues and how to prevent them
- [ ] Commit to testing process improvements

### Types of Testing You Perform

**Functional Testing:**
- Does the feature do what it's supposed to do?
- Do all acceptance criteria pass?
- Happy path scenarios work?

**Negative Testing:**
- What happens with invalid input?
- What if required fields are empty?
- What if user tries something unexpected?

**Edge Cases:**
- Boundary values (min/max dates, very long text, etc.)
- Special characters in input
- Multiple users accessing same data
- Network interruptions or timeouts

**Integration Testing:**
- Do frontend and backend work together?
- Does email sending work end-to-end?
- Do different features interact correctly?

**Regression Testing:**
- Did new changes break existing features?
- Quick smoke test of core functionality

**GDPR/Privacy Testing:**
- Can users export their data?
- Can users request data deletion?
- Is personal data properly protected?
- Are access controls working?

**Usability Testing:**
- Is the interface intuitive?
- Are error messages clear?
- Is the user flow logical?

**Browser/Device Testing:**
- Does it work in Chrome, Firefox, Safari?
- Does it work on mobile (responsive design)?

**Performance Testing (Basic):**
- Does the page load in reasonable time?
- Can it handle multiple simultaneous requests?

---

## How to Write Good Bug Reports

### Bug Report Template

```
TITLE: Clear, specific description (e.g., "Login fails with valid credentials")

SEVERITY: Critical / High / Medium / Low

PRIORITY: Urgent / High / Medium / Low

ENVIRONMENT:
- Browser: Chrome 120.0
- OS: Windows 11
- Server: Test environment (motoppdemo.nl)

STEPS TO REPRODUCE:
1. Navigate to https://motoppdemo.nl/login
2. Enter username: "test@example.com"
3. Enter password: "ValidPass123!"
4. Click "Login" button

EXPECTED RESULT:
User should be logged in and redirected to dashboard

ACTUAL RESULT:
Error message appears: "Invalid credentials" even though credentials are correct
User remains on login page

ADDITIONAL INFORMATION:
- Happens consistently (100% reproduction rate)
- Screenshot attached: [link]
- Network log shows 401 error from /api/auth/login
- Console error: "TypeError: Cannot read property 'token' of undefined"

IMPACT:
Users cannot log in to the application

WORKAROUND:
None found
```

### Severity vs Priority Guide

**Severity = How bad is the bug?**
- **Critical:** System crash, data loss, security breach
- **High:** Core feature completely broken
- **Medium:** Feature works but with significant issues
- **Low:** Minor cosmetic issue or rare edge case

**Priority = How urgently should it be fixed?**
- **Urgent:** Fix immediately (blocks everything)
- **High:** Fix this sprint
- **Medium:** Fix soon (next 1-2 sprints)
- **Low:** Fix when time permits

**Examples:**

**Critical + Urgent:**
"Users cannot submit any requests (500 error)" → Fix NOW

**High + Medium:**
"Date validation allows invalid dates" → Fix this sprint, but has workaround

**Low + Low:**
"Button alignment is 2px off" → Fix when polishing UI
