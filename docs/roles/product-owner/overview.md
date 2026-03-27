# Product Owner — Role Overview

## Role Overview

### What is a Product Owner?

The Product Owner (PO) is **responsible for maximizing the value of the product** and the work of the Development Team.

**You are NOT:**
- ❌ A project manager telling people what to do
- ❌ A requirements gatherer who just passes messages
- ❌ Someone who writes everything down and disappears

**You ARE:**
- ✅ The voice of the stakeholders and users
- ✅ The decision-maker on what gets built and when
- ✅ The guardian of product value and vision
- ✅ The person who says "yes" or "no" to features

### Core Responsibility

**One sentence:** You decide **what** gets built and **why**, the team decides **how**.

---

## Key Responsibilities

### 1. Product Backlog Management

**You own the Product Backlog.** This means:

**Creating:**
- Write user stories with acceptance criteria
- Ensure stories are clear, testable, and valuable
- Include GDPR requirements where relevant

**Prioritizing:**
- Order the backlog by value/urgency
- Make trade-off decisions (what's more important?)
- Re-prioritize based on changing needs

**Refining:**
- Ensure top stories are ready for Sprint Planning
- Split large stories into smaller ones
- Clarify requirements with the team

**Maintaining:**
- Remove outdated stories
- Update priorities as needed
- Keep backlog organized and visible

### 2. Vision & Value

**You communicate WHY we're building this:**

- Share the Product Vision with the team
- Explain the value of each feature
- Help team understand user needs
- Make decisions that maximize value

### 3. Stakeholder Management

**You are the bridge between stakeholders and team:**

- Gather requirements from stakeholders (staff, DPO for GDPR)
- Communicate progress and decisions
- Manage expectations about what's possible
- Shield team from conflicting demands

### 4. Sprint Participation

**You are actively involved in all Sprint events:**

- **Sprint Planning:** Present and clarify user stories
- **Daily Standup:** Available for questions (optional attendance)
- **Sprint Review:** Present the Increment to stakeholders
- **Sprint Retrospective:** Participate and improve collaboration

### 5. Acceptance & Quality (Using Definition of Done)

**You decide if work is "Done":**

**Two levels of Done:**

**1. Story-level: Acceptance Criteria**
- Review completed work against **story-specific** acceptance criteria
- Example: "Email sent within 5 seconds" → Test this specific requirement

**2. Product-level: Definition of Done**
- Review completed work against **general quality standards**
- Definition of Done = checklist that applies to EVERY story

**Definition of Done (EAP Template - Your team customizes this in Sprint 0):**

Every user story is only "Done" when:

**Code:**
- [ ] Code is readable and reviewed by at least one team member
- [ ] No critical warnings or errors
- [ ] Code follows agreed coding standards

**Testing:**
- [ ] Unit tests are added or updated where relevant
- [ ] Tests pass in CI
- [ ] Test coverage is adequate for the changes made

**DevOps:**
- [ ] Build succeeds
- [ ] Relevant automated tests are executed as part of the pipeline
- [ ] Deployment works in the target environment (if applicable)

**Quality & Resilience:**
- [ ] The application behaves predictably under failure conditions
- [ ] Errors are logged clearly
- [ ] Recovery or rollback is possible

**Documentation:**
- [ ] Changes are documented
- [ ] Setup instructions are updated (if applicable)
- [ ] API documentation is updated (if applicable)

**Architecture:**
- [ ] Architectural impact is documented (if applicable)
- [ ] If significant architectural decisions were made:
  - Architecture Decision Record (ADR) is written
  - ADR is reviewed and accepted by the team
  - Architecture diagrams are updated (if needed)

**Privacy & Data Protection:**
- [ ] Personal data handling is reviewed (if applicable)
- [ ] No sensitive data exposed in logs or error messages
- [ ] Data retention implications are considered
- [ ] Access controls prevent unauthorized data access
- [ ] Privacy by design principles are followed

**Agreement:**
- [ ] The team agrees this work is "Done"
- [ ] **Product Owner has reviewed and accepted the work** (that's you!)
- [ ] Done means ready to show in Sprint Demo and ready to be used by others

**Note:** Not every story requires all checkpoints. For example:
- Small bug fixes may not need architecture documentation
- UI-only changes may not affect API documentation
- Internal refactoring may not need updated setup instructions

Use professional judgment as a team. When in doubt, document.

**Your team creates their final Definition of Done during Sprint 0, based on this template.**

**Your role with Definition of Done:**

**Before Sprint:**
- Help team customize DoD for your product (if needed)
- Ensure DoD is visible and understood

**During Sprint:**
- When team says "Story X is done," check DoD
- If anything is missing: "Not done yet, please complete [missing item]"
- Don't accept "done" until ALL DoD items are checked

**Sprint Review:**
- Only demo work that meets DoD
- Don't show "90% done" work - it's not done

**Why this matters:**
- DoD prevents technical debt (cutting corners)
- Ensures consistent quality
- "Done" means actually shippable, not "mostly done"

**Common mistake:**
- ❌ Accepting work that "mostly works" because sprint is ending
- ✅ Better: Accept only truly Done work, move incomplete work to next sprint

**Note:** Definition of Done is typically created by the team during Sprint 0, with your input on quality expectations.
