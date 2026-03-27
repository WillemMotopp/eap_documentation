# Developer — Anti-Patterns (What Goes Wrong)

## Anti-Patterns (What Goes Wrong)

### Anti-Pattern 1: Solo Developer

**What it looks like:**

Developer works alone, makes no progress updates, and marks everything Done in the last two days of the sprint:

**Days 1-8:** All stories stay in "In Progress." Standup updates: "Still working on it."

**Day 9:**

> **Developer:** "I'm done. Marking everything Done."
>
> **Tester:** "I just got all of this to test — an hour before Sprint Review?"
>
> **Scrum Master:** "How are we going to demo untested features?"

**Sprint Review:**

> **Stakeholder:** "The form crashes when I try to submit."
>
> **Developer:** "It worked on my machine..."

**Why it's bad:**
- No time to fix bugs before Sprint Review — untested code is not Done code
- Tester is overwhelmed and cannot do a proper job in one hour
- Team has no visibility into sprint health — no one knows if you are on track or blocked
- Sprint Review becomes a bug showcase instead of a value demonstration

**Symptoms:**
- Stories all move from "In Progress" to "Done" in the last two days of the sprint
- Tester says "I got everything to test yesterday"
- Sprint Review shows bugs that would have been caught in Day 3 if testing had started earlier
- Standup updates never change: "still working on it"

**How to fix it:**

**Immediate:**
- Mark stories "Ready for Testing" as soon as the core flow works — even without all edge cases handled
- Give specific progress updates in standup: "Leave request form is 80% done — should have it ready for testing tomorrow morning"
- Communicate blockers immediately: "I'm stuck on the authentication middleware. I've been stuck since yesterday. Can someone help?"

**Long-term:**
- Break your work into small, testable increments — aim to have something for the Tester every 2 days
- Think of the Tester as your quality partner, not someone who checks your work at the end
- Understand that sprint-end surprises are a team problem, not just your problem

---

### Anti-Pattern 2: Gold-Plater

**What it looks like:**

Story: "Employee can submit a leave request using a form."

Acceptance criteria: start date, end date, leave type, submit button, confirmation message.

Developer's interpretation:

> **Developer (to self):** "I'll build a proper form. Animated transitions, custom date picker, full WCAG 2.1 accessibility, reusable component library, dark mode support..."

**Day 6 of Sprint:**

> **Scrum Master:** "How is the leave request form going?"
>
> **Developer:** "I'm still building the date picker component. It's almost done."
>
> **Scrum Master:** "The acceptance criteria say 'start date and end date inputs.' Did the PO ask for a custom date picker?"
>
> **Developer:** "No, but a native date input looks bad. I wanted to do it right."

**Sprint Review:**

> **PO:** "The form isn't done. We committed to this story."
>
> **Developer:** "The date picker alone took three days. I thought it was important."

**Why it's bad:**
- Sprint commitment was missed — the team cannot rely on your estimates if you regularly add unasked-for scope
- PO's priorities are ignored — they decided what to build, you built something else
- Sprint Goal may be missed because a story the team depended on isn't done
- Future stories that depended on this one are now blocked

**Symptoms:**
- Stories regularly take 2-3x their estimate
- Developer says "I wanted to do it right" or "I was adding value"
- Team regularly misses Sprint Goal
- PO is surprised by what was built

**How to fix it:**

**Immediate:**
- Build exactly what the acceptance criteria say. Nothing more.
- Before adding anything: "Is this in the acceptance criteria?" If no → stop, add a story to the backlog
- Ask the PO if additional scope is genuinely needed before building it: "I could add a custom date picker — is that something you want? It would add 2 days."

**Mindset shift:**
- The acceptance criteria define what Done looks like — they are not a minimum, they are the target
- "Good enough to ship" is a real engineering value — you can always improve later
- New ideas belong in the backlog, not in the current sprint

**When you see a genuinely valuable improvement:**
- Tell the PO: "I noticed we could improve X. It would take Y hours. Should I add a story?"
- Let the PO decide — that's their job

---

### Anti-Pattern 3: "It Works on My Machine" Developer

**What it looks like:**

Developer finishes the leave request endpoint, tests it locally, everything works. Marks story "Ready for Testing."

CI fails:

> **GitHub Actions:** Tests: 3 failed. Build: FAILED.

> **Tester:** "I can't test this — CI is red and the deployment failed."

> **Developer:** "It works perfectly on my machine though. The CI must be broken."

> **DevOps:** "CI is not broken. Your test is importing a module that doesn't exist in the test environment."

> **Developer:** "I'll look at it later — I'm working on a new story."

**Next day:** CI is still red. Two other PRs are blocked waiting to merge.

> **Scrum Master:** "The pipeline has been red for 24 hours. Nobody can deploy."

**Why it's bad:**
- Broken CI blocks the entire team from deploying — one person's broken pipeline stops everyone
- "Done" stories may not actually work in the shared environment — they just work locally
- DevOps and teammates waste time investigating a problem that should have been caught before push
- Trust in the team's ability to ship erodes

**Symptoms:**
- CI is frequently red
- Team can't deploy to the test environment
- Tester can't test because the shared environment is broken
- "It works on my machine" becomes a running team joke

**How to fix it:**

**Before every push:**
- Run the full test suite locally: `pytest` (backend), `npm test` (frontend)
- Check that your code runs with the same environment variables that CI uses — not just your local `.env`
- Never push code you haven't run

**After every push:**
- Check CI status — within 10 minutes of pushing
- If CI breaks: fix it before starting any new work

**General rules:**
- Never merge a PR with failing CI — no exceptions
- Test against the shared test environment, not just localhost
- If you add a new dependency: check that it is in `requirements.txt` or `package.json` — not just installed locally

---

### Anti-Pattern 4: Scope Ignorer

**What it looks like:**

PO defined acceptance criteria for "Employee can submit a leave request":
- Form with start date, end date, leave type
- Validation of dates
- Confirmation message on submission

Developer thinks:

> **Developer (to self):** "I'll also add manager approval while I'm in this code — it's closely related. And email notifications. And a status badge on the list view."

**Day 8:** Developer opens a PR. The PR adds 1,200 lines of code.

> **Reviewer:** "Wait — there's an approval workflow in here. That wasn't in the story."
>
> **Developer:** "I thought it made sense to add it — we'd have to touch this code anyway."

> **PO:** "We have a separate story for approval — and it has different acceptance criteria. Now I don't know what's in the sprint and what isn't."

> **Another Developer:** "My approval workflow story is 80% done. Now yours conflicts with mine."

**Why it's bad:**
- Undisclosed changes hide complexity and make reviews harder
- May conflict with other stories being built simultaneously by teammates
- PO loses control over what is and isn't in the sprint
- The extra work is unestimated — nobody accounted for the time, so estimates are meaningless

**Symptoms:**
- PRs include features not in the story description
- Conflicts with other team members' work during integration
- PR reviews surface surprising additions
- Estimates become meaningless because developers regularly add unplanned scope

**How to fix it:**

**Immediate:**
- Acceptance criteria = scope boundary. Period.
- If you see related work that would be valuable: "PO, I could also implement manager approval while I'm in this code — it would take an extra day. Should I, or do you want it in its own story?"
- Implement only what was agreed. Save everything else for the backlog.

**Practice:**
- Before opening a PR: re-read the acceptance criteria. Does your PR implement all of them? Does it implement anything beyond them?
- If yes to the second question: remove the extra work into a separate branch and create a backlog story
