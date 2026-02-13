# PID Background: PRINCE2 Project Board Roles

## Overview

This document explains the three key governance roles on the Project Board for the Enterprise Aanvraagportaal (EAP) project. These roles are part of the PRINCE2 (PRojects IN Controlled Environments) project management framework, which provides the governance structure while the Scrum team handles the day-to-day delivery.

---

## The PRINCE2 Project Board

The Project Board is the **senior management team** responsible for the overall direction and success of the project. It consists of three distinct roles, each representing different stakeholder interests:

```
            Executive
          (Business)
           /      \
          /        \
         /          \
   Senior User    Senior Supplier
   (Customer)      (Technical)
```

These three roles form a **triangle of accountability**, ensuring the project balances:
- **Business value** (Executive)
- **User needs** (Senior User)
- **Technical feasibility** (Senior Supplier)

---

## 1. Executive

### Role Definition
The **Executive** is the single point of accountability for the project. They own the business case and are ultimately responsible for the project's success or failure.

### Key Responsibilities
- **Owns the Business Case**: Ensures the project remains viable and delivers value
- **Budget Authority**: Controls project finances and approves expenditures
- **Ultimate Decision Maker**: Makes final decisions when board members disagree
- **Project Direction**: Sets overall project direction aligned with organizational strategy
- **Chairs Project Board**: Leads Project Board meetings and stage gate reviews

### In the EAP Project
**Role Holder:** Motopp Program Director

**Specific Responsibilities:**
- Ensures project aligns with Motopp's mission to prepare trainees for IT careers
- Approves major scope changes that affect learning objectives
- Ensures project delivers value: trained graduates ready for partner organizations
- Final sign-off on project completion
- Makes go/no-go decisions at stage gates

**Example Decisions:**
- "Should we extend the project timeline if critical learning objectives aren't met?" (No - fixed 12 weeks)
- "Can we increase the cloud budget if needed for better learning outcomes?" (Within limits)
- "Does this project adequately prepare trainees for partner organizations?" (Success criteria)

---

## 2. Senior User

### Role Definition
The **Senior User** represents the interests of those who will **use the final product** or benefit from its outputs. They ensure the project delivers what users actually need.

### Key Responsibilities
- **User Perspective**: Ensures project meets user needs and expectations
- **Requirements Validation**: Validates that requirements accurately reflect user needs
- **Acceptance**: Accepts deliverables on behalf of users
- **User Community Liaison**: Represents the voice of end-users on the Project Board
- **Usability Focus**: Ensures the solution is fit for purpose and user-friendly

### In the EAP Project
**Role Holder:** Simulated Business Stakeholder (Motopp Staff Member)

**Specific Responsibilities:**
- Represents end-users: employees who submit requests, managers who approve them
- Validates business requirements and user stories
- Attends sprint reviews to provide user feedback
- Ensures the application solves real business problems (replacing email/Excel workflows)
- Approves functional design decisions from a user perspective

**Example Decisions:**
- "Is this request submission form intuitive enough for employees?" (Usability)
- "Does the approval workflow match how managers actually work?" (Business fit)
- "Are the notification emails clear and actionable?" (User experience)
- "Should we prioritize mobile responsiveness over admin features?" (User value)

**Why "Simulated"?**
Since this is a training project without real end-users, a Motopp staff member plays this role to provide realistic user feedback and business perspective.

---

## 3. Senior Supplier

### Role Definition
The **Senior Supplier** represents those who will **design, develop, facilitate, procure, and implement** the project's deliverables. They ensure the project is technically sound and deliverable.

### Key Responsibilities
- **Technical Authority**: Ensures project uses appropriate technical approaches and methods
- **Resource Commitment**: Commits technical resources (people, tools, expertise)
- **Quality Assurance**: Ensures deliverables meet technical standards and best practices
- **Feasibility Assessment**: Validates that technical solutions are achievable
- **Supplier Interests**: Protects the interests of those doing the technical work

### In the EAP Project
**Role Holder:** Technical Architect (Motopp CTO or Senior Engineer)

**Specific Responsibilities:**
- Reviews and approves architectural decisions made by trainees
- Ensures technical quality and adherence to best practices
- Provides technical guidance (4 hours per week)
- Validates infrastructure and security approaches
- Ensures chosen technology stack is appropriate for learning objectives
- Protects trainees from making technically unsound decisions

**Example Decisions:**
- "Is the chosen database architecture scalable and appropriate?" (Technical quality)
- "Should we use PaaS or IaaS for this project?" (Architecture decision)
- "Are the security measures adequate for enterprise requirements?" (Technical standards)
- "Is the team's approach to CI/CD pipeline setup sound?" (DevOps practices)

**Balance of Guidance vs. Autonomy:**
The Senior Supplier provides a **safety net** for technical decisions while still allowing trainees to learn through exploration and occasional mistakes. They guide rather than dictate.

---

## How the Three Roles Work Together

### Balanced Decision-Making

The three roles create a system of **checks and balances**:

| Scenario | Executive Concern | Senior User Concern | Senior Supplier Concern |
|----------|-------------------|---------------------|-------------------------|
| Adding a new feature | Does it justify the cost? | Do users need it? | Is it technically feasible in timeframe? |
| Technology choice | What's the budget impact? | Will it meet user needs? | Is it the right technical approach? |
| Quality issue | Can we afford to fix it? | Does it affect usability? | What's the technical severity? |
| Timeline pressure | Business case at risk? | Will users get value? | Are we cutting technical corners? |

### Example: Feature Prioritization Decision

**Situation:** Team wants to add real-time notifications (WebSocket) instead of polling.

**Senior User:** "Users would love real-time updates, but email notifications might be sufficient."

**Senior Supplier:** "WebSocket adds complexity. With 12-week timeline, polling is safer and still good UX."

**Executive:** "What's the learning value? Will partner organizations use this technology?"

**Decision:** Use polling for MVP, document WebSocket as future enhancement. Balances user needs, technical risk, and learning objectives.

---

## Stage Gate Reviews

The Project Board meets at key **stage gates** (every 4 weeks / 2 sprints) to:

1. **Review Progress**: Against plan, budget, and quality standards
2. **Assess Risks**: Review risk register and mitigation effectiveness
3. **Evaluate Deliverables**: Check stage deliverables meet acceptance criteria
4. **Make Go/No-Go Decision**: Approve continuation to next stage or require corrective action

**Each board member brings their perspective:**
- **Executive:** "Are we on budget and delivering business value?"
- **Senior User:** "Are users satisfied with what's being delivered?"
- **Senior Supplier:** "Is the technical quality acceptable?"

All three must agree to proceed to the next stage.

---

## Day-to-Day vs. Strategic Governance

### PRINCE2 Board (Strategic)
- **Frequency:** Stage gates (every 4 weeks) + final presentation
- **Focus:** Strategic decisions, major risks, budget, overall direction
- **Involvement:** Minimal day-to-day involvement, high-level oversight

### Scrum Team (Tactical)
- **Frequency:** Daily (stand-ups, development work)
- **Focus:** Sprint delivery, user stories, technical tasks
- **Involvement:** Full-time work on project deliverables

### Project Manager Bridge
The **Project Manager (Scrum Coach)** bridges these two levels:
- Reports upward to Project Board weekly
- Supports Scrum team daily
- Escalates issues that exceed tolerances
- Ensures PRINCE2 governance doesn't impede Scrum agility

---

## Why This Structure for the EAP Project?

### For Trainees
- **Realistic corporate experience**: Most large organizations have governance structures
- **Clear escalation paths**: Trainees learn when to escalate and to whom
- **Multiple perspectives**: Learn to consider business, user, and technical viewpoints
- **Professional skills**: Practice presenting to senior stakeholders

### For Motopp
- **Risk Management**: Board oversight prevents project failure
- **Quality Assurance**: Technical Architect ensures standards are met
- **Alignment**: Ensures project serves training objectives
- **Accountability**: Clear ownership of business case and outcomes

### For Partner Organizations
- **Confidence**: Structured governance demonstrates professional project management
- **Quality Signal**: Board oversight indicates quality deliverables
- **Transferable Skills**: Trainees learn governance structures they'll encounter in jobs

---

## Key Principles

### 1. Continued Business Justification
**Executive's Focus:** Project must remain viable throughout its life. If business case weakens, project should be stopped.

### 2. Learn from Experience
**All Board Members:** Each stage gate reviews lessons learned and adapts approach.

### 3. Defined Roles and Responsibilities
**Clear Accountability:** Each board member knows their specific responsibilities and authority.

### 4. Manage by Stages
**Stage Gates:** Project divided into manageable stages with go/no-go decisions.

### 5. Manage by Exception
**Tolerances:** Project Manager handles day-to-day within agreed tolerances. Board intervenes only when tolerances are exceeded.

### 6. Focus on Products
**Deliverables:** Board focuses on product quality and delivery, not activities.

### 7. Tailor to Suit Environment
**Pragmatic Application:** PRINCE2 principles adapted for 12-week training project context.

---

## Tolerances and Escalation

The Project Board sets **tolerances** - acceptable deviation ranges that the Project Manager can manage without escalation:

| Aspect | Tolerance | Escalation to Board |
|--------|-----------|---------------------|
| **Time** | Individual sprint can slip by 1 day | Overall 12-week timeline at risk |
| **Cost** | ±10% of €500 budget (±€50) | Budget overrun >10% |
| **Scope** | Adjust "Should Have" features | "Must Have" features at risk |
| **Quality** | Address bugs in next sprint | Critical security or quality issues |
| **Risk** | Manage Low/Medium risks | High or Critical risks emerge |

**When tolerances are exceeded**, the Project Manager escalates to the Project Board for guidance.

---

## Communication Between Board and Team

### Upward Communication (Team → Board)
- **Weekly Status Reports:** Project Manager sends brief written updates
- **Stage Gate Reports:** Comprehensive review every 4 weeks
- **Exception Reports:** Immediate escalation when tolerances exceeded
- **Sprint Review Attendance:** Senior User attends sprint reviews when possible

### Downward Communication (Board → Team)
- **Stage Gate Decisions:** Go/no-go decisions communicated clearly
- **Strategic Direction:** Board provides context for priorities
- **Resource Commitments:** Technical Architect confirms support availability
- **Feedback:** Board provides feedback after sprint reviews and stage gates

---

## Success Scenario: How It Works in Practice

### Week 6 - End of Sprint 3 (Stage 1 Gate Review)

**Preparation:**
- Scrum Master prepares Stage 1 Report
- Metrics gathered: velocity, quality, budget, risks
- Sprint 3 review demo prepared for board

**Stage Gate Meeting:**

**Project Manager (Scrum Coach) Presents:**
- "Sprint 1-3 completed, core workflow functioning"
- "Velocity stable at 35 story points per sprint"
- "Budget at €180 of €500, on track"
- "One risk escalated to HIGH: test coverage at 65%, below 70% target"

**Senior Supplier (Technical Architect):**
- "I've reviewed the architecture - solid foundation"
- "Concerned about test coverage - recommend dedicating Sprint 4 capacity"
- "Security scanning shows no critical vulnerabilities, good"
- "Approve moving to Stage 2 with condition: test coverage must reach 70% by end of Sprint 4"

**Senior User (Simulated Stakeholder):**
- "Request submission and approval workflows are intuitive"
- "Manager feedback is positive on approval interface"
- "Would like to see mobile responsiveness prioritized in Stage 2"
- "Approve Stage 2 continuation"

**Executive (Program Director):**
- "Excellent progress, team is learning well"
- "Budget on track, good cost management"
- "Agree with Technical Architect - test coverage must improve"
- "Approve Stage 2 with conditions: 70% test coverage target, continue monitoring velocity"

**Board Decision:** **GO** to Stage 2 (Sprints 4-5) with action items documented

---

## Common Questions

### Q: What if the board members disagree?
**A:** The Executive has final decision-making authority. However, the goal is consensus through discussion of trade-offs.

### Q: Can board members be involved day-to-day?
**A:** Yes, especially the Senior Supplier (Technical Architect) who provides weekly office hours. However, they must be careful not to undermine the Project Manager's authority.

### Q: What if there's an emergency?
**A:** The Project Manager can make immediate decisions within tolerances. For issues exceeding tolerances, emergency board consultation via email/phone is acceptable.

### Q: Do all three roles need to be different people?
**A:** Ideally yes for checks and balances. However, in small projects, the Executive might also serve as Senior User (not recommended for EAP project).

### Q: Can the Scrum team bypass the board?
**A:** No. Major decisions (technology changes, scope changes, budget increases) must go through the board. The Project Manager is the interface.

---

## Summary

The **PRINCE2 Project Board** provides strategic governance for the EAP project:

| Role | Person | Primary Focus |
|------|--------|---------------|
| **Executive** | Motopp Program Director | Business case, budget, strategic alignment |
| **Senior User** | Simulated Stakeholder | User needs, requirements validation, acceptance |
| **Senior Supplier** | Technical Architect | Technical quality, feasibility, standards |

Together, they ensure the project:
- ✅ Delivers business value (Executive)
- ✅ Meets user needs (Senior User)
- ✅ Is technically sound (Senior Supplier)
- ✅ Provides realistic corporate project experience for trainees
- ✅ Operates within agreed constraints (time, cost, quality, scope)

This governance structure, combined with Scrum delivery, creates a **realistic enterprise project environment** that prepares trainees for their future careers while maintaining quality and accountability.

---

**Document Version:** 1.0  
**Date:** November 20, 2025  
**Related Documents:** Project Initiation Document (PID)
