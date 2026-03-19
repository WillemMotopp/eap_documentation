# Tester / QA Role Guide

**Version:** 1.0  
**Date:** 2026-03-03  
**Audience:** Trainees (Tester/QA role)  
**Purpose:** Clear expectations, responsibilities, and practical guidance

---

## Role Overview

### What is a Tester/QA?

The Tester (Quality Assurance) is **responsible for ensuring the product meets quality standards** before it reaches users.

**You are NOT:**
- ❌ Just someone who clicks buttons at the end
- ❌ The "quality police" who rejects everything
- ❌ Only responsible for finding bugs
- ❌ Working alone after developers finish

**You ARE:**
- ✅ Quality advocate throughout the entire development process
- ✅ The person who thinks about edge cases and failure scenarios
- ✅ Preventing bugs, not just finding them
- ✅ Collaborating with developers from story refinement to deployment

### Core Responsibility

**One sentence:** You ensure the team delivers high-quality, working software by testing early, testing often, and thinking about what could go wrong.

---

## Key Responsibilities

### 1. Test Planning & Strategy

**You help the team think about testing from the start:**

**During Refinement:**
- Understand acceptance criteria from testing perspective
- Ask "How will we test this?" for each story
- Identify test scenarios and edge cases
- Flag untestable requirements early

**Before Sprint:**
- Review which stories need which types of tests
- Identify testing dependencies (test data, environments)
- Plan testing approach for the sprint

### 2. Test Design & Execution

**You create and execute tests:**

**Test Design:**
- Write test cases based on acceptance criteria
- Think of edge cases developers might miss
- Design tests for happy path AND failure scenarios
- Consider different user types and data scenarios

**Test Execution:**
- Perform manual testing on completed features
- Execute automated tests (if team has them)
- Test integrations between components
- Verify fixes for bugs
- Perform regression testing (did we break something else?)

### 3. Bug Detection & Reporting

**You find problems and communicate them clearly:**

**Finding Bugs:**
- Test features against acceptance criteria
- Try to break things intentionally
- Test edge cases and boundary conditions
- Look for usability issues and inconsistencies

**Reporting Bugs:**
- Document bugs clearly with steps to reproduce
- Include screenshots/screen recordings
- Assess severity and priority
- Verify bug fixes when developers resolve them

### 4. Quality Advocacy

**You represent quality in team decisions:**

- Speak up if Definition of Done isn't met
- Push back on "ship it broken" pressure
- Advocate for testability in design
- Help team understand quality risks

### 5. Test Automation Support

**You support automated testing (with developers):**

- Identify which tests should be automated
- Help developers understand test scenarios
- Write automated tests if you have coding skills
- Maintain and update existing automated tests

**Note:** In EAP, developers often write automated tests. Your role is to ensure the RIGHT things are tested.

### 6. Documentation & Knowledge Sharing

**You document quality and share learnings:**

- Document test scenarios and results
- Track known issues and workarounds
- Share findings in Sprint Review
- Update test documentation as product evolves

---

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

---

## Good Practice Scenarios

### Scenario 1: Early Testing Collaboration

**Context:** Sprint Planning, team discussing new story "Employee can submit leave request"

**What Tester Does:**

**During story discussion:**

> **Tester:** "I see the acceptance criteria mention 'start date and end date.' Should we test:
> - What happens if end date is before start date?
> - What's the maximum date range allowed?
> - Can users select past dates or only future dates?
> - What about public holidays - should those be handled?"

**Developer:** "Good questions. Let me clarify with the Product Owner..."

**Product Owner:** "End date must be after start date. No maximum range. Only future dates. Holidays are out of scope for this sprint."

**Tester:** "Perfect, I'll test those scenarios. Also, should we test concurrent submissions - what if user submits same request twice?"

**PO:** "Good point - add validation to prevent duplicate submissions within 1 minute."

**Result:**
- ✅ Requirements clarified BEFORE coding
- ✅ Edge cases identified early
- ✅ Acceptance criteria expanded
- ✅ Less rework later

**Why this is good:**
- Tester participated actively in Planning
- Asked "How will we test this?" early
- Helped improve requirements
- Prevented bugs by thinking ahead

### Scenario 2: Incremental Testing During Sprint

**Context:** Sprint Day 3, developer finishes "basic form" story

**What Tester Does:**

**Developer in standup:** "I finished the leave request form. Ready for testing."

**Tester:** "Great! I'll test it this morning and give you feedback by lunch."

**Morning - Testing:**
- [ ] Tests happy path (valid request submission) ✅ Works
- [ ] Tests empty required fields ❌ No validation, form submits anyway
- [ ] Tests invalid date (end before start) ❌ Allows invalid dates
- [ ] Tests very long text in reason field ✅ Works, truncates at 500 chars

**By lunch - Bug report:**
```
BUG-001: Form submits with empty required fields
Severity: High | Priority: High
Steps: Leave all fields empty, click Submit
Expected: Validation errors shown
Actual: Form submits with empty values
```

**Developer:** "Thanks! I'll fix this today."

**Afternoon - Developer fixes, Tester re-tests:**
- ✅ Validation now works
- ✅ All original tests still pass (regression check)

**Next morning standup:**

**Tester:** "Form story is now fully tested and working. Developer can move to next story."

**Result:**
- ✅ Bugs found early (Day 3, not Day 10)
- ✅ Developer got quick feedback
- ✅ Issues fixed same day
- ✅ Story completed properly

**Why this is good:**
- Tester didn't wait until end of sprint
- Fast feedback loop with developer
- Regression testing after fixes
- Clear communication about quality

### Scenario 3: GDPR Testing

**Context:** Sprint includes "User can export their data" story

**What Tester Does:**

**Test Plan for GDPR Export:**

**Test Scenarios:**
1. User with data requests export → receives file with all their data
2. User with no data requests export → receives empty/minimal file
3. Export includes all required fields (name, email, requests, dates)
4. Export does NOT include other users' data
5. Export file format is readable (JSON/CSV)
6. Export works for users with special characters in data

**Testing:**

**Test 1: User with data**
- Create user account
- Submit 3 leave requests
- Request data export
- Download file
- ✅ Verify: All 3 requests present with correct dates
- ✅ Verify: User's email and name present
- ✅ Verify: File format is valid JSON

**Test 2: Data isolation**
- Create two users (User A, User B)
- User A submits requests
- User B requests export
- ✅ Verify: User B's export contains ONLY their data, not User A's

**Finding:**
❌ User B's export included request IDs from User A (not full data, but IDs leaked)

**Bug Report:**
```
BUG-015: Data export leaks request IDs from other users
Severity: Critical (GDPR violation)
Priority: Urgent

Steps:
1. Create User A, submit request (ID: 123)
2. Create User B, submit request (ID: 124)
3. User B requests data export
4. Open User B's export file

Expected: Only request ID 124
Actual: Export shows "related_requests": [123, 124]

GDPR Impact: User B can see that other requests exist (privacy leak)
```

**Developer:** "Oh! I included 'all requests in same period' by mistake. Fixing now."

**After fix:**
- Re-test all 6 scenarios ✅ All pass
- Mark story as Done from testing perspective

**Result:**
- ✅ Critical GDPR bug caught before production
- ✅ Privacy by design validated
- ✅ Comprehensive GDPR test coverage

**Why this is good:**
- Tester understood GDPR requirements
- Created specific test plan for privacy
- Tested data isolation explicitly
- Caught critical privacy leak

---

## Anti-Patterns (What Goes Wrong)

### Anti-Pattern 1: Testing Only at Sprint End

**What it looks like:**

**Sprint Days 1-8:** Tester waits for "all features to be ready"

**Sprint Day 9 (last day):**

**Tester:** "Okay, starting testing now..."

*[Tests for 3 hours]*

**Tester:** "I found 12 bugs. None of the stories meet Definition of Done."

**Developer:** "But sprint ends tomorrow! We don't have time to fix all this!"

**Scrum Master:** "Why are we discovering this on Day 9?"

**Sprint Review:**
Only 1 of 5 stories is actually Done. Sprint Goal failed.

**Why it's bad:**
- No time to fix bugs before sprint ends
- Developers idle early in sprint, stressed at end
- Quality suffers (pressure to ship broken features)
- Team can't deliver on commitments
- Retrospective is painful

**Symptoms:**
- Most bugs found in last 2 days of sprint
- Developers say "I finished this a week ago"
- Stories rarely meet Definition of Done
- Sprint Reviews show broken features
- Team velocity is unpredictable

**How to fix it:**

**Immediate:**
- **Test incrementally:** As soon as developer says "ready for testing," test it
- **Don't wait:** Even if only one feature is ready on Day 2, test it Day 2
- **Fast feedback:** Report bugs within hours, not days

**Mindset shift:**
- Testing is NOT the final phase
- Testing happens THROUGHOUT the sprint
- Your goal: Help team deliver quality continuously, not judge quality at the end

**Practices:**
- **Daily testing cycle:** Test what's ready each day
- **Set expectation:** "I'll test within 4 hours of you marking it ready"
- **Communicate status:** In standup, say "Story X is tested and done" or "Story Y has 3 bugs"

**Workflow example:**
```
Day 2: Developer finishes Story A → Tester tests → 2 bugs found → Developer fixes → Done
Day 4: Developer finishes Story B → Tester tests → Passes → Done
Day 6: Developer finishes Story C → Tester tests → 1 bug → Developer fixes → Done
Day 8: Full regression test → All good
Day 9-10: Buffer for any issues, refinement for next sprint
```

### Anti-Pattern 2: "Not My Job" Tester

**What it looks like:**

**Refinement session:**

**Developer:** "How should we test this complex workflow?"

**Tester:** "That's not my job. You write the code, I test it."

**Mid-Sprint:**

**Developer:** "Can you help me understand this edge case?"

**Tester:** "I'll test it when you're done. Don't bother me until then."

**Bug found:**

**Tester:** "This is completely broken. How did you even write this?"

**Developer:** "If you'd reviewed the approach earlier, we could have avoided this..."

**Team dynamic:**
- Developers frustrated with tester's attitude
- Tester isolated from team
- Quality suffers because tester only finds issues, doesn't prevent them
- No collaboration, adversarial relationship

**Why it's bad:**
- Testing becomes quality gate, not quality advocacy
- Tester seen as blocker, not helper
- Team doesn't collaborate on quality
- Bugs found late (more expensive to fix)
- Team morale drops

**Symptoms:**
- Tester sits separately, doesn't engage with team
- "Throw it over the wall" mentality
- Tester says "not my problem" frequently
- Developers avoid asking tester questions
- Retrospectives: complaints about tester-developer relationship

**How to fix it:**

**Immediate:**
- **Apologize:** "I've been too hands-off. Let's collaborate better."
- **Offer help:** "How can I help you build this right the first time?"
- **Join discussions:** Actively participate in refinement, planning, design talks

**Mindset shift:**
- **You're part of the team, not separate**
- **Quality is everyone's job** - you're the advocate, not sole owner
- **Preventing bugs > Finding bugs**
- **Collaboration > Separation**

**Practices:**
- **Pair with developers:** "Can I sit with you while you build this? I'll think about test cases."
- **Review designs:** "Let me look at your approach before you code - I'll spot edge cases"
- **Friendly bug reports:** "Found an issue - let's chat about it" not "This is broken"
- **Celebrate quality:** "Great job! This feature had zero bugs" not just criticism

### Anti-Pattern 3: Vague Bug Reports

**What it looks like:**

**Bug Report Example:**

```
Title: Login doesn't work

Description: The login is broken. Fix it.
```

**Developer response:** "What? It works for me. I can't reproduce this."

**Tester:** "Well it doesn't work! Just fix it!"

**Developer:** "Can you give me more details?"

**Tester:** "I already told you - it's broken."

*[3 days of back-and-forth trying to understand the bug]*

**Finally discovered:** Only happens when password has special characters AND user's account was created more than 7 days ago.

**Why it's bad:**
- Developer can't reproduce bug
- Wastes time with back-and-forth
- Bug may not get fixed properly
- Frustration on both sides
- Critical details missing

**Symptoms:**
- Bugs get marked "Cannot Reproduce"
- Developers keep asking for more info
- Bugs take days to fix (should take hours)
- Tester frustrated that bugs don't get fixed
- Developer frustrated by unclear reports

**How to fix it:**

**Use proper bug template (see section above):**

**❌ BAD Bug Report:**
```
Login doesn't work
```

**✅ GOOD Bug Report:**
```
TITLE: Login fails with "Invalid credentials" for users with special characters in password

SEVERITY: High
PRIORITY: High

ENVIRONMENT:
- Browser: Chrome 120.0
- OS: Windows 11
- Test environment

STEPS TO REPRODUCE:
1. Create user with email: test@example.com
2. Set password: "Pass@123!"
3. Wait 8 days (or manually set account creation date to 8 days ago in DB)
4. Navigate to login page
5. Enter email: test@example.com
6. Enter password: Pass@123!
7. Click Login

EXPECTED: User logs in successfully
ACTUAL: Error message "Invalid credentials" shown

ADDITIONAL INFO:
- Happens only with passwords containing @ or !
- Happens only for accounts > 7 days old
- Screenshot attached
- Console shows: "Token validation failed"
- Reproducible 100% of the time with these conditions

WORKAROUND: Create new account (< 7 days) OR change password to remove special chars
```

**Practices:**
- **Always include steps to reproduce** - if you can't write them, you haven't understood the bug
- **Provide evidence:** Screenshots, console logs, network logs
- **Test reproduction:** Before submitting bug, try to reproduce it yourself from your steps
- **Ask yourself:** "If I gave this report to someone else, could they reproduce it?"

### Anti-Pattern 4: "Automaton" Tester (Only Checking Boxes)

**What it looks like:**

**Testing approach:**

**Tester methodically checks each acceptance criterion:**
- [ ] Form has name field ✅
- [ ] Form has email field ✅
- [ ] Form has submit button ✅
- [ ] Submit button is clickable ✅

**All checkboxes passed!**

**Tester marks story as Done.**

**But Tester never tried:**
- What if email is invalid format?
- What if name has 500 characters?
- What if user submits form twice?
- What if network fails during submission?
- What about accessibility (keyboard navigation)?

**Sprint Review - Stakeholder tries to use the feature:**

**Stakeholder:** "I submitted with email 'notanemail' and it accepted it!"

**Team:** "That wasn't in acceptance criteria..."

**Why it's bad:**
- Acceptance criteria are minimum requirements, not complete test coverage
- Misses edge cases and real-world scenarios
- Product has poor quality despite "passing tests"
- User experience suffers
- Bugs found in production or by stakeholders

**Symptoms:**
- All stories pass testing, but quality is poor
- Bugs found by stakeholders in Sprint Review
- Real users find obvious issues
- Tester says "It met the criteria!" defensively
- Team realizes acceptance criteria were incomplete

**How to fix it:**

**Think beyond the checklist:**

**Acceptance Criteria (minimum):**
```
- [ ] User can enter email address
- [ ] User can submit form
- [ ] User receives confirmation
```

**Tester's comprehensive test scenarios:**

**Happy Path:**
- Valid email → submission works → confirmation received ✅

**Validation:**
- Invalid email format (no @) → error shown ❌ BUG FOUND
- Empty email → error shown ✅
- Very long email (500 chars) → error shown ✅

**Edge Cases:**
- Email with special chars (user+tag@example.com) → works ✅
- Email with unicode characters → works or shows clear error ✅

**User Experience:**
- Submit button disabled while sending → prevents double-submit ✅
- Clear error messages → user understands what's wrong ✅
- Keyboard navigation → form usable without mouse ✅

**Integration:**
- Network fails during submit → user gets clear error message ✅
- Server returns 500 error → user sees friendly message ✅

**Mindset shift:**
- **Acceptance criteria = starting point, not finish line**
- **Think like a user:** "How might this break?"
- **Think maliciously:** "How can I break this?"
- **Think creatively:** "What scenarios did we not consider?"

**Practices:**
- **Ask "What if...?"** for every feature
- **Test happy path AND sad path**
- **Try to break things deliberately**
- **Think about real-world usage scenarios**
- **Use exploratory testing** - not just scripted tests

---

## Common Challenges & Solutions

### Challenge 1: "Developers keep marking things 'Done' that aren't Done"

**Example:** Developer marks story Done, but it doesn't meet Definition of Done (no tests written, bugs still present, etc.)

**Solution:**

**1. Reference Definition of Done explicitly:**

**In Standup:**
> "Story X is marked Done, but I see it doesn't have unit tests yet. According to our DoD, we need tests. Can we get those added before calling it Done?"

**2. Use Jira workflow:**
- Developer marks: "Ready for Testing"
- Tester tests and either: "Accept" (Done) or "Reject" (back to In Progress)
- Only Tester can move stories to "Done"

**3. Team agreement:**
- In Retrospective: "Let's agree: Done means it passes DoD, not just coded"
- Make DoD visible (put it on wall, link it in Jira)

### Challenge 2: "I don't have enough time to test everything"

**Reality:** You can't test everything exhaustively. Prioritize.

**Solution - Risk-Based Testing:**

**High Priority (Test thoroughly):**
- Core user flows (login, main features)
- GDPR/privacy features (data export, deletion)
- Features touching personal data
- Integration points between systems
- Features with complex business logic

**Medium Priority (Test main scenarios):**
- Secondary features
- Edge cases for core flows
- UI polish and usability

**Low Priority (Quick smoke test):**
- Cosmetic changes
- Internal tools
- Rarely-used features

**Practices:**
- **Focus on risk:** "What's the worst that could happen if this breaks?"
- **Test critical path first:** Core functionality before nice-to-haves
- **Use automated tests** for repetitive testing (regression)
- **Communicate priorities:** "I'll thoroughly test X, quick test Y, skip Z"

### Challenge 3: "I found a bug, but developer says it's a feature"

**Example:** 

**Tester:** "When user enters an invalid date, the form resets all fields. That's a bug."

**Developer:** "No, that's intentional - we clear the form on any error."

**Tester:** "But users have to re-enter everything! That's terrible UX."

**Developer:** "That's how I built it. Not a bug."

**Solution:**

**1. Check acceptance criteria:**
- If AC says "clear form on error" → Not a bug, but you can suggest UX improvement
- If AC is silent → Clarify with Product Owner

**2. Escalate to Product Owner:**

> "PO, when user enters invalid date, the form clears all fields. Users have to re-enter everything. Is this intended behavior? I think it hurts UX."

**PO decides:**
- "Yes, intended" → Not a bug, accept it (or suggest improvement for later)
- "No, that's not intended" → It's a bug, developer fixes

**3. Distinguish bug vs improvement:**
- **Bug:** Doesn't meet acceptance criteria or DoD
- **Improvement:** Works as specified, but could be better

Log improvements as "Enhancement" not "Bug" - discuss prioritization with PO.

### Challenge 4: "I don't know how to test this technical feature"

**Example:** Story about "Implement caching for API responses" - very technical, unclear how to test from outside.

**Solution:**

**1. Ask developer to explain:**

> "I'm not sure how to test the caching feature. Can you show me how it works and what I should verify?"

**Developer shows:** "When you call /api/requests, first call takes 500ms. Second call takes 10ms. That's caching working."

**Tester:** "Got it! I'll test: 
- First call is slow (cache miss)
- Second call is fast (cache hit)
- After cache expires (5 min), call is slow again
- Cached data matches fresh data"

**2. Pair test with developer:**
- Developer walks through technical implementation
- Tester asks questions, learns, tests together
- Together verify it works

**3. Focus on observable behavior:**
- You don't need to understand code
- You need to verify: Does it do what it's supposed to?
- Use developer tools (browser console, network tab) to observe

---

## Testing Tools & Techniques

### Browser Developer Tools

**Essential for testing:**

**Chrome DevTools (F12):**
- **Console:** See JavaScript errors
- **Network:** See API calls, response times, status codes
- **Application:** Check cookies, localStorage, session data
- **Elements:** Inspect HTML/CSS

**Example usage:**
- Testing API call: Network tab → see if POST /api/requests returns 200 OK
- Testing error handling: Console → see if error is logged clearly
- Testing caching: Network tab → see if second call is from cache

### Screen Recording for Bug Reports

**Tools:**
- Windows: Xbox Game Bar (Win+G)
- Mac: QuickTime Screen Recording
- Browser extension: Loom

**When to use:**
- Bug is hard to describe in words
- Bug involves animation or timing
- Showing sequence of actions
- Demonstrating UX issue

### Test Data Management

**Create reusable test accounts:**

**Examples:**
- `test.employee@example.com` - Standard employee
- `test.manager@example.com` - Manager role
- `test.admin@example.com` - Admin role
- `test.edge.case@example.com` - Account with 100+ requests for testing limits

**Document test data:**
- Keep list of test accounts and their purposes
- Share with team (everyone can use for testing)
- Reset/clean data regularly

### Exploratory Testing

**Not all testing should be scripted. Sometimes just explore:**

**Technique:**
- Pick a feature
- Use it like a real user would
- Try random things
- See what breaks

**Example session (15 minutes):**
- "Let me try to submit 10 requests at once"
- "What if I bookmark this page and come back tomorrow?"
- "What if I resize the window really small?"
- "What if I use browser back button mid-flow?"

**Document findings:** Even if you find no bugs, note "Explored X feature, no issues"

---

## Quick Reference Checklists

### Sprint 0 Checklist

- [ ] Read Product Vision and understand product
- [ ] Review Product Backlog user stories
- [ ] Understand GDPR requirements
- [ ] Set up test environment (VPS access, test accounts)
- [ ] Participate in Definition of Done creation (add testing perspective)
- [ ] Participate in Definition of Ready review
- [ ] Attend backlog refinement - ask "How will we test this?"
- [ ] Create test data for Sprint 1
- [ ] Set up bug tracking approach in Jira

### Sprint Planning Checklist

- [ ] Listen to story discussions
- [ ] Ask "How will we test this?" for complex stories
- [ ] Identify testing dependencies (test data, environments, access)
- [ ] Note edge cases and failure scenarios
- [ ] Ensure testing effort is part of team's estimate
- [ ] Confirm you can access/test stories in sprint

### Daily Testing Checklist

- [ ] Attend Daily Standup - report testing status
- [ ] Check Jira for stories marked "Ready for Testing"
- [ ] Test stories as soon as they're ready (don't wait)
- [ ] Log bugs immediately with clear reproduction steps
- [ ] Re-test fixed bugs within 24 hours
- [ ] Update Jira status (move to Done or back to In Progress)
- [ ] Communicate findings to team (Standup or directly)

### Story Testing Checklist

When testing a story:

- [ ] Read acceptance criteria thoroughly
- [ ] Test happy path (valid inputs, expected flow)
- [ ] Test validation (empty fields, invalid formats)
- [ ] Test edge cases (boundary values, special characters)
- [ ] Test error handling (network failures, server errors)
- [ ] Test integration (does it work with other features?)
- [ ] Check GDPR compliance (if personal data involved)
- [ ] Verify Definition of Done is met
- [ ] Document test results
- [ ] Mark story Done or log bugs

### Sprint Review Checklist

- [ ] Verify all "Done" stories actually meet DoD
- [ ] Run full regression test on integrated increment
- [ ] Prepare quality summary (stories tested, bugs found/fixed)
- [ ] Document known issues not yet fixed
- [ ] Be ready to discuss quality risks
- [ ] Demo any testing tools or techniques used (if relevant)

### Sprint Retrospective Checklist

- [ ] Reflect on what worked well in testing process
- [ ] Identify testing bottlenecks or issues
- [ ] Suggest improvements to testing approach
- [ ] Discuss quality problems and root causes
- [ ] Commit to specific testing improvements next sprint

---

## Tips for Success

### 1. Test Early, Test Often

**Don't wait.** Test incrementally as features are ready.

**Workflow:**
- Developer finishes feature → You test within hours → Give feedback
- Fast feedback = Less rework = Better quality

### 2. Think Like a User AND a Hacker

**As a user:** "How will real people use this? What will confuse them?"

**As a hacker:** "How can I break this? What edge cases did we miss?"

**Both perspectives find different bugs.**

### 3. Communicate Clearly

**Good communication:**
- Bug reports: Clear, specific, reproducible
- Status updates: "Story X is tested and Done" or "Story Y has 2 bugs"
- Risks: "Feature Z is complex, I'll need extra time to test"

**Bad communication:**
- "Something is broken"
- "I'm still testing"
- Silence

### 4. Be Collaborative, Not Adversarial

**You and developers are on the same team.**

**Good tester:**
- "Found an issue, let's fix it together"
- "Great job! This feature had zero bugs"
- "How can I help you test this?"

**Bad tester:**
- "This is completely broken, what were you thinking?"
- "Rejected, fix it"
- "Not my problem"

### 5. Focus on Prevention, Not Just Detection

**Prevention (Best):**
- Ask "How will we test this?" in refinement
- Help developers understand edge cases early
- Review designs before coding

**Detection (Good):**
- Find bugs during sprint
- Fast feedback to developers

**Late detection (Worst):**
- Find bugs in Sprint Review
- Find bugs in production

### 6. Document Your Findings

**Keep track of:**
- Test scenarios executed
- Bugs found and fixed
- Known issues still open
- Test data used

**Why:** Team can learn from your testing approach, replicate tests later.

### 7. Don't Let Perfect Be Enemy of Good

**You can't test everything perfectly.**

**Prioritize:**
- Critical features thoroughly
- Secondary features adequately
- Minor features lightly

**It's okay to say:** "I tested core flows deeply, did smoke test on secondary features."

---

## Getting Help

### When to Ask Developers

- **How to test technical features:** "How does caching work? What should I verify?"
- **How to reproduce bugs:** "I saw this once, but can't reproduce. Any ideas?"
- **Test environment issues:** "API is returning 500 errors. Is test server down?"

### When to Ask Product Owner

- **Unclear requirements:** "Acceptance criteria doesn't specify - should invalid dates clear the form?"
- **Is this a bug or feature:** "Form resets on error. Is this intended?"
- **Priority questions:** "I found 5 bugs. Which should developers fix first?"

### When to Ask Scrum Master

- **Process questions:** "Should I be testing during Sprint Planning?"
- **Team collaboration issues:** "Developers aren't fixing bugs. Can you help?"
- **Workflow questions:** "How should we use Jira for bug tracking?"

### When to Ask Staff

- **GDPR uncertainty:** "Is this personal data? Do we need special handling?"
- **Security concerns:** "I found users can see others' data. How serious is this?"
- **Quality standards:** "What's our acceptable bug threshold?"

---

## Remember

**You are learning.** Nobody expects perfect testing in Sprint 1.

**Good Testers:**
- Test early and often (not just at the end)
- Communicate clearly (bugs, status, risks)
- Collaborate with team (help prevent bugs)
- Think beyond the checklist (edge cases, real usage)
- Focus on high-value testing (risk-based priorities)

**You don't need to:**
- Test every possible scenario (impossible)
- Understand all technical details (focus on behavior)
- Work alone (collaborate with developers)
- Be perfect (continuous improvement)

**Your success = Team delivers high-quality software that works reliably and meets user needs.**

---

**Questions?** Ask your Scrum Master, developers, or fellow testers.

**END OF TESTER/QA ROLE GUIDE**
