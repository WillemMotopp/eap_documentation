# Tester/QA — Anti-Patterns (What Goes Wrong)

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
