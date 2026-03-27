# Developer — Common Challenges & Solutions

## Common Challenges & Solutions

### Challenge 1: "I don't know how to estimate this story"

**Example:** PO presents a story: "Employee receives a push notification when their leave request is approved." You have never implemented push notifications before.

**The problem:**
Giving a confident estimate for something you've never done is guessing. Guessing leads to wrong sprint commitments, missed sprints, and team frustration.

**Solution:**

Say so in refinement — out loud, to the team:

> **Developer:** "I'm not sure how long this takes — I've never implemented browser push notifications. I could spike it: spend a day exploring how it works and what the implementation would look like, then give a proper estimate."

A **spike** is a short (typically 1-2 day) exploration task whose goal is to reduce uncertainty, not to produce shippable code.

- Spikes are legitimate sprint items — add them to the backlog as a task
- After the spike, re-estimate the story with real knowledge
- Never pretend you know when you don't — the team needs honest estimates to plan realistically

**What not to say:**
- ❌ "I'll estimate 3 points" (when you have no idea — this is false confidence)
- ❌ "I'll estimate 13 points to be safe" (padding estimates is dishonest and wastes sprint capacity)
- ✅ "I don't know yet. Can we spike it?"

---

### Challenge 2: "The API spec isn't agreed yet and we're already in the sprint"

**Example:** Sprint 2 starts. Backend and frontend both have stories for the manager approval feature. No one wrote the API spec in Sprint 0. Both developers want to start coding.

**The problem:**
If backend and frontend implement the same feature without an agreed spec, they will make different assumptions. Integration will fail. One or both sides will need to rework their code.

**Solution:**

Stop. Write the spec first — even a rough version — before anyone writes implementation code.

> **Backend Dev:** "Before we start coding, let's write the spec together. It'll take 30 minutes."
>
> **Frontend Dev:** "Agreed. Let's do it now."

In 30 minutes, they write:

```yaml
POST /api/v1/requests/{id}/approve
Request body: { "comment": string (optional) }
Response 200: { "id": integer, "status": "approved", "approved_at": datetime }
Response 403: { "error": "not authorized" }
Response 404: { "error": "request not found" }
```

Both developers review it, agree, and then code independently.

**If one developer is blocked waiting for the other to write the spec:**
- Pair program the spec together — this is exactly the right use of pairing
- 30 minutes of pairing > 2 days of integration debugging

**Rule:** No implementation without an agreed spec. Even a draft spec written in 30 minutes is better than no spec.

---

### Challenge 3: "My code touches personal data — is this a GDPR issue?"

**Example:** Implementing `GET /api/v1/requests/{id}` — returns a leave request including employee name, email, and dates. You are adding a debug log line that includes the response.

**The problem:**
Logging personal data (name, email, leave dates) is a GDPR violation. Personal data in logs can be accessed by anyone with log access — not just the intended recipient of the data.

**Solution:**

Check the GDPR Coding Checklist (see Quick Reference Checklists below) before writing the code.

For the specific log line question:

> **Developer (to self):** "I want to log the full response for debugging. But the response includes employee name and email. That's personal data. I should not log the full response."

Instead, log only non-personal identifiers:

```python
# ✅ GOOD: log IDs, not personal data
logger.info(f"Request {request_id} retrieved for user {user_id}")

# ❌ BAD: log personal data
logger.info(f"Returned request: {response_body}")  # Contains name, email, dates
```

**When in doubt, ask before coding:**

> **Developer:** "PO, this endpoint returns user email addresses in the response. Is that intentional? The frontend is showing them in the request history list."
>
> **PO:** "Good catch — the list view shouldn't show email. Only the detail view should. I'll update the acceptance criteria."

**GDPR Coding Checklist:**
- [ ] No personal data (name, email, dates, IP) in log messages
- [ ] Access control: verify user can only access their own data
- [ ] No sensitive data in error messages returned to the client
- [ ] Data minimization: return only the fields needed, not all fields in the database row
- [ ] If unsure: stop and ask PO or staff before implementing

**Never** assume GDPR compliance is someone else's problem — it is a coding responsibility.

---

### Challenge 4: "My PR has been waiting for review for 2 days"

**Example:** You opened a PR on Monday morning. It's Wednesday afternoon. No one has reviewed it. You can't merge, and you're blocked.

**The problem:**
If the team agreed in the Definition of Done that code review should happen within 24 hours, this is a broken team agreement — not just an inconvenience.

**Solution:**

**Step 1:** Ping the reviewer directly in Teams — do not wait for them to notice:

> "Hey, can you review PR #42 today? I've been waiting since Monday and I'm blocked on the next story."

**Step 2:** If no response by end of day: raise it in standup the next morning:

> "I'm blocked on PR #42 — it's been waiting for review for 2 days. Can someone pick it up today?"

**Step 3:** If the team is consistently slow at reviews: raise it in the Retrospective:

> "PR reviews took an average of 3 days this sprint. Our DoD says 24 hours. Can we talk about how to fix this?"

**Prevention:**
- When you open a PR: immediately ping your reviewer in Teams with the link — do not assume they will notice
- Make PRs small — a 50-line PR gets reviewed faster than a 500-line PR
- Offer to pair review: "I'll review yours if you review mine"

**What not to do:**
- ❌ Merge without review ("I'll ask for review after merge") — this defeats the purpose of code review
- ❌ Wait silently for 3 days before saying anything — you are blocked, say so
