# Team Charter: Platform Engineering

## Our Mission

**What we do:**
We build and maintain the foundational platform that product engineering teams depend on to deliver value to customers. This includes deployment infrastructure, observability systems, service frameworks, data pipelines, and the reliability practices that keep everything running.

**Why it matters:**
Every feature the company ships runs on our platform. When we are fast, product teams are fast. When we are reliable, customers trust the product. When we are thoughtful about developer experience, the entire engineering organization operates at a higher level. We are the multiplier — our impact is measured not just by what we build, but by what we enable others to build.

**What would disappear without us:**
Deployments would stall. Incidents would take hours instead of minutes to resolve. Each product squad would reinvent infrastructure independently, inconsistently, and expensively. Scaling to new regions would be a multi-quarter project instead of a configuration change.

---

## Our Values

### 1. Ownership

**What it means:**
We own our systems end-to-end — from design through operation. If something in our domain is broken, we fix it whether or not we caused the breakage. If something is undocumented, we document it when we encounter the gap. Ownership means we do not hand problems to "someone else" when that someone else does not exist.

**How we live it:**
- On-call engineers have full authority to make production changes to resolve incidents
- When we notice something wrong that is not urgent, we file it and put it in the backlog — we don't just complain about it
- Documentation is updated as part of completing work, not as an afterthought
- We proactively monitor our systems and address degradation before it becomes an outage

**What it does not mean:**
- It does not mean working alone. We own as a team.
- It does not mean never asking for help — it means taking responsibility for the outcome regardless of who contributes.

---

### 2. Collaboration Over Heroics

**What it means:**
We succeed together. Sustainable outcomes come from shared understanding and mutual support — not from one person staying up all night to save the day. We help before being asked. We share context generously.

**How we live it:**
- Pair programming encouraged, especially for complex or unfamiliar work
- Knowledge sharing sessions when someone learns something valuable
- Code reviews are collaborative — we ask "what if?" rather than only pointing out errors
- Incident response is team-based. Nobody fights an outage alone.
- We share credit publicly and broadly

**What it does not mean:**
- It does not mean every decision requires consensus. Some decisions are made individually (see Decision Making below).
- It does not mean no one has individual accountability — it means accountability exists within a supportive context.

---

### 3. Continuous Growth

**What it means:**
We invest in getting better — individually and as a team. The skills that got us here are not sufficient for where we are going. Learning is part of the job, not something that happens after hours.

**How we live it:**
- Each person has a current growth area discussed in 1:1s and visible to the team
- We route work that develops specific skills toward people developing those skills
- Stretch assignments are available for those ready to grow into new areas
- Feedback is timely, specific, and actionable — not saved for quarterly reviews
- We celebrate learning from failures as much as learning from successes

---

### 4. Craft and Quality

**What it means:**
We take pride in work that is well-built, well-tested, and well-documented. We do not cut corners that will create pain for future-us or for our users. Quality is not the opposite of speed — it is what enables sustainable speed.

**How we live it:**
- All code reviewed before merge — no exceptions for urgency (hotfixes reviewed post-merge)
- Tests required for new functionality — the test is as important as the implementation
- Runbooks kept current — if you follow a runbook and it is wrong, fixing it is part of the incident resolution
- We refactor proactively during normal work — leave things better than you found them
- We measure and improve our own processes, not just our code

---

## How We Work

### Decision Making

Not every decision deserves the same process. Using a heavyweight process for lightweight decisions creates paralysis. Making heavyweight decisions without input creates alignment debt.

**Decision Framework:**

| Decision Type | Who Decides | Process | Examples |
|---|---|---|---|
| Architectural (broad impact, hard to reverse) | Tech lead + team input | RFC with 3-day comment period | New service boundaries, database technology choices, API contract changes |
| Daily technical (narrow impact, easily reversible) | Individual engineer | Decide, inform team async | Library choice within a service, implementation approach, test strategy |
| Team process (how we work together) | Team consensus | Discussion in team meeting, majority with tech lead tiebreak | Meeting schedules, communication norms, sprint process changes |
| Cross-team (impacts other teams) | Tech lead + stakeholders | Collaborative discussion with affected teams | Shared API changes, platform-wide tooling decisions, deprecations |
| People & hiring | Tech lead + EM | Collaboration with final decision per domain | Role definitions, hiring priorities, team structure |
| Emergency (production incident) | On-call engineer | Act immediately, review afterward | Rollbacks, traffic rerouting, emergency patches |

**Disagreement Resolution:**
1. Attempt to resolve directly between the disagreeing parties — most disagreements dissolve with more shared context
2. If unresolved: bring data, options, and trade-offs to the relevant group (pair, squad, or full team depending on scope)
3. If still unresolved after discussion: tech lead makes the call, documents reasoning
4. Once decided: commit fully. Disagree-and-commit is expected. Revisiting is welcome when new information emerges, not when preference persists.

**RFC Process (for architectural decisions):**
- Author writes RFC with context, options, recommendation
- Posted to team channel with 3 business-day comment period
- Author addresses comments, incorporates feedback
- Tech lead approves or requests revisions
- Decision recorded in Architecture Decision Records (ADRs)

---

### Communication

**Async-First Philosophy:**
Our default is written, asynchronous communication. Meetings are for alignment, relationship-building, and discussion that genuinely benefits from real-time interaction. If a Slack message or document would accomplish the same goal, we prefer that.

**Channels and Usage:**

| Channel | Used For | Not For |
|---|---|---|
| Slack #platform-team | Quick questions, status updates, informal coordination, celebrations | Decisions (use RFC), anything requiring action from offline team members |
| Slack #platform-incidents | Active incident coordination | Post-mortems (use docs) |
| Confluence / Notion | Decisions, designs, knowledge articles, runbooks, RFCs | Ephemeral conversations |
| Email | External stakeholder communication, formal announcements | Internal team coordination |
| Video call | Alignment discussions, 1:1s, pairing, retros | Status updates, information that could be written |

**Response Time Expectations:**

| Channel | Expected Response | Notes |
|---|---|---|
| Incident pages (PagerDuty) | 5 minutes | On-call only |
| Slack urgent (tagged with @team) | 1 hour during work hours | Use sparingly |
| Slack normal | Same business day | Fine to batch-respond |
| Email | Next business day | Exceptions communicated |
| Code review | Within 24 hours | Smaller PRs get faster reviews — incentive for small PRs |

**Communication Norms:**
- If it takes more than 3 Slack messages to resolve, move to a call — then document the outcome
- Thread replies to keep channels scannable
- Use @-mentions intentionally — @channel only for actual team-wide urgency
- Status updates on multi-day work posted in team channel daily (brief, not formal)

---

### Meetings

**Standing Meetings:**

| Meeting | When | Duration | Purpose | Who |
|---|---|---|---|---|
| Daily standup | 9:30 AM | 15 min | Surface blockers, sync on priorities | Full team |
| Sprint planning | Monday AM | 90 min | Commit to next sprint's work | Full team |
| Retrospective | Alternate Fridays | 60 min | Reflect and improve | Full team |
| Tech deep dive | Thursday PM | 60 min | Technical discussion, design reviews, learning | Full team (optional attendance) |
| 1:1 (with TL) | Weekly | 30 min | Growth, feedback, support | Individual + tech lead |
| Architecture review | Monthly | 60 min | Review RFCs, assess technical direction | Tech lead + senior engineers |

**Meeting Norms:**
- Start on time. If you will be late, send a message — do not make 7 people wait silently.
- Every meeting has a stated purpose and expected outcome. If neither exists, cancel it.
- Notes documented within 24 hours and shared — meetings without notes may as well not have happened for absent team members.
- Cameras on when reasonably possible — builds connection, especially for remote members.
- One speaker at a time. If discussion is too lively for that, the facilitator intervenes.
- It is acceptable to decline a meeting and read the notes if your attendance is optional and your focus work is more valuable.

---

## Team Norms

### Code and Quality Standards

- All code reviewed by at least one other engineer before merge
- Tests required for new functionality — PR without tests requires explicit justification
- Documentation updated as part of the change — not a separate follow-up task
- On-call runbooks verified as accurate whenever they are used. If wrong, fix them.
- Linting and formatting automated — no human time spent on style discussions
- No direct commits to main — all changes via pull request

### Work-Life and Sustainability

- Core collaboration hours: 10:00 AM – 4:00 PM (local time). Meetings scheduled within this window.
- Outside core hours, engineers manage their own schedule. No expectation of evening or weekend availability except on-call.
- On-call rotation is fair and sustainable: rotations shared equally, compensated time off after heavy incidents.
- PTO is encouraged and respected. Do not contact someone on vacation unless it is a true emergency with no alternative.
- Sustainable pace is a real priority — if someone consistently works late, that is a team problem to solve (scope, staffing, or process), not an individual badge of honor.

### Feedback Culture

- Feedback is timely — days after the event, not weeks. Waiting for a performance review dilutes impact.
- Assume good intent. If someone did something confusing, ask about the context before assuming negligence.
- Focus on behavior and impact, not character. "When you did X, the impact was Y" — not "You are Z."
- Private criticism, public praise — unless the person explicitly prefers public constructive feedback.
- Feedback is bidirectional. Senior engineers and tech lead actively solicit feedback on their own performance.
- Regular feedback is informal — a quick Slack message or 1:1 comment. It should not feel like an event.

---

## Success Metrics

### Team Health (How We're Doing as Humans)

| Metric | Target | How Measured | Reviewed |
|--------|--------|--------------|----------|
| Team satisfaction score | ≥4.2/5 | Anonymous quarterly pulse survey | Quarterly retro |
| Voluntary attrition | <10% annually | HR data | Quarterly |
| Growth plan progress | Each person advancing on at least one goal | 1:1 check-ins | Monthly |
| On-call burden | ≤1 page per on-call shift (avg) | PagerDuty data | Monthly |
| Innovation time utilization | >80% | Self-reported | Monthly |

### Delivery (How We're Doing on Outcomes)

| Metric | Target | How Measured | Reviewed |
|--------|--------|--------------|----------|
| Sprint commitment met | ≥80% of committed points | Sprint tracking | Every sprint |
| Production incidents (P1/P2) | <2 per month | Incident log | Monthly |
| Deployment success rate | ≥99% | CI/CD pipeline data | Weekly |
| Code review turnaround | <24 hours average | GitHub/Bitbucket metrics | Monthly |
| Documentation coverage | All services have current runbooks | Audit | Quarterly |

### Stakeholder Satisfaction (How Others Experience Us)

| Metric | Target | How Measured | Reviewed |
|--------|--------|--------------|----------|
| Internal developer NPS | ≥50 | Quarterly survey to product teams | Quarterly |
| Platform request response time | <2 business days acknowledgment | Request tracker | Monthly |
| Stakeholder escalations | <1 per quarter | Escalation log | Quarterly |

---

## Growth Paths

### Individual Growth

- **Regular 1:1s** with career-focused agenda items — not just status updates
- **Learning budget:** LKR 500,000/year/person for courses, books, conferences, certifications
- **Conference attendance:** encouraged and supported. Present what you learn back to the team.
- **Internal mobility:** if someone grows beyond what this team can offer, we help them find the right next step — even if it is on another team
- **Stretch assignments:** available and discussed proactively. Growth happens through challenge, not just tenure.

### Team Growth

- **Weekly tech deep dives:** rotating presenters, topics from our domain or adjacent areas
- **Cross-training:** no single point of failure on any system. Pairing and rotation ensure shared knowledge.
- **Mentorship:** senior engineers each mentor one junior/mid engineer. Structured with monthly goal check-ins.
- **External visibility:** blog posts, open-source contributions, and conference submissions are encouraged and count as real work

### Growth Area Visibility

Each team member has a stated current growth area — visible in a shared doc (not public outside the team). This enables:
- Routing relevant work to people developing that skill
- Peer support and pairing on growth areas
- Recognition when growth milestones are hit
- 1:1 conversations anchored in progress, not just problems

---

## Charter Maintenance

**Review cadence:** Quarterly (aligned with team retrospective)

**Owner:** Tech lead, but the team has veto power on any change. This is our shared agreement, not a policy imposed from above.

**Update process:**
1. Any team member can propose a charter change at any time
2. Changes discussed in team meeting (or async if straightforward)
3. Consensus required for value changes; majority for process/norm changes
4. Changes documented with date and reasoning

**How we use this charter:**
- Referenced when friction arises — "let's check what we agreed"
- Shared with new hires in first week — with context and invitation to challenge anything
- Revisited when the team's composition or context changes significantly (e.g., growth from 8 to 15)

**Last updated:** June 2026
**Next review:** September 2026
