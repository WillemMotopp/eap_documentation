# Product Owner — Anti-Patterns (What Goes Wrong)

## Anti-Patterns (What Goes Wrong)

### Anti-Pattern 1: Absent Product Owner

**What it looks like:**

**Week 1:** PO writes user stories.
**Week 2-6:** PO disappears, team never sees them.
**Sprint Planning:** Team asks questions, PO says "I don't remember, let me check" repeatedly.
**Sprint Review:** PO is unprepared, demo is chaotic.

**Why it's bad:**
- Team blocked waiting for decisions
- Stories aren't refined, team guesses at requirements
- No prioritization, team picks randomly
- No value focus, team builds wrong things
- Sprint Reviews are embarrassing

**Symptoms:**
- Team says: "We can't progress, waiting for PO"
- Stories are vague or contradictory
- Team builds features PO didn't want
- Stakeholders frustrated with slow progress

**How to fix it:**

**Immediate:**
- **Set availability hours:** "I'm available on Teams daily 10-12 and 14-16"
- **Attend Daily Standup:** Even just listening helps you stay connected
- **Respond within 24 hours:** To all team questions
- **Schedule weekly refinement:** 1-hour session to review upcoming stories

**Long-term:**
- **Make it a habit:** Block calendar time for PO work (2-3 hours/day)
- **Be proactive:** Ask team "Any questions?" rather than waiting
- **Visible backlog:** Keep Jira updated so team always knows priorities

### Anti-Pattern 2: Requirements Dictator

**What it looks like:**

**Sprint Planning:**

> **PO:** "You MUST build these 5 stories this sprint. No discussion."
>
> **Developer:** "That's 30 points, we only did 18 last sprint—"
>
> **PO:** "Then work harder. These are all critical."
>
> **Scrum Master:** "Maybe we should—"
>
> **PO:** "I'm the PO, I decide what gets built. Just do it."

**Mid-Sprint:**

> **Developer:** "This acceptance criteria is impossible to test. Can we adjust—"
>
> **PO:** "No changes. Build it exactly as written."

**Sprint Review:**

> **PO to team:** "You failed to deliver everything I asked for. This is unacceptable."

**Why it's bad:**
- Team morale collapses
- Collaboration breaks down
- Team stops asking questions (fear of rejection)
- Unrealistic commitments lead to poor quality
- PO seen as antagonist, not partner

**Symptoms:**
- Team is quiet in Planning (no discussion)
- Stories regularly incomplete at Sprint end
- Quality issues increase
- Team-PO relationship is tense
- Retrospectives filled with complaints about PO

**How to fix it:**

**Immediate:**
- **Apologize:** "I've been too demanding. Let's collaborate better."
- **Listen to capacity:** "Team, what's realistic for this sprint?"
- **Be flexible:** "If we can only do 3 stories, which 3 deliver most value?"

**Mindset shift:**
- **You decide WHAT & WHY, team decides HOW & HOW MUCH**
- **Team velocity is reality, not negotiable**
- **Collaboration > Dictation**
- **Team's technical input is valuable**

**Practices:**
- **Ask, don't tell:** "Can we achieve X?" not "You must do X"
- **Prioritize ruthlessly:** "If we can only do 3 of these 5, let's pick the most valuable 3"
- **Respect team capacity:** "Last sprint was 18 points, so let's plan for 15-20"

### Anti-Pattern 3: Vague Storyteller

**What it looks like:**

**User Story Example:**

```
As a user
I want the system to be better
So that it's easier to use

Acceptance Criteria:
- Make it good
- Users should like it
```

**Sprint Planning:**

> **Developer:** "What does 'better' mean specifically?"
>
> **PO:** "You know, just... better. More user-friendly."
>
> **Developer:** "Can you give specific examples?"
>
> **PO:** "Just use your judgment. You're the developers."

**Mid-Sprint:**

> **Developer:** "We built feature X, is this what you wanted?"
>
> **PO:** "Hmm, not really. I meant something different."
>
> **Developer:** "Can you clarify what you want?"
>
> **PO:** "I'll know it when I see it."

**Sprint Review:**

> **PO:** "This isn't what I wanted. It's not user-friendly enough."
>
> **Team:** "You didn't specify what user-friendly means!"

**Why it's bad:**
- Team guesses at requirements
- Rework wastes time and morale
- "Done" is undefined, constant rejection
- Team frustrated by moving goalposts
- No way to estimate vague requirements

**Symptoms:**
- Stories have no acceptance criteria
- Team asks many clarification questions
- Frequent rework ("that's not what I meant")
- PO rejects work but can't explain why
- Team velocity drops (constant changes)

**How to fix it:**

**Immediate:**
- **Write specific acceptance criteria:** Use checkboxes, measurable conditions
- **Use examples:** "E.g., when user enters invalid date, show error message 'End date must be after start date'"
- **Define "user-friendly":** Break it down into specific behaviors

**Example - Before & After:**

**❌ BEFORE (Vague):**
```
Story: Improve request form
Acceptance Criteria:
- Form should be user-friendly
- Make it look professional
```

**✅ AFTER (Specific):**
```
Story: Improve Request Form Validation

As an employee
I want immediate feedback on form errors
So that I can correct mistakes before submitting

Acceptance Criteria:
- [ ] If start date is after end date, show error: "End date must be after start date"
- [ ] If leave type is not selected, show error: "Please select leave type"
- [ ] Error messages appear immediately (< 1 second) when field loses focus
- [ ] Error messages displayed in red text above the relevant field
- [ ] Submit button disabled until all errors are resolved
- [ ] Example: Entering start date "2026-03-15" and end date "2026-03-10" triggers error

GDPR: No additional personal data collected
```

**Practices:**
- **Always include 3-5 specific acceptance criteria**
- **Use examples with actual data**
- **Define "good" with measurable criteria**
- **Ask team: "Is this clear enough to build?"**

### Anti-Pattern 4: Scope Creep Champion

**What it looks like:**

**Sprint Planning:** Team commits to 3 stories (18 points).

**Day 2 of Sprint:**

> **PO:** "I just thought of something! We also need a 'cancel request' button. Can you add that?"
>
> **Team:** "That's a new story, it would add 5 points—"
>
> **PO:** "It's quick, just a button. Please add it."

**Day 5 of Sprint:**

> **PO:** "Can we change the email format? I want it to include the manager's name."
>
> **Developer:** "That wasn't in acceptance criteria, and we're mid-sprint—"
>
> **PO:** "It's a small change, just do it."

**Day 9 (Sprint Review):**

> **Stakeholder:** "Why isn't the cancel button working?"
>
> **Team:** "We didn't finish it, we ran out of time."
>
> **PO:** "But I asked for it early in the sprint!"

**Why it's bad:**
- Original commitment becomes impossible
- Team stress increases, quality drops
- Sprint Goal abandoned
- Velocity unpredictable
- Team stops trusting Sprint Planning

**Symptoms:**
- New requirements added mid-sprint frequently
- Team rarely completes Sprint Goal
- Developers working overtime
- Quality issues increase
- Retrospectives: "PO keeps changing scope"

**How to fix it:**

**Immediate:**
- **Stop adding to sprint:** "Good idea! I'll add it to backlog for next sprint."
- **Respect Sprint commitment:** Current sprint scope is frozen

**When you have new idea mid-sprint:**

**❌ DON'T:**
> "Can you add this now?"

**✅ DO:**
> "I have a new idea: [explain]. This is valuable, but I'll add it to the Product Backlog for Sprint N+1. Let's stay focused on our current Sprint Goal."

**Exception:** Only change scope if:
- **Critical bug** discovered (discuss with team and Scrum Master)
- **Regulatory requirement** emerges (rare, discuss urgency)

**And only if:**
- **Team agrees** they can absorb it
- **Remove equal scope** from sprint to compensate

**Practices:**
- **Keep a "Future Ideas" list:** Note ideas during sprint, review later
- **Protect Sprint Goal:** "Anything not supporting Sprint Goal waits for next sprint"
- **Trust the cadence:** "We have a sprint every 2 weeks, new ideas can wait"
