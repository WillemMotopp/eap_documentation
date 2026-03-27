# Scrum Master — Good Practice Scenarios

## Good Practice Scenarios

### Scenario 1: Effective Impediment Removal

**Context:** Sprint Day 2. In the Daily Standup, a developer says they're blocked waiting for database access on the test server.

**What Scrum Master does:**

**In Standup:**

> **Developer:** "I'm blocked — I need access to the test database to continue. Can't move forward without it."

> **SM:** "Got it. I'll follow up on that after standup. [To DevOps] Do you know who controls that access?"

> **DevOps:** "It requires a VPS config change. I can try, but it might need staff credentials."

> **SM:** "Okay. Developer — can you pick up Story Y in the meantime so you're not idle? I'll escalate the access issue to staff this morning."

**After Standup:**

The SM sends a Teams message to staff: "Developer X is blocked on test database access. DevOps believes staff credentials are needed to grant it. How quickly can we resolve this?"

Staff responds within 2 hours. Access is granted by early afternoon.

**Next day Standup:**

> **SM:** "Database access is resolved. Developer X, you should be able to continue with your original story."

**Result:**
- ✅ Impediment resolved within 24 hours
- ✅ Developer wasn't idle — had alternative work
- ✅ SM didn't try to fix it alone, correctly escalated
- ✅ Team morale maintained

**Why this is good:**
- SM followed up immediately, not "at the next standup"
- Identified root cause (staff credentials needed) instead of hoping DevOps could handle it
- Gave the developer alternative work rather than letting them sit idle
- Resolved within 24 hours — a high-impact day-2 impediment didn't become a week-long blocker

---

### Scenario 2: Facilitating a Difficult Retrospective

**Context:** End of Sprint 2. The team is frustrated. In the retrospective, things get tense.

**What happens without good facilitation:**

> **Developer:** "Testing is always last and we never finish stories on time."
> **Tester:** "That's because developers keep marking things Done when they clearly aren't."
> [Silence. The retrospective stalls.]

**What Scrum Master does:**

> **SM:** "I hear two concerns here, and I think they're related. Let's not assign blame — let's understand the system. Both of you are describing the same problem from different angles."

> **SM:** "I'm going to use sticky notes. Everyone write down one thing that slowed us down this sprint — anonymously. You have 3 minutes."

[Team writes sticky notes, SM groups them on the board]

> **SM:** "I see three themes: 'unclear definition of done for stories', 'testing starts too late', and 'communication gaps between developer and tester'. Let's focus on the first one — that seems to be the root."

> **SM:** "When a developer marks a story 'Ready for Testing', what does that currently mean to you [to Developer]? And what does it mean to you [to Tester]?"

**Developer:** "It means the core feature works."

**Tester:** "I expect all acceptance criteria to pass with no obvious bugs."

> **SM:** "So we have different mental models of 'Ready for Testing'. Can we agree on a shared definition right now?"

**Team agrees:** "Ready for Testing means: acceptance criteria are implemented, developer has tested the happy path manually, and there are no obvious crashes."

> **SM:** "Great. [To Developer and Tester] Can you both own adding that to our Definition of Done by end of day tomorrow?"

**Result:**
- ✅ Blame dissolved into a process improvement
- ✅ Root cause identified (misaligned definitions)
- ✅ Concrete action with owner and deadline
- ✅ Team relationship improved rather than damaged

**Why this is good:**
- SM didn't take sides or minimize concerns
- Anonymous sticky notes lowered defensiveness
- Focused on the system ("two people with different mental models"), not the individuals
- Concrete, actionable outcome — not just "communicate better"

---

### Scenario 3: Protecting the Team from Mid-Sprint Scope Change

**Context:** Sprint Day 6 of 10. The team committed to 3 stories and is on track. A stakeholder messages the SM directly:

> **Stakeholder:** "We just realized we need a 'cancel request' button for the demo next week. Can the team add it to this sprint? It shouldn't take long."

**What a bad SM does:**
Adds the story to the sprint without discussion. Team is surprised in standup. Sprint Goal shifts. Two original stories don't get done.

**What a good SM does:**

> **SM (to stakeholder):** "I understand — that sounds important for the demo. Adding it now would put our current Sprint Goal at risk, though. Let me loop in the PO so we can make an informed decision together."

> **SM (to PO):** "The stakeholder wants to add a 'cancel request' story to this sprint for the demo. Can you evaluate the priority? If we add it, what do we remove to protect the team's capacity?"

**PO evaluates:**
- Option 1: "The demo is Sprint Review — it's in 4 days. Let's add the cancel story but de-scope Story 3 (it's lower priority anyway)."
- Option 2: "The sprint is too full. Let's get the cancel story into Sprint 3 instead — it's first in the backlog."

**PO and SM communicate decision back to stakeholder:**

> **PO:** "We can add the cancel button if we defer Story 3, OR we can keep the current scope and have it ready for Sprint 3. Which do you prefer?"

**Stakeholder:** "Let's keep the current scope and defer it."

**Result:**
- ✅ Sprint commitment protected
- ✅ Stakeholder heard and given a choice
- ✅ PO (the right decision-maker) was involved
- ✅ Team was not surprised or disrupted

**Why this is good:**
- SM was the buffer between external pressure and the team
- Didn't make the scope decision alone (that's the PO's role)
- Gave the stakeholder agency through a clear choice
- Kept the team focused on their Sprint Goal
