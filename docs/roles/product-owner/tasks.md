# Product Owner — Concrete Tasks

## Concrete Tasks

### During Sprint 0 (Preparation Week)

**Your ONLY job this week: Build the Product Backlog**

**Day 1-2:**
- [ ] Read Product Vision thoroughly
- [ ] Receive GDPR requirements from staff/DPO
- [ ] Understand privacy by design principles
- [ ] Make notes on required features

**Day 2-5:**
- [ ] Write 15-20 user stories with acceptance criteria
- [ ] Include GDPR-related stories (data export, anonymization, consent, etc.)
- [ ] Ensure each story has clear value proposition
- [ ] Prepare for team refinement sessions

**Day 3-5:**
- [ ] Facilitate daily refinement sessions with team (30-60 min)
- [ ] Answer team questions about requirements
- [ ] Adjust stories based on technical input
- [ ] Get team feedback on clarity and testability

**Day 4-5:**
- [ ] Facilitate Planning Poker estimation sessions
- [ ] Ensure top 10 stories are estimated **by the team** (you facilitate, they estimate)
- [ ] Prioritize backlog based on value and dependencies
- [ ] Prepare Sprint 1 Planning agenda

**Important:** You facilitate estimation, the **team provides the estimates**. You never estimate story points yourself - this is the team's responsibility based on their technical understanding.

**End of Sprint 0:**
- [ ] Product Backlog has 15-20 ready stories
- [ ] Top 10 stories are estimated and detailed
- [ ] Team understands the product vision
- [ ] **Team has customized Definition of Ready** (based on template)
- [ ] **Team has customized Definition of Done** (based on template)
- [ ] Sprint 1 Planning agenda is ready

**Success criteria:** Team can walk into Sprint 1 Planning and immediately select stories without confusion.

**Note:** Definition of Ready and Definition of Done are created collaboratively during Sprint 0. You provide input on quality expectations and clarity requirements, but the team owns the final version.

### During Each Sprint (Ongoing)

**Beginning of Sprint (Sprint Planning):**
- [ ] Present top priority user stories
- [ ] Explain the value/goal of each story
- [ ] Answer clarifying questions
- [ ] Help team commit to achievable Sprint Goal
- [ ] Ensure Sprint Goal aligns with product vision

**During Sprint (Daily/As Needed):**
- [ ] Be available for questions (within 24 hours response)
- [ ] Clarify acceptance criteria when asked
- [ ] Make decisions on scope/priorities quickly
- [ ] Attend Daily Standup (required in EAP, normally optional but recommended)
- [ ] Review work in progress if team requests
- [ ] **When team says "story is done," verify it meets Definition of Done before accepting**

**Mid-Sprint (Refinement Session - once per sprint):**
- [ ] Facilitate backlog refinement (1-2 hours)
- [ ] Present upcoming stories for next sprint
- [ ] Answer questions, adjust stories based on feedback
- [ ] Ensure next sprint's stories are "Ready"

**End of Sprint (Sprint Review):**
- [ ] Prepare demo script (what to show, what value it delivers)
- [ ] Present completed work to stakeholders
- [ ] Gather feedback from stakeholders
- [ ] Adjust backlog based on feedback

**End of Sprint (Sprint Retrospective):**
- [ ] Participate in team retrospective
- [ ] Listen to team concerns about collaboration
- [ ] Commit to improvements in your role

### Between Sprints

- [ ] Refine backlog (add/remove/update stories)
- [ ] Engage with stakeholders (gather feedback)
- [ ] Prepare for next Sprint Planning
- [ ] Write new user stories if needed

---

## How to Write Good User Stories

### User Story Format

```
As a [type of user]
I want [goal/desire]
So that [benefit/value]

Acceptance Criteria:
- [ ] Specific testable condition 1
- [ ] Specific testable condition 2
- [ ] Specific testable condition 3

GDPR Considerations (if applicable):
- Personal data involved: [specify]
- Legal basis: [consent/contract/legitimate interest]
- Privacy by design: [how is privacy protected]
```

### Example: Good User Story

```
USER STORY: Employee Self-Service Request Creation

As an employee
I want to submit a leave request through a web form
So that I can request time off without sending emails

Acceptance Criteria:
- [ ] Form includes: start date, end date, type of leave (vacation/sick/other)
- [ ] Form validates dates (end date must be after start date)
- [ ] Form shows confirmation message after submission
- [ ] Employee receives email confirmation with request details
- [ ] Request appears in "My Requests" list with status "Pending"

GDPR Considerations:
- Personal data: Employee name, email, leave dates
- Legal basis: Employment contract (necessary for employment)
- Privacy by design: Only employee and approver can see request details
```

### Example: Bad User Story (and Why)

```
❌ BAD:
"The system should have a request form"

Why it's bad:
- Who is the user? (employee? manager? admin?)
- What kind of request?
- What value does it provide?
- No acceptance criteria (how do we know it's done?)
- Not testable
```

```
✅ BETTER:
"As an employee, I want to submit a leave request through a form
so that I can request time off efficiently."

[Then add specific acceptance criteria]
```

### INVEST Criteria Checklist

Good user stories are **INVEST**:

- **I**ndependent: Can be built without depending on other stories
- **N**egotiable: Details can be discussed, not a contract
- **V**aluable: Delivers value to users
- **E**stimable: Team can estimate effort
- **S**mall: Can be completed in one sprint
- **T**estable: Clear acceptance criteria
