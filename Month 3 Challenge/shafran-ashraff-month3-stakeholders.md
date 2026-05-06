# Stakeholder Communication Plan: Microservices Migration

*Principle: never escalate without a recommendation; never let stakeholders be surprised; never share buffer details externally.*

---

## Stakeholder Map

| Stakeholder            | Interest | Influence | What they actually need from me                                              |
|------------------------|----------|-----------|------------------------------------------------------------------------------|
| VP Engineering         | High     | High      | Confidence, risks they can act on, decisions they need to make               |
| Product Director       | High     | Medium    | Timeline reality, feature trade-offs, when their roadmap unblocks            |
| CTO                    | Medium   | High      | Strategic alignment, architectural posture, executive-level milestones       |
| Engineering Manager    | High     | Medium    | People issues, capacity reality, performance / pairing decisions             |
| Support Manager        | Medium   | Low       | Training plan, launch readiness, what changes for end-users                  |
| Finance Partner        | Low      | Medium    | Budget tracking, contractor approval, cost vs. plan                          |
| QA Lead                | High     | Low       | Test environment access, contract test gates, release windows                |
| Compliance / Security  | Medium   | High      | Pen test booking, PCI scope, security review sign-off                        |
| Internal stakeholders (other product squads) | Medium | Low | When their integrations need to update, contract changes, deprecation timelines |

**Plot logic:** Manage closely (high/high) — VP Eng, CTO. Keep satisfied (low/high) — Compliance. Keep informed (high/low) — QA, internal squads, Support. Monitor (low/low) — Finance for routine budget; surface only when ask is needed.

---

## Communication Matrix

| Audience               | Format                          | Frequency       | Content                                              | Owner       |
|------------------------|---------------------------------|-----------------|------------------------------------------------------|-------------|
| VP Engineering         | 1:1, Teams                       | Weekly (30 min) | RAG status, top 3 risks, decisions needed            | Tech Lead   |
| Product Director       | Status email + bi-weekly sync    | Weekly (email), bi-weekly (30 min) | Progress vs. plan, blockers, scope trades | Tech Lead   |
| CTO                    | Executive summary email          | Monthly         | Strategic milestones, architectural deltas           | Tech Lead   |
| Engineering Manager    | 1:1 + sprint review              | Weekly + at review | People + capacity, performance signals             | Tech Lead   |
| Support Manager        | Pre-launch readiness review      | Per phase       | Training plan, runbooks, change impact               | Tech Lead   |
| Finance Partner        | Email update                     | Monthly         | Budget burn, contractor utilisation                  | EM          |
| QA Lead                | Slack channel + planning attend  | Per sprint      | Env schedule, contract test status, release windows  | Senior 1    |
| Compliance / Security  | Booking + review meeting         | At Phase 1 / Phase 3 gates | Security plan, pen test, PCI sign-off       | Tech Lead   |
| Internal squads        | Newsletter (Confluence + email)  | Bi-weekly       | Contract changes, deprecation dates, integration help| Tech Lead   |
| Whole team             | Stand-up                         | Daily (15 min)  | Tasks, blockers, dependencies                        | Tech Lead   |
| Whole team             | Retro                            | End of sprint   | What worked / what didn’t / one experiment           | Tech Lead   |

**Rules I hold myself to**

1. Lead with what they need to know, not what we did.
2. Never escalate without at least 2 options + a recommendation.
3. RAG status doesn’t skip Amber. If we go from Green to Red, I have failed at communication.
4. Buffer is internal information only.

---

## RACI for Key Decisions

| Decision                                       | R                | A             | C                                | I                       |
|------------------------------------------------|------------------|---------------|----------------------------------|-------------------------|
| Architecture / saga pattern choice             | Tech Lead        | Tech Lead     | Senior engineers, CTO            | EM, Product             |
| Per-service cutover go/no-go                   | Tech Lead        | Tech Lead     | Service owner, QA, Support       | VP Eng                  |
| Scope change request from Product              | Product Director | Product Director | Tech Lead, EM                | Team, VP Eng            |
| Hire contractor (Option 1)                     | EM               | VP Eng        | Tech Lead, Finance               | Team                    |
| Defer service to next phase / next year        | Product Director | VP Eng        | Tech Lead, EM                    | CTO, Team, internal squads |
| Production change during BF freeze (P1 only)   | Tech Lead        | VP Eng        | EM, Support                      | CTO                     |
| Performance budget per service                 | Tech Lead        | Tech Lead     | Senior engineers                 | EM                      |
| PCI scope and security sign-off                | Tech Lead        | Compliance    | Senior 1, Senior 2               | EM, VP Eng              |
| Roll back a cutover                            | Tech Lead        | Tech Lead     | Senior owner, Support            | VP Eng (immediate notify) |
| Postmortem ownership for any Sev-1             | Tech Lead        | EM            | Senior involved, SRE             | VP Eng, CTO             |

**Hard rule:** exactly one Accountable per row. If two people think they’re A, nobody is. I check this every time we add a row.

---

## Status Report Template — Weekly

> Sent every Monday by 10:00. To: VP Eng + Product Director. CC: EM, CTO (monthly compilation).

```
Subject: [Migration] Weekly Status — Week of {date} — {Green/Amber/Red}

Overall status: 🟢 Green / 🟡 Amber / 🔴 Red

Summary (3 bullets max):
- {progress headline}
- {risk headline}
- {decision needed headline, or “none this week”}

Progress this week
- ✅ Completed: {3–5 items, outcome-shaped, not task-shaped}
- 🔄 In progress: {2–3 items}
- ⏳ Planned next week: {2–3 items}

Key metrics
| Metric                         | Target  | Actual  | Trend |
|--------------------------------|---------|---------|-------|
| Velocity (3-sprint avg)        | 25 pts  | {x}     | ↑/→/↓ |
| Services in production         | {n}     | {n}     | →     |
| Reconciliation drift           | <0.05%  | {x}     | →     |
| Buffer consumed (% of project) | ≤ % time elapsed | {x}% | → |
| Open Sev-1 / Sev-2             | 0       | {n}     | →     |

Risks & issues (top 3 only)
| ID | Title | Status | Action / who | When |
|----|-------|--------|--------------|------|
| R1 | … | active mitigation | TL | this sprint |

Decisions needed
- [ ] {decision, owner, deadline}

Next week focus
- {priority 1}
- {priority 2}
```

**Why these rules**

- Three-bullet summary because executives don’t scroll.
- Buffer-vs-elapsed metric because that single line tells you whether the plan is healthy without exposing the buffer number itself.
- “Decisions needed” always present — even when empty — because that train of attention is what I want VP Eng to associate with this report.

---

## Status Report Template — Sprint Report (bi-weekly)

> Sent at end of every sprint. To: Product Director, EM, internal squads. Built from Azure DevOps dashboards — set up once, refreshed automatically.

```
Subject: [Migration] Sprint {n} Report — {Green/Amber/Red}

Sprint goal: {one sentence}
Outcome: {achieved / partially achieved / missed} — one sentence why.

Velocity vs. plan
- Committed: {x} pts | Delivered: {y} pts | Carryover: {z} pts
- 3-sprint trailing average: {n} pts

Burndown trajectory
- {chart link / screenshot}
- {one sentence read of the shape}

Scope changes this sprint
- Added: {x pts} — {reason}
- Removed: {y pts} — {reason}
- Net: {±n pts}

Completed
- {feature/service} — {outcome, link}
- …

Carryover (what slipped, why, when it lands)
- {item} — {reason} — {sprint it lands in}

Notable risks updated
- {R-id}: {state change}

Next sprint goal
- {one sentence}

Dashboard: {Azure DevOps link}
```

---

## Executive Summary Template — Monthly (CTO)

> One page, three sections. Strategy first, then progress, then risk.

```
Subject: [Migration] {Month} — {Green/Amber/Red}

Where we are strategically
- {1–2 sentences: are we on the path the migration was set up for? What changed in posture?}

Milestones this month
- {phase progress + biggest milestone hit}
- {biggest milestone next month}

Top risks (max 3)
- {R1 title} — current score {n}, trend ↑/→/↓, action {…}

Decisions / asks
- {one ask, or “none this month”}
```

---

## Escalation Framework

| Level                | Triggers                                                                 | Timeline      | Owner                | Format                                |
|----------------------|--------------------------------------------------------------------------|---------------|----------------------|---------------------------------------|
| **Level 1 — Team**   | Routine blockers, single-engineer-day issues, ambiguous tickets          | 1–2 days      | Tech Lead            | Stand-up, async Slack thread          |
| **Level 2 — Management** | Resource conflicts, sprint slip likely, cross-team dependency issue, scope change > 20 pts | 1 week | Engineering Manager + Tech Lead | Sync (30 min), follow-up email |
| **Level 3 — Executive** | Timeline at risk, budget impact, security incident, BF freeze conflict materialising, any Critical risk activating | Immediate (same day) | VP Engineering | Urgent Teams + email, 30-min meeting same day |

**Trigger rules I commit to**

- Status moves Green → Amber: raise in next scheduled meeting (max 2 working days), with a mitigation plan attached.
- Status moves Amber → Red: immediate notification (same day), email + Teams ping, recommendation included.
- “We have a problem.” is not an escalation. “We have {problem}; my recommendation is {A or B}; I need a decision by {date}.” is.

---

## Communication Scenarios

### Scenario A — Milestone at risk (Amber)

> *Audience:* VP Eng + Product Director
> *Format:* 30-min meeting, same week. Email pre-read sent 24h before.
> *Tone:* facts > emotion; recommendation > complaint.

**Pre-read (email)**

```
Subject: [Migration] Heads-up on M2.5 (Order cutover) — Amber

Status: Amber. Cutover for M2.5 on track for week 16; latest indicators
suggest 1–2 sprint slip if we don’t intervene.

What changed
- Saga compensation rate trending at 1.2% (target <0.5%) over last 4 days.
- Two senior engineers consumed by ad-hoc reconciliation incidents on User
  service for ~30% of the week.

Why this matters
- Order is on the critical path; slipping 2 sprints pushes the Payment
  start date and tightens the BF freeze margin.

Options (full trade-offs in deck, link)
1. Add a contractor (Option 1 from capacity plan) — restores margin,
   $50K, decision needed this sprint.
2. Defer Search to next year — frees ~3 sprints of capacity for the
   critical path, no revenue impact for Q4.
3. Accept slip and shorten Phase 4 hardening by 1 sprint — lowers
   confidence on cutover stability; not recommended for 99.9% target.

My recommendation
- Option 2 — defer Search. Lowest cost, no contractor onboarding tax,
  protects the freeze margin. I’d like to confirm in our Wednesday sync
  so I can re-plan Sprint 7.

Asking you for
- A decision by EOD Wed.
- Product Director sign-off on Search deferral if we go with Option 2.
```

**In the meeting (30 min)**

1. Situation — facts only (3 min).
2. Root cause analysis — what we know vs. what we’re still investigating (5 min).
3. Options + trade-offs (10 min).
4. Recommendation (5 min).
5. Decision + owner of next step (5 min).
6. Two minutes for the question I’m most likely getting wrong.

### Scenario B — Critical risk activating (Red)

> Example trigger: data inconsistency detected on a live service (R1 materialising).

**Within 1 hour**

- Halt cutover; route 100% to monolith; freeze deploys for the affected service.
- Open incident channel; notify on-call.

**Within 4 hours**

- Send VP Eng + CTO a structured update:

```
Subject: [Migration] RED — Order Service data drift detected

What happened
- {timestamp}: reconciliation drift {x}% on order_payments table.

What we did
- Cutover halted; all traffic on monolith; freeze deploys for Order.
- Reconciliation job running; backfill plan being prepared.

Customer impact (current best estimate)
- {n} orders affected; no payments lost (verified by reconciliation).
- Support team briefed; comms template ready if needed.

What we need
- VP Eng: cover for Product comms today.
- CTO: aware, no action needed yet.

Next update: {time, max 4h from now}.
```

**Tone:** flat, factual, no hedging language. The job in a Red is to lower the room’s temperature, not raise it.

### Scenario C — Major success (Phase exit signed)

> Audience: All stakeholders + team. Format: short email + team celebration.

```
Subject: [Migration] Phase 2 complete — three core services live

We just closed Phase 2 of the migration: User, Product, and Order
services are all live in production at 100% traffic.

What this enables
- The biggest single technical risk on the project (R3 — distributed
  transactions) is now mitigated against real traffic.
- Product can begin scoping the {next quarter} roadmap items that depend
  on the new Order API.

Team
- Senior 1 led the Order saga design and lived the cutover; this was the
  hardest slice on the project and it landed clean.
- Mid 1 took ownership of Helm templating mid-Phase 1 and now runs the
  golden pipeline for the team — that’s a step up.

Next up
- Phase 3 starts {date}: Payment, Notification, Inventory, Search.
- Risk register refreshed (link), top focus is R2 (BF freeze).

Thank you to everyone who attended planning, supported integrations,
and made the cutover boring.
```

**Why I write success notes the same way I write incident notes:** same audience, same trust account. Don’t hide good news; don’t over-celebrate either.

### Scenario D — Scope-change pressure mid-phase

> Trigger: Product asks for a “small extra” feature that doesn’t fit. The lecture called this the “yes-and” negotiation.

**Verbatim line I use:**

> “We can absolutely do that. To fit it in this sprint without slipping
> M2.3, we need to swap out {X} or move {Y} to next sprint. Which works
> for you, or do you want to take it back to the Product Director?”

**Why this works**

- Never just absorb (the “yes machine” anti-pattern).
- Never just refuse (kills trust).
- Always trade — every yes is paired with a no, written down.

---

## Templates I keep at the top of the project Confluence

1. **Weekly status email** (above)
2. **Sprint report** (above)
3. **Monthly exec summary** (above)
4. **Amber pre-read** — Scenario A
5. **Red incident first-update** — Scenario B
6. **Cutover go/no-go checklist** (per service)
7. **Postmortem template** (blameless, 5-whys + actions)
8. **Phase exit sign-off form** (criteria from timeline doc, signed by VP Eng + Product Director)

These exist *before* I need them. Writing them under stress is how the message goes off the rails.

---

## What “communicating well” looks like on this project

- VP Eng is never surprised on a Friday by something I knew on a Tuesday.
- Product Director never finds out about a slip from a downstream team.
- The team never reads in the status email something they didn’t hear in the retro first.
- When I escalate, the person receiving it leaves the meeting with a smaller problem than they came in with.
- When I deliver, I don’t sell it harder than the result deserves.

The lecture line I keep coming back to: *the best delivery management is invisible when you’re doing it well — stakeholders don’t get surprised, the team doesn’t feel overwhelmed, and the product ships when you said it would.* That is the bar.
