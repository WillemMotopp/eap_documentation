# Product Owner — Good Practice Scenarios

## Good Practice Scenarios

### Scenario 1: Effective Sprint Planning

**Context:** Sprint 1 Planning, team is ready to select stories.

**What PO Does:**

**Before the meeting:**
- Reviews top 10 stories in backlog
- Ensures all have acceptance criteria
- Prepares to explain value of each story

**During Sprint Planning:**

> **PO:** "Our Sprint Goal is to enable employees to submit basic leave requests. I've prioritized three stories for this sprint:
>
> **Story 1:** Employee can create leave request
> **Value:** This is the core feature employees need most.
> **Team's estimate:** 8 points
>
> **Story 2:** Employee can view their request history
> **Value:** Employees need to track what they've requested.
> **Team's estimate:** 5 points
>
> **Story 3:** Request validation (start/end dates)
> **Value:** Prevents invalid requests, reduces manual checking.
> **Team's estimate:** 3 points
>
> Total: 16 points. In Sprint 0, the team estimated your velocity at 15-20 points per sprint, so this seems achievable.
>
> **Question for team:** Can we commit to these three stories? Any concerns?"

**Team:** "Story 1 seems large. Can we split it?"

**PO:** "Good point. Let's split it:
- Story 1A: Basic form (name, dates, type)
- Story 1B: Email confirmation

Team, can you estimate these two pieces?"

**Team:** "[Brief Planning Poker] 1A is 5 points, 1B is 3 points."

**PO:** "Perfect, that gives us more flexibility. So our sprint is: 1A (5), 1B (3), Story 2 (5), Story 3 (3) = 16 points total. Team, can we commit?"

**Team:** "Yes, we commit to this scope."

**Result:**
- ✅ Clear Sprint Goal
- ✅ Stories prioritized by value
- ✅ Team involved in scope decision
- ✅ Realistic commitment
- ✅ Flexibility to adapt

### Scenario 2: Handling Mid-Sprint Clarification

**Context:** Day 3 of sprint, developer has question about acceptance criteria.

**Developer:** "Story says 'employee receives email confirmation.' Should this be immediate or can it be queued?"

**❌ BAD PO Response:**
> "I don't know, what do you think?"

**Why it's bad:** PO abdicated decision-making. This is YOUR decision.

**✅ GOOD PO Response:**
> "Good question. Immediate is better for user experience - they should see confirmation right away. Queue it only if technical constraints require it. What's the impact?"

**Developer:** "Immediate is doable, just wanted to confirm."

**PO:** "Perfect, let's go with immediate. I'll update the acceptance criteria to be explicit: 'Email sent within 5 seconds of submission.'"

**Why it's good:**
- PO made decision based on user value
- Asked for technical input
- Updated story for clarity
- Quick response (same day)

### Scenario 3: Sprint Review with Stakeholder Feedback

**Context:** End of Sprint 1, presenting to staff stakeholders.

**PO presents demo:**

> **PO:** "In Sprint 1, we achieved our goal: employees can now submit leave requests.
>
> **Demo:** [Shows form, submission, confirmation, request list]
>
> **Value delivered:** Employees no longer need to send email requests. The form validates dates automatically, reducing errors.
>
> **Next sprint:** We'll add the approval workflow so managers can approve/reject requests."

**Stakeholder:** "This looks good, but I notice there's no field for 'reason for leave.' We need that for HR reporting."

**❌ BAD PO Response:**
> "Oh, the team didn't build that. We can add it next sprint."

**Why it's bad:** Sounds like PO didn't know this was needed. Implies poor requirements gathering.

**✅ GOOD PO Response:**
> "Good point. I didn't include that in this sprint because I prioritized getting the basic flow working first. Adding a 'reason' field is definitely valuable for HR reporting. I'll add that story to the backlog and we can prioritize it for Sprint 2 or 3. Should this be required or optional?"

**Stakeholder:** "Optional is fine."

**PO:** "Perfect, I'll write that story this week. [Takes notes]"

**Why it's good:**
- Acknowledged the feedback professionally
- Explained prioritization decision
- Committed to action (backlog story)
- Asked clarifying question (required/optional)
- Documented it immediately
