# Feedback Practice

*Framework used: **SBI + Request** (Situation, Behavior, Impact, Request). Tone target: **Radical Candor** — care personally, challenge directly.*

## Framework reminder

- **Situation:** time/place/context — specific enough to replay the moment.  
- **Behavior:** what you observed (facts), not motive or identity.  
- **Impact:** effect on team, customer, quality, timeline, trust.  
- **Request:** one clear behavior change (or reinforcement for positive feedback).

---

### Feedback 1 — Alex (constructive): facilitation and decision velocity

**Situation:** In last Tuesday’s architecture review for the billing API versioning approach, we had PM and two downstream teams present.

**Behavior:** You walked the group through two strong options, but the discussion circled for 25 minutes without naming decision criteria or proposing a default. When challenged, you defended depth rather than timeboxing the next step.

**Impact:** We ended without a recorded decision, which delayed consumer teams’ planning and pushed risk into implementation week.

**Request:** Next time, can you open with criteria + a 10-minute timebox, then drive to a decision log entry (even if the decision is “spike for 2 days”)? If you want, I’ll sit in the first one and debrief right after.

---

### Feedback 2 — Jordan (positive): growth in code review quality

**Situation:** Yesterday in the code review for the payment service input validation changes.

**Behavior:** You called out a subtle normalization bug and suggested a minimal test that would fail before the fix — the kind of “show your reasoning” review comment that teaches the author.

**Impact:** That likely prevented a correctness issue in production and it signals you’re building senior-level judgment in security-sensitive areas.

**Request:** Would you be willing to share a 5-minute example in our next team meeting of how you approached that review (redacted), so others can copy the pattern?

---

### Feedback 3 — Sam (constructive): stretch and motivation

**Situation:** Over the last two sprints during backlog grooming and assignment.

**Behavior:** You picked up another round of incremental improvements in the legacy admin module — useful work — while the Kubernetes migration workstream still has open tasks nobody has volunteered to own.

**Impact:** Your execution stays high, but the team loses your senior leverage on the riskiest migration problems, and it reads like you’re optimizing for comfort over impact.

**Request:** For next sprint, I want you to take **one** migration slice you’d rate 6–7/10 difficulty — not the whole project — and we’ll scope it together so it’s bounded. Can we pick that candidate tomorrow?

---

### Feedback 4 — Casey (constructive): independence after pairing

**Situation:** This sprint on the notification service change set.

**Behavior:** You paired well with Morgan and asked strong questions, but the commits and PR description read mostly like Morgan’s mental model; you did not yet drive a small end-to-end slice solo.

**Impact:** Pairing is working, but we cannot increase scope until we see you own delivery with your own sequencing and tradeoffs.

**Request:** Next sprint, take one ticket sized “small” where you are the sole assignee; Morgan is available for *timed* checkpoints, not continuous pairing. Let’s choose the ticket in planning.

---

### Feedback 5 — Morgan (positive + stretch): collaboration as leadership

**Situation:** Across the last release cycle (three weeks), especially during the hotfix nights.

**Behavior:** You quietly coordinated handoffs, updated the incident channel clearly, and picked up unglamorous stabilization tasks without being asked.

**Impact:** On-call had less thrash, and newer folks had a calmer example to follow — that is real leadership even without a title.

**Request:** I’d like to recognize this in our retro. Also, would you draft a short “release coordination checklist” we can reuse as a team artifact (one page max)?

---

### Feedback 6 — Riley (difficult): performance + support

**Situation:** Over the past month on the checkout service workstream.

**Behavior:** You missed two sprint commitments, and the merged changes shipped with three P2 defects that required follow-up fixes and extra QA cycles.

**Impact:** The team absorbed rework and timeline risk; stakeholders started asking whether checkout delivery is dependable.

**Request:** I care about you doing well here — before we talk solutions, I want your perspective: what is going on, and what capacity feels realistic for the next two weeks? After that, we’ll agree on a written plan (scope, pairing, checkpoints) so this does not keep sliding.
