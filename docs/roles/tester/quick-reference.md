# Tester/QA — Quick Reference

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
