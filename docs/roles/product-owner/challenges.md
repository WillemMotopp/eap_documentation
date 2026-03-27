# Product Owner — Common Challenges & Solutions

## Common Challenges & Solutions

### Challenge 1: "I don't know the answer to technical questions"

**Example:** Developer asks "Should we use REST or GraphQL for the API?"

**Solution:**
- **This is NOT your decision** - this is a technical/architectural decision
- **Your response:** "That's a technical decision for the team. My requirement is: employees can submit requests via a web form. How you build the API is up to you."
- **Focus on WHAT, not HOW**

**When you DO need to decide:**
- "Should requests be editable after submission?" → **Product decision, you decide**
- "Should we show 10 or 50 requests per page?" → **UX decision, you decide** (or gather user feedback)

### Challenge 2: "Stakeholder wants everything NOW"

**Example:** Staff says "We need all these 20 features by Sprint 3."

**Solution:**
- **Your job: Manage expectations**
- **Response:** "I understand all 20 are valuable. Team velocity is ~18 points/sprint. Over 3 sprints, that's ~54 points total. Let's prioritize the top features that deliver the most value. Which 3-5 features are absolutely critical?"
- **Show the trade-off:** "If we try to build all 20 quickly, quality suffers. If we focus on the top 10, we deliver solid value."

**Then:**
- Prioritize ruthlessly
- Communicate regularly what's possible
- Celebrate delivered value

### Challenge 3: "Team keeps saying stories aren't ready"

**Example:** In Sprint Planning, team says "These stories aren't detailed enough."

**Root cause:** You're not using the Definition of Ready effectively.

**Solution:**

**1. Use Definition of Ready as YOUR checklist:**

Before Sprint Planning, every story in the top of your backlog should meet the team's Definition of Ready.

**EAP Definition of Ready (Template - Your team customizes this in Sprint 0):**

A backlog item is **Ready** when:

**Clarity:**
- [ ] The goal of the item is clear
- [ ] The value for the product or user is understood
- [ ] Acceptance criteria are written and understandable

**Scope:**
- [ ] The item is small enough to be completed within one Sprint
- [ ] Dependencies are identified
- [ ] Open questions are known and discussed

**Feasibility (including DevOps):**
- [ ] The team understands in general how the work can be done
- [ ] Required environments, services, or integrations are known
- [ ] Needed access, secrets, or configuration are identified

**Quality & Testing:**
- [ ] The team knows how the work can be tested
- [ ] Relevant test types are considered (unit tests, integration tests)

**Delivery awareness:**
- [ ] The team understands how this item will be delivered through the pipeline
- [ ] No known blocking issues in CI/CD or deployment exist

**Agreement:**
- [ ] The Product Owner agrees the item is ready (that's you!)
- [ ] **The team has estimated the story** (Planning Poker in refinement)
- [ ] The team agrees the item can be taken into a Sprint

**Your responsibility:** Check this BEFORE Sprint Planning. Don't bring stories that aren't "Ready."

**Note:** Your team creates their final Definition of Ready during Sprint 0, based on this template. You help ensure it's used consistently.

**2. Schedule weekly backlog refinement:**

**When:** Mid-sprint (e.g., Thursday of Week 1 in 2-week sprint)
**Duration:** 1-2 hours
**Attendees:** You + Team

**Agenda:**
- Present 5-8 stories for NEXT sprint
- Team asks clarification questions
- You adjust stories based on feedback
- Team estimates stories (Planning Poker)
- You mark stories as "Ready" when DoR is met

**Result:** By Sprint Planning, top stories are already understood and estimated.

**3. Don't skip refinement:**

**❌ Common mistake:** "We're too busy coding, skip refinement this week."

**Why this fails:** Next Sprint Planning, nothing is ready, Planning takes 3 hours of painful clarification.

**✅ Better:** Protect refinement time. 1-2 hours mid-sprint saves 2+ hours in Planning.

### Challenge 4: "I feel like I'm not doing enough"

**Common feeling:** "I wrote stories in Sprint 0, now what? Team is coding, I'm just... waiting?"

**Reality:** You ARE doing important work:

**During Sprint, you should be:**
- Answering team questions (ongoing)
- Refining upcoming stories (for next sprint)
- Gathering stakeholder feedback
- Monitoring progress toward Sprint Goal
- Preparing Sprint Review
- Thinking about prioritization
- Writing new stories for future sprints

**Time allocation (rough guide):**
- 30% - Team collaboration (questions, refinement, ceremonies)
- 30% - Backlog management (writing, refining, prioritizing)
- 20% - Stakeholder engagement (gathering feedback, reporting)
- 20% - Sprint ceremonies (Planning, Review, Retrospective)

**You are NOT idle.** You are thinking, deciding, prioritizing - this is strategic work.
