# Tester/QA — Common Challenges & Solutions

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
