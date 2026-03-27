---
Document: EAP_Intern_Onboarding_Guide
Version: 1.4
Status: Approved
Audience: Interns
Approval required: No
Changes from v1.3: Added "Role Boundaries: Who Decides What in UI/UX" section with quick reference table, practical examples, and common pitfalls. Compact version for onboarding with reference to detailed standalone document.
---

# Intern Onboarding Guide – Enterprise Application Project (EAP)

## Purpose of this guide

Welcome to the **Enterprise Application Project (EAP)**.

This guide explains:
- how you are expected to work as a team;
- which roles exist and who holds them;
- how planning and delivery are organised;
- what "quality" means in this project;
- which tools and infrastructure are available.

This guide gives you **context and expectations**.  
Detailed rules, templates, and agreements are provided in separate documents.

---

## The project mindset

This project is set up as a **professional software development project**.

That means:
- you work in a Scrum team;
- you take responsibility for planning, quality, and delivery;
- problems, defects, and operational issues are part of normal work;
- staff support and coach you, but do not take over your roles.

You are expected to act as a **professional team**, not as students following step-by-step instructions.

---

## Team roles and responsibilities

### Product Owner (team role)

One team member acts as the **Product Owner**.

The Product Owner:
- defines and orders the Product Backlog;
- clarifies requirements and acceptance criteria;
- makes scope and priority decisions;
- represents stakeholder interests within the team.

The Product Owner role is held by a **team member**, not by staff.

Staff may act as stakeholders or advisors, but they do **not** make product decisions.

---

### Scrum Master (team role)

One team member acts as the **Scrum Master**.

The Scrum Master:
- facilitates Scrum events;
- ensures Scrum rules and timeboxes are respected;
- helps the team identify and remove impediments;
- supports transparency and collaboration within the team.

The Scrum Master is a **team role**, not a staff role.

Staff members act as **Scrum Coaches**.  
They support and challenge the Scrum Master, but they do **not** run Scrum events or take over the Scrum Master's responsibilities.

---

### DevOps responsibility (team responsibility)

One or more team members take responsibility for **DevOps activities**, such as:
- CI/CD pipelines;
- deployments;
- monitoring and logs;
- operational issues.

DevOps is a **team responsibility**.

You are expected to:
- detect problems early;
- investigate delivery and pipeline failures;
- communicate clearly about operational issues;
- work together on recovery or rollback when needed.

---

### Development responsibility (shared responsibility)

All team members contribute to **building, testing, and improving the product**.

Development work includes:
- writing code (frontend and backend);
- creating and maintaining tests;
- code reviews;
- debugging and fixing defects;
- refactoring and technical improvements.

---

### Shared responsibility

All team members contribute to building, testing, improving, and operating the product.

You share responsibility for:
- achieving the Sprint Goal;
- product quality;
- professional behaviour;
- collaboration and communication.

---

## Role Boundaries: Who Decides What in UI/UX

**Common challenge in Sprint 1-2:** Confusion about who decides how pages should look and function.

This section clarifies decision boundaries between Product Owner and Development Team.

---

### Core Principle: WHAT vs HOW

**Product Owner determines:**
- **WHAT** functionality must exist (features, data, user actions)
- **WHY** we're building it (value, user needs, business goals)
- Business rules and validations
- GDPR requirements

**Development Team determines:**
- **HOW** it looks (design, layout, colors, fonts, components)
- **HOW** it's built (technical implementation, architecture)
- **HOW** it's tested (test strategy, tools)

**Key distinction:**
- PO owns **functional requirements**
- Team owns **implementation decisions**

---

### Quick Reference: Who Decides What

| Decision Type | Who Decides | Example |
|--------------|-------------|---------|
| **Functionality** | | |
| Which fields in a form | Product Owner | "Form needs: start date, end date, leave type" |
| Which actions user can take | Product Owner | "User can submit, view history, cancel request" |
| What data is shown | Product Owner | "Show request status, dates, and approval history" |
| **Validation & Rules** | | |
| Validation rules | Product Owner | "End date must be after start date" |
| Error message content | Product Owner | "Show clear message: 'End date must be after start date'" |
| When validation triggers | Product Owner | "Validate when user clicks Submit" |
| **Design & Layout** | | |
| Where fields are positioned | Frontend Developer | "Start date top-left, end date below it" |
| Colors, fonts, spacing | Frontend Developer | "Blue buttons, 16px font, 20px margins" |
| Which UI components | Frontend Developer | "Material UI date picker for date selection" |
| Responsive breakpoints | Frontend Developer | "Mobile: stack vertically at 768px" |
| **Error Handling** | | |
| Error message styling | Frontend Developer | "Red text, 14px, above relevant field" |
| How errors are displayed | Frontend Developer | "Toast notification vs inline message" |
| **Technical** | | |
| How validation implemented | Backend Developer | "Server-side validation with specific error codes" |
| API design | Backend Developer | "POST /api/leave-requests with JSON payload" |
| Database schema | Backend Developer | "leave_requests table with foreign key to users" |
| **User Experience** | | |
| Is layout logical? | PO provides feedback | "Yes, form is clear" OR "Make submit button more prominent" |
| Are important things visible? | PO provides feedback | "Status should be more prominent" |
| Is flow intuitive? | PO provides feedback | "Add confirmation before canceling request" |

---

### How This Works in Practice

#### Step 1: PO Writes Functional Requirements

**In user story acceptance criteria:**

```
Acceptance Criteria:
- [ ] Form contains: start date, end date, leave type, reason (optional)
- [ ] Validation: end date must be after start date
- [ ] Validation: dates cannot be in the past
- [ ] After submission: show confirmation with request details
- [ ] User receives email confirmation
- [ ] Request appears in user's request history with status
```

**What PO does NOT specify:**
- How form looks (layout, colors, fonts)
- Where fields are positioned
- Which UI components to use
- Exact styling of confirmation message

---

#### Step 2: Frontend Developer Makes Design Decisions

**Developer creates wireframe or prototype:**

```
Example wireframe:
┌─────────────────────────────┐
│ New Leave Request           │
│                             │
│ Start Date:  [Date Picker] │
│ End Date:    [Date Picker] │
│ Type:        [Dropdown]    │
│ Reason:      [Text Area]   │
│                             │
│ [Cancel]     [Submit]      │
└─────────────────────────────┘
```

**Developer decides:**
- Layout: form top, history below
- Components: Material UI date picker
- Colors: blue primary buttons
- Responsive: stack on mobile

---

#### Step 3: Developer Shows to PO for Feedback

**Developer:** "I made a wireframe. Is the layout logical for users?"

**PO reviews and gives UX feedback:**

✅ **Good feedback (functional/UX):**
- "Layout is clear, users will understand it"
- "Can we make the submit button more prominent? It's the primary action"
- "Status should be more visible - that's important for users"

❌ **Bad feedback (design details):**
- "Make button 150px wide instead of 120px"
- "Use #0066CC blue instead of #0077DD"
- "Move field 10px to the left"

**Why bad:** PO is dictating design details. Frontend Developer should make these decisions.

---

#### Step 4: Developer Implements

- Frontend builds based on wireframe + PO feedback
- Backend builds API endpoints
- Tester validates against acceptance criteria

---

### Common Pitfalls & Solutions

#### Pitfall 1: PO Specifies Design Details

**Problem:**
```
❌ PO writes in acceptance criteria:
"Submit button must be 150px wide, blue #0066CC, positioned bottom-right"
```

**Why problematic:**
- PO micromanages design
- Team can't use their expertise
- Wastes PO time on details instead of value

**Solution:**
```
✅ PO writes:
"Submit action must be clearly visible and accessible"

Frontend Developer decides exact styling.
```

---

#### Pitfall 2: Nobody Takes Design Ownership

**Problem:**
```
Developer: "How should this page look?"
PO: "I don't know, you decide"
Developer: "But you're PO, you should know!"
[Deadlock - nobody decides]
```

**Solution:**

**PO clarifies:**
> "I specify WHAT must work, not HOW it looks. Make a wireframe, show me, I'll give feedback on whether it's logical for users."

**Developer:**
> "OK, I'll make a proposal."

---

#### Pitfall 3: Vague Requirements

**Problem:**
```
❌ Story: "User can submit leave request"
Acceptance Criteria: "Form should be user-friendly"
```

**Team:** "What does user-friendly mean?"

**Solution:**
```
✅ PO writes specific functional criteria:
- [ ] Form has fields: start date, end date, type, reason
- [ ] Validation: end date after start date
- [ ] Clear error messages if validation fails
- [ ] Confirmation shown after successful submission

"User-friendly" implementation = Frontend Developer's expertise
```

---

### When in Doubt

**Functional question?** → Ask Product Owner
- "Should users be able to cancel a request?"
- "What happens if validation fails?"
- "Which data should be shown?"

**Design question?** → Frontend Developer decides, shows to PO
- "Should form be one column or two columns?"
- "Which color for the submit button?"
- "Where should error messages appear?"

**Technical question?** → Development Team decides
- "REST or GraphQL?"
- "Which database table structure?"
- "Client-side or server-side validation?"

**Never assume - clarify and document in Jira.**

---

### For Detailed Guidance

This section provides core principles and quick reference.

**For comprehensive guidance including:**
- Complete workflows from story to implementation
- Detailed scenario examples with dialogues
- Anti-pattern deep-dives
- ITNL02 case study (real incident)
- Sprint 2+ implementation checklists

**See separate document:** "Product Owner Role in UI/UX Decisions" (PO_UI_UX_Boundaries_ITNL02_v1.0.md)

**When to read full document:**
- Team experiences confusion about decision boundaries
- Conflicts about "who should decide"
- PO and developers disagree about responsibilities
- Preparing for Sprint 2 after Sprint 1 UI/UX issues

---

## Available tooling and infrastructure

### Source control

**GitHub (private repositories)**
- All code is stored in private GitHub repositories
- Git Flow workflow is mandatory:
  - `main` branch: production-ready code
  - `dev` branch: integration branch
  - `feature/*` branches: individual feature development
- Branch protection rules are active on `main` and `dev`
- Pull requests are required for merging

### Project management

**Jira (paid license)**
- Sprint planning and tracking
- Product Backlog management
- Scrum board for Sprint work
- Access credentials provided by staff

### CI/CD

**GitHub Actions**
- Automated testing on pull requests
- Continuous integration pipeline
- Deployment automation to target environment
- Pipeline configuration is part of your repository

### Deployment platform

**TransIP VPS (Linux)**
- Production-like deployment environment
- Linux-based server
- SSH access for deployment
- Access credentials provided by staff

### Communication

**Microsoft Teams**
- Primary communication tool
- Daily standups (when remote)
- Sprint ceremonies
- Team discussions and decisions

---

## How you plan work

### Definition of Ready

Before work is taken into a Sprint, the team agrees that a backlog item is **Ready**.

This means:
- the goal of the item is clear;
- the value for the product or user is understood;
- acceptance criteria are written and understandable;
- the item is small enough to be completed within one Sprint;
- dependencies and open questions are known;
- technical and DevOps implications are considered;
- architectural impact is identified (if applicable).

The Definition of Ready supports **good Sprint Planning**.

It does **not** remove responsibility from the Product Owner or the team.  
It helps you make better decisions together.

---

## How you deliver work

### Definition of Done

Work is only considered **Done** when the team agrees it meets the Definition of Done.

This includes:
- code that is readable and reviewed;
- automated tests that run as part of the pipeline;
- a successful build;
- deployment in the target environment (if applicable);
- predictable behaviour under failure conditions;
- clear logging and recovery or rollback options;
- updated documentation where needed;
- architectural decisions documented (if applicable).

"Done" means:
- ready to show in a Sprint Demo;
- ready to be used by others.

See the **Definition of Done Template** for the complete checklist.

---

## Architecture and technical decisions

### Architecture documentation

Significant architectural and technical decisions must be documented using **Architecture Decision Records (ADRs)**.

**When to write an ADR:**
- When choosing between multiple viable technical alternatives
- When making decisions that are difficult or expensive to change later
- When deviating from established patterns
- When decisions significantly impact non-functional requirements

**ADR process:**
1. Propose decision in ADR format
2. Discuss with team
3. Review by at least 2 team members
4. Accept and merge when consensus is reached

See the **ADR Template** for the format and structure.

### Architecture governance

Some architectural decisions are **prescribed** by staff and are not negotiable (technology stack, security requirements, infrastructure constraints).

Other architectural decisions are **your responsibility** within those constraints (database schema, API design, component structure, implementation patterns).

Details on which decisions fall into which category will be shared during Sprint 1.

---

## Scrum events

You work in **Sprints of two weeks** and use the Scrum framework.

The Scrum events are:
- Sprint Planning;
- Daily Scrum;
- Sprint Review (Demo);
- Retrospective.

The Scrum Master facilitates these events.  
The Product Owner ensures clarity of goals and priorities.

All team members participate actively.

---

## Professional expectations

In this project:
- problems and defects are normal;
- delivery issues may occur;
- not everything will go as planned.

What matters is **how you respond**:
- investigate calmly;
- communicate clearly;
- respect quality and agreed processes;
- make decisions as a team.

This project focuses on **professional behaviour**, not on avoiding mistakes.

---

## Professional Communication: Feedback Loops and Boundaries

### Closing Feedback Loops (Mandatory)

**What is a Feedback Loop?**

**Scenario:**
1. You report problem: "X is broken"
2. Staff provides solution: "Try Y, let me know"
3. **You MUST close the loop:** "Tested Y, result is Z"

**This is professional communication 101.**

### When Staff Says "Let Me Know"

**This is NOT optional or polite suggestion.**

**Staff means:**
- Test what I gave you
- Report back within 24-48 hours
- Tell me if it works OR doesn't work
- Close the feedback loop

**You MUST respond even if:**
- ✅ It works perfectly → "Tested, it works! Thanks!"
- ✅ It doesn't work → "Tested, doesn't work. Error is: [specific error]"
- ✅ It partially works → "Tested, partially works. Issue is: [describe]"

**Do NOT:**
- ❌ Stay silent
- ❌ Assume staff will follow up
- ❌ Only report if it doesn't work
- ❌ Go build something else without telling staff

### Why Feedback Loops Matter

**Staff's perspective when you go silent:**
- "Problem solved" OR "They're busy with other things"
- Staff does NOT think: "They're building an alternative"

**If you want to try different approach:**

**You MUST ask first:**
```
"Staff, I tested your solution. [Result].
I have an alternative idea: [X].
Can I explore this? It would require [Y]."
```

**Wait for explicit approval before proceeding.**

### Escalation and Follow-up

**When to Escalate to Staff:**
- Infrastructure limitations (VPS constraints, blocked ports, etc.)
- Questions about architecture decisions
- Need for external services or integrations
- Uncertainty about governance boundaries
- Blocking issues preventing Sprint progress
- Any situation requiring financial spending

**How to Escalate Effectively:**

**Good escalation:**
```
"Staff, we encountered [specific problem].
We tried [what we tried].
This is blocking [feature/Sprint Goal] OR we can work on [alternatives].
Urgency: [blocking vs can work around].
Request: [what decision/action you need]."
```

**Poor escalation:**
```
"Something's broken"
"We have a problem"
"Can you look at this?" (with no context)
```

### What to Expect After Escalation

**For non-urgent issues:**

**Staff will:**
1. Acknowledge within 24 hours (work hours)
2. Give you a timeline: "I'll have answer by [time]"
3. Provide updates if it takes longer than expected

**You should:**
1. Wait for staff response
2. Follow up if you don't hear back in 24 hours
3. Continue follow-ups daily if truly blocking and no response
4. Work on non-blocked items while waiting

**For URGENT/BLOCKING issues:**

**Do NOT rely on digital messages (Teams).**

**Escalate personally:**
- Phone call to staff
- Face-to-face conversation  
- Video call if remote

**Explain:**
- Why it's urgent: "This blocks our Sprint Goal"
- What you need: "I need a decision by [time today]"
- What you've tried: "We attempted X, Y, Z"

### What Requires Explicit Approval

**Before you can proceed with:**
- Purchasing anything (domains, services, tools)
- Integrating external services (APIs, platforms)
- Creating accounts that could incur costs
- Making architectural changes
- Changing infrastructure configuration
- Signing up for third-party services

**You need EXPLICIT approval:**
- ✅ "Yes, proceed with X"
- ✅ "Approved, here's the account/budget to use"
- ✅ "Go ahead with that approach"

**NOT approval:**
- ❌ No response yet
- ❌ "Interesting idea" (just acknowledging)
- ❌ "That could work" (not yet deciding)
- ❌ "I mentioned it in standup" (not approval process)
- ❌ Silence after you escalated

**Rule:** If you're not 100% sure it's approved, ask: "Is this approved? Can I proceed?"

### Boundaries and Constraints

**What You Can Decide (Application Decisions):**

Within platform constraints, you have freedom to:
- Choose implementation patterns
- Design database schemas (with GDPR considerations)
- Structure your code and components
- Select specific libraries from approved ecosystems
- Organize your workflow and processes
- Make technical decisions within the approved tech stack

**What Requires Staff Approval (Platform Decisions):**

You must get staff approval before:
- **Purchasing anything** (domains, services, subscriptions)
- **Integrating external services** (APIs, third-party platforms)
- **Changing infrastructure** (VPS configuration, DNS, firewall)
- **Making financial commitments** (even "free" tier services)
- **Adding external dependencies** that involve data processing
- **Changing tech stack** (e.g., React version, database type)

### When You Hit Infrastructure Constraints

**Example: TransIP blocks SMTP for email sending**

**❌ Don't:**
- Buy a domain and use external email service
- Sign up for third-party API without asking
- Work around the constraint independently
- Use personal credit card for project work

**✅ Do:**
1. Document the problem clearly
2. Escalate to staff immediately: "We're blocked by X, what should we do?"
3. Wait for staff to evaluate options
4. Test staff's solution and report back
5. If want alternative: ask permission with risk assessment
6. Implement the approved solution

**Why:**
- Financial accountability (budget control)
- GDPR compliance (data processing agreements needed)
- Security (vendor vetting required)
- Learning opportunity (understand constraints, don't just avoid them)

### The "I'll Pay Myself" Rule

**Never use personal credit cards or accounts for project work.**

Even if:
- "It's only €5"
- "Free tier is enough"
- "I want to help"

**Why:**
- Unclear financial responsibility
- Personal liability for project costs
- No organizational oversight
- Violates procurement policies
- **Will NOT be reimbursed**

**If you think something is needed:** Escalate to staff, justify the need, let staff make financial decisions.

### Escalation is Not Failure

**Asking staff for guidance is professional behavior, not weakness.**

**In corporate IT:**
- Escalating constraints = good judgment
- Making unauthorized purchases = termination risk
- Working around infrastructure without approval = security violation

**We want you to:**
- Take initiative on implementation
- Escalate on platform/infrastructure decisions
- Understand the difference
- Close feedback loops promptly
- Ask permission when uncertain

### "If Staff is Slow" Frustration

**If you feel staff is not responding fast enough:**

1. **Check if you're truly blocked:** Can you work on other features?
2. **Follow up clearly:** Make urgency explicit
3. **Don't assume permission:** Silence ≠ approval
4. **Escalate further:** If staff unresponsive for 48+ hours, escalate to program manager

**Professional patience is a skill.**

In corporate IT:
- Infrastructure changes take days/weeks
- Budget approvals take time
- Vendor evaluations take time
- Legal/GDPR reviews take time

Learning to work around blockers and communicate urgency effectively is valuable.

### Real Example: What NOT to Do

**What Happened (Real Incident):**
- Team needed email functionality
- TransIP blocked SMTP
- Team member escalated to staff
- Staff (1.5h later): "Enabled mail ports, try it and let me know"
- **Team went silent for weeks**
- Team member independently:
  - Purchased domain (~€15)
  - Created Mailgun account
  - Integrated Mailgun API
- Staff discovered weeks later

**Why This Was Problematic:**
- Staff's solution not tested (or feedback not given)
- Alternative implemented without permission
- Money spent without approval
- External service integrated without approval
- GDPR compliance risk created
- Staff's time wasted (thought problem was solved)
- Trust broken

**Consequences:**
- Mailgun integration removed
- Domain purchase NOT reimbursed (team member's loss)
- Assessment impact (professional communication: inadequate)
- Serious warning issued

**What Should Have Happened:**
```
Day 1: Team tests port change
Day 1-2: "Staff, tested port change. [Works/doesn't work, error: X]."

If doesn't work:
"Staff, still blocked. You mentioned DNS config. Can you proceed with that?"

If want alternative:
"Staff, I found Mailgun API. Would require domain purchase (€X) and 
external integration. Can I explore this? What are implications?"

[Wait for staff approval]

[Only then proceed with approved approach]
```

**Critical Lesson:**
- "Try it and let me know" = **mandatory feedback requirement**
- Escalating problem ≠ permission to solve independently
- Going silent = professional communication failure
- **This is a serious violation that impacts your assessment**

### Documenting In-Sprint Clarifications

**Problem:** Clarifications happen during sprint, but if not documented, lead to confusion and rework.

**Scenario:**
```
Day 3 of Sprint:
Developer: "PO, if validation fails, should form fields reset or stay filled?"
PO: "Keep fields filled - better UX, user doesn't retype everything."
Developer: "Thanks!" [starts building]
```

**What goes wrong if NOT documented:**

**Day 5:** Tester tests feature, sees fields stay filled  
**Tester:** "Bug! Fields should reset on error!"  
**Developer:** "PO said to keep them filled..."  
**Tester:** "Where? Not in acceptance criteria!"  
→ Confusion, rework, wasted time

**Next Sprint:** New team member works on related feature, doesn't know about this decision  
→ Builds it wrong, more rework

---

### Who Documents What

#### Product Owner: Owner of Documentation

**Responsibility:**
- Update acceptance criteria in Jira when clarification happens
- Document within 24 hours
- Make clarification visible to entire team

**How to document:**

**Before clarification:**
```
Acceptance Criteria:
- [ ] Form has: start date, end date, type
- [ ] Validation: end date after start date  
- [ ] Show error message if validation fails
```

**After clarification (PO updates Jira):**
```
Acceptance Criteria:
- [ ] Form has: start date, end date, type
- [ ] Validation: end date after start date
- [ ] Show error message if validation fails
- [ ] On validation error: keep form fields filled (user doesn't retype)
- [ ] Error message appears above relevant field in red text
```

**Why in story itself:**
- Single source of truth
- Everyone (dev, tester, future team members) sees it
- Stays accessible after sprint
- Part of Definition of Done verification

---

#### Developer: Triggers Documentation

**Responsibility:**
- Ask clarification from PO
- **Ask PO to document it:** "Can you update the story with this?"
- Or: Give PO exact text to add

**Good pattern:**
```
Developer (Teams): "PO, should form fields reset or stay filled on error?"

PO: "Stay filled - better UX."

Developer: "Perfect! Can you add this to acceptance criteria? 
           So it's clear for tester and anyone working on this later."

PO: "Done - updated in Jira."
```

**Why developer should trigger:**
- PO is busy, might forget to document
- Developer knows which clarifications have impact
- Shared ownership of quality

---

#### Tester: Validates Documentation

**Responsibility:**
- Check acceptance criteria BEFORE testing
- If behavior doesn't match AC → clarify with PO
- Don't assume undocumented behavior is correct

**Good pattern:**
```
Tester reads AC: "On error: keep fields filled"
Tester tests: Fields stay filled ✅
Tester: Matches AC, correct behavior
```

**Bad pattern:**
```
Tester reads AC: [nothing about fields on error]
Tester tests: Fields stay filled
Tester: "Is this right? Don't know, not in AC..."
→ Needs to ask PO (wastes time)
```

---

### Where to Document

**Primary: Jira Story Acceptance Criteria (Source of Truth)**

Update the story itself:
- Everyone sees updates
- Single location
- Survives after sprint
- Part of DoD check

**Secondary: Jira Comments (Optional - For Context)**

For complex clarifications, add comment explaining WHY:

```
Jira Comment (by PO):
@developer @tester

Clarification (19-03-2026):
Q: Reset form fields on validation error?
A: NO - keep fields filled.

Rationale: Better UX, especially for long forms. 
User frustrated if must retype everything for one mistake.

AC updated accordingly.
```

**Why comments useful:**
- Gives context for decision
- Helps future team understand rationale
- Shows conversation history

---

### When PO Not Available

**If PO doesn't respond within 4 hours:**

**Option 1: Developer makes documented assumption**
```
Developer (in Jira comment):
"PO not available. Assuming: keep fields filled on error (better UX).
@PO please confirm or correct."

[Developer builds it]
```

**Option 2: Developer escalates in Daily Scrum**
```
Developer: "Blocker: unclear what error behavior should be.
           PO not reachable yesterday. Need answer today."

SM: "PO, can you answer this after standup?"
```

**Option 3: Developer collaborates with Tester**
```
Developer: "What do you think - keep fields or reset?"
Tester: "Keep them - better UX. Let's build that, 
        PO can reject if wrong."

[Document assumption in Jira]
```

**Critical:** Document the assumption so PO can validate later.

---

### Anti-Patterns: What NOT to Do

#### ❌ "Verbal Agreements Are Enough"

**What happens:**
```
Developer and PO talk in hallway:
PO: "Keep fields filled on error"
Developer: "OK"

[Nothing documented]

Next week:
Tester: "Why are fields filled? Seems like a bug..."
Developer: "PO said..."
PO: "I don't remember that..."
```

**Why bad:**
- Information lost
- Others don't know
- Conflicts over "what was agreed"

**Fix:** Always document in Jira.

---

#### ❌ "Code Comments Are Documentation"

**What happens:**
```javascript
// PO said: keep fields filled on validation error
// Don't reset - better UX
if (validationFailed) {
  // Keep form values
}
```

**Why bad:**
- Tester doesn't see code comments
- PO doesn't see code comments  
- Not in acceptance criteria = not official
- Future non-developers don't know

**Fix:** Code comments are fine, BUT ALSO update Jira AC.

---

#### ❌ "Teams Chat Is Documentation"

**What happens:**
```
Teams chat (Day 3):
Developer: "Question about validation..."
PO: "Keep fields filled"

Sprint Review (Day 10):
Tester: "Where does it say to keep fields?"
Developer: "Teams chat, scroll 200 messages back..."
```

**Why bad:**
- Not durable documentation
- Hard to find (search/scroll)
- Not linked to story
- Chat history has retention limits

**Fix:** Teams for quick question, Jira for documentation.

---

### Team Agreement (Sprint 0 or Retrospective)

**Recommend creating team agreement:**

**In-Sprint Clarifications Protocol:**

1. **Developer:**
   - Get clarification from PO
   - Ask: "Can you update Jira?"
   - If PO unavailable: document assumption in Jira comment

2. **Product Owner:**
   - Update acceptance criteria within 24 hours
   - Tag @team in Jira when AC changed
   - Daily check: "Did I document all clarifications?"

3. **Tester:**
   - Read latest AC before testing
   - If behavior ≠ AC, check if AC is current

4. **Scrum Master:**
   - Daily Scrum: "Any undocumented clarifications?"
   - Sprint Review: Verify all stories have current AC

5. **Tool:**
   - Primary: Jira acceptance criteria
   - Secondary: Jira comments (context)
   - NOT: Teams chat, code comments, verbal only

**Signed by team in Sprint 0**

---

### Golden Rule

> **"If it's not in Jira, it doesn't exist."**
>
> Verbal agreements are not documentation.

---

### Professional Maturity

**Junior behavior:**
- "I have a problem, someone fix it for me"
- Goes silent, does own thing
- Assumes permission when none given
- Bypasses governance when convenient

**Professional behavior:**
- "I have a problem, here's what I tried, what should I do?"
- Tests solutions given by seniors
- Reports results promptly
- Asks permission for alternatives
- Closes feedback loops
- Respects governance boundaries

**We're training you for professional behavior.**

This is as important as your technical skills.

---

## First week checklist

In your first week, ensure you have:
- [ ] Access to GitHub repository
- [ ] Access to Jira project
- [ ] SSH access to TransIP VPS
- [ ] Microsoft Teams access
- [ ] Read the Sprint Guide for Interns
- [ ] Read the Definition of Ready template
- [ ] Read the Definition of Done template
- [ ] Read the Product Vision (including GDPR requirements)
- [ ] Understood your team role (Product Owner, Scrum Master, DevOps lead, or Developer)
- [ ] Participated in first Sprint Planning

**For Product Owner specifically:**
- [ ] Received GDPR requirements from staff/DPO
- [ ] Understand privacy by design principles

---

## Final note

You are trusted with real responsibility.

Use that trust well:
- talk to each other;
- make decisions explicit;
- reflect and improve every Sprint.

Staff are here to **coach and challenge**, not to solve problems for you.

---

**End of Intern Onboarding Guide v1.1**
