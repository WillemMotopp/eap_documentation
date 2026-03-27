# Tester/QA — Good Practice Scenarios

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
