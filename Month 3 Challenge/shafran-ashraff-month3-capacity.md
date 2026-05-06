# Capacity Planning: Monolith → Microservices Migration

## Team Composition

| Name        | Role                | Availability                    | Skills / strengths                          | Weak spots                          |
|-------------|---------------------|---------------------------------|---------------------------------------------|-------------------------------------|
| Tech Lead   | Lead                | **80%** (20% architecture board, escalations) | Full-stack, K8s, distributed systems       | Bandwidth — not an IC at scale here |
| Senior 1    | Engineer (DevOps lean) | **100%**                     | Backend (Java), CI/CD, infra-as-code        | Limited frontend exposure           |
| Senior 2    | Engineer            | **50%** (split with another project) | Backend (Node), observability, perf       | Fragmented availability             |
| Senior 3    | Engineer            | **100%**                       | Full-stack, strong on data modelling        | Newer to K8s; ramping in Phase 1    |
| Mid 1       | Engineer            | **100%**                       | Frontend, learning K8s actively             | Backend depth; first migration project |
| Mid 2       | Engineer            | **50%** (split with another project) | Backend                                  | K8s ramp; needs paired work on hard tasks |

**Headcount:** 6 engineers
**Effective FTE:** 0.8 + 1.0 + 0.5 + 1.0 + 1.0 + 0.5 = **4.8 FTE**

This is the number we plan against. Plans built on “6 engineers” quietly assume 6.0 FTE and silently overshoot by 20% before sprint 1.

---

## Velocity Analysis

### Historical baseline (last 3 sprints, similar team shape)

| Sprint | Committed | Delivered | Notes                              |
|--------|-----------|-----------|------------------------------------|
| S-3    | 34        | 32        | Normal sprint                      |
| S-2    | 33        | 30        | One engineer on leave 3 days       |
| S-1    | 36        | 34        | Slightly heavy, no carryover       |
| **3-sprint average** | — | **32 points/sprint** | Use this as baseline |

**Why I use the 3-sprint average:** the lecture made the point — never use the best sprint, never use the “overtime sprint”. Average over a stable period is the only honest number.

### Adjusted velocity for this project

Starting from 32 pts/sprint (assumed at 6.0 FTE):

| Adjustment                                                                 | Impact          |
|-----------------------------------------------------------------------------|-----------------|
| Effective FTE: 4.8 / 6.0                                                    | × 0.80          |
| Focus factor 65% (industry-typical 60–70%, applied to baseline that was already partial) | (already in baseline) |
| Phase 1 ramp / K8s learning curve (first 8 weeks only)                      | × 0.80 (P1 only)|
| **Adjusted steady-state velocity (Phase 2 onwards)**                        | ≈ **25 pts/sprint** |
| **Phase 1 velocity (with ramp)**                                            | ≈ **20 pts/sprint** |

That is the number commitments are sized against.

---

## Project Estimation (top-down sanity check)

| Phase                | Est. story points | Sprints @ adj. velocity | Calendar weeks  |
|----------------------|-------------------|-------------------------|------------------|
| Foundation           | 80                | 4 (Phase 1 velocity 20) | 8 wk → planned 6 wk + 1 sprint phase buffer |
| Core Services        | 200               | 8 (steady 25)           | 16 wk → planned 10 wk + buffer |
| Supporting Services  | 120               | 5 (steady 25)           | 10 wk → planned 10 wk |
| Cutover + Hardening  | 50                | 2                       | 4 wk + freeze buffer |
| **Total**            | **450**           | **19**                   | **38–40 wk** raw, **36 wk** planned with disciplined buffer |

**Honest read:** the raw math says we need ~19 sprints; we have 18. The 1-sprint gap is closed by (a) parallelising Notification and Search in Phase 3, and (b) treating the BF freeze window as a hard slip-absorber rather than productive time.

---

## Capacity Gap Analysis

**Required velocity to hit 18-sprint timeline:** 450 / 18 = **25 pts/sprint** ✓ matches steady-state adjusted velocity.

But the *risk-adjusted* picture isn’t that clean:

| Risk factor                                                  | Velocity impact          |
|--------------------------------------------------------------|--------------------------|
| Phase 1 K8s learning curve                                   | −20% over 4 sprints      |
| Cross-service integration delays (R3, R4)                    | −10% on average          |
| Holiday season + planned leave (Jul/Aug/Dec)                 | ~−2 sprints over project |
| Half-time engineers context-switching back to other projects | −5% on weeks where it bites |

If all of those land at once, we’re at ~21 pts/sprint effective, which translates to a ≈ 22-sprint plan — a 4-sprint (8-week) overrun against the contract date.

**That is the gap.** We close it deliberately — not by hope.

---

## Mitigation Options (presented to VP Eng + Product Director at kickoff)

### Option 1 — Add a contractor (recommended)

- **Cost:** ~$50K for 6 months (1 mid-senior backend, 0.8 FTE allowing for ramp).
- **Capacity impact:** +0.8 FTE → ~+5 pts/sprint after a 2-sprint ramp.
- **Timeline impact:** restores 18-sprint plan, holds 24 Oct cutover deadline.
- **Why it’s the recommendation:** smallest disruption to product roadmap, biggest controllable lever, removes a known gap rather than betting on optimism.
- **Risk it adds:** onboarding overhead in Phase 1 (already counted in ramp); knowledge dependency on a non-permanent engineer.

### Option 2 — Reduce scope

- **Approach:** defer 2 non-critical services (candidates: Notification and Search — both off the critical path).
- **Capacity impact:** −80 pts of work.
- **Timeline impact:** ~32 weeks; 4 weeks ahead of the freeze.
- **Trade-off:** Notification stays on the monolith, blocking later product roadmap items; Search retains current performance ceiling.
- **When to choose this:** if budget for Option 1 isn’t signed off by end of Sprint 2, this becomes the fallback.

### Option 3 — Extend the timeline

- **New end date:** Nov 2025 — pushes critical work *into* the BF freeze.
- **Why this is on the list:** completeness.
- **Why it’s rejected:** it re-opens R2 (the freeze conflict), which is the most expensive risk in the register. Saving budget by spending availability is the wrong trade for a 99.9% uptime project.

**Recommendation in one line:** Option 1 if the budget exists; Option 2 if not. Option 3 only as a forced last resort with VP Eng explicit approval.

---

## Sprint-by-Sprint Plan (key sprints — full plan in Azure DevOps)

### Sprint 1–2: Foundation (Phase 1 ramp)

| Engineer    | Focus                                            | Points |
|-------------|--------------------------------------------------|--------|
| Tech Lead   | K8s architecture, secrets, RBAC                  | 5      |
| Senior 1    | CI/CD template + ephemeral envs                  | 6      |
| Senior 2    | Observability stack (OTel, dashboards)           | 4      |
| Senior 3    | Auth service skeleton                            | 5      |
| Mid 1       | K8s ramp (paired with Tech Lead) + helm charts   | 2      |
| Mid 2       | CI/CD support + image hardening                  | 2      |
| **Total**   |                                                  | **24** |

### Sprint 3: Auth go-live + Phase 1 demo

| Engineer    | Focus                                            | Points |
|-------------|--------------------------------------------------|--------|
| Tech Lead   | Cutover orchestration, runbook                   | 4      |
| Senior 1    | CI/CD hardening                                  | 5      |
| Senior 2    | Perf baseline capture                            | 4      |
| Senior 3    | Auth dual-run, rollout                           | 6      |
| Mid 1       | Helm template, monitoring dashboards             | 3      |
| Mid 2       | Test data harness                                | 2      |
| **Total**   |                                                  | **24** |

### Sprint 6 (mid-Phase 2 — Order Service crunch)

| Engineer    | Focus                                            | Points |
|-------------|--------------------------------------------------|--------|
| Tech Lead   | Saga design ratification, code review, blockers  | 4      |
| Senior 1    | Order service core + saga orchestrator           | 8      |
| Senior 2    | Reconciliation job + perf testing                | 4      |
| Senior 3    | User → Order integration                          | 6      |
| Mid 1       | Frontend integration on Order                    | 3      |
| Mid 2       | Compensation handlers, idempotency keys          | 2      |
| **Total**   |                                                  | **27** |

### Sprint 12 (Phase 3 — Payment + Inventory parallel)

| Engineer    | Focus                                            | Points |
|-------------|--------------------------------------------------|--------|
| Tech Lead   | PCI scope, security review, escalations          | 3      |
| Senior 1    | Payment service core                             | 8      |
| Senior 2    | Perf budgets, observability for Payment + Inv    | 4      |
| Senior 3    | Inventory service                                | 6      |
| Mid 1       | Notification service (off-critical-path)         | 4      |
| Mid 2       | Inventory test data + reconciliation             | 2      |
| **Total**   |                                                  | **27** |

### Sprint 16 (Phase 4 — decommission)

| Engineer    | Focus                                            | Points |
|-------------|--------------------------------------------------|--------|
| Tech Lead   | Decommission orchestration, comms                | 4      |
| Senior 1    | Monolith write-path removal (Order, Payment)     | 7      |
| Senior 2    | Load test, DR drill                              | 5      |
| Senior 3    | Monolith write-path removal (User, Product)      | 6      |
| Mid 1       | Documentation, runbooks                          | 3      |
| Mid 2       | Support hand-off material                        | 2      |
| **Total**   |                                                  | **27** |

(Per-engineer points are rounded; the totals are what we commit on. Junior engineers are intentionally below their headline FTE share to leave room for pairing and review without it looking like padding.)

---

## Allocation Mix per Sprint

The 60/15/10/15 split from the lecture, applied to this project:

| Category    | Allocation        | Notes                                                                 |
|-------------|-------------------|-----------------------------------------------------------------------|
| Features    | ~60% (≈15 pts)    | Migration is mostly “features” for the purpose of this split          |
| Bugs        | ~15% (≈4 pts)     | Migration tends to find latent monolith bugs — budget for it          |
| Tech debt   | ~10% (≈3 pts)     | Observability, runbooks, pipeline polish                              |
| Buffer      | ~15% (≈3 pts)     | Held by Tech Lead, not pre-assigned                                   |

In Phase 1 we shift toward **70% features / 5% tech debt** because the platform IS the feature.
In Phase 4 we shift toward **40% features / 30% hardening** as per the lecture pattern.

---

## Leave & Availability

| Month     | Planned leave            | Capacity impact                    | Note                          |
|-----------|--------------------------|------------------------------------|-------------------------------|
| April     | Mid 1 (1 wk)             | ~−5%                                | Small, absorbable             |
| July      | Senior 3 (2 wk), Senior 1 (1 wk) | ~−1 sprint of capacity        | Plan no critical-path cutover this month |
| August    | Tech Lead (2 wk)         | Tech Lead handover for 2 wk         | EM covers escalations         |
| December  | 4 weeks total spread     | ~−2 sprints (already in BF buffer)  | Inside freeze window — fine   |

We refresh this calendar at the start of each month and **re-baseline velocity if total leave > 1 person-week in a sprint**.

---

## Allocation Model

We chose a **dedicated team model with 2 partial allocations** (Senior 2 and Mid 2). Tracked in Azure Boards as resource allocation %.

- **Why not fully dedicated:** we don’t control the budget for it; Senior 2 and Mid 2 are committed elsewhere.
- **Hard rule:** the 50% engineers don’t own critical-path work as sole owners (R5 mitigation). They pair, review, or own off-critical-path slices.
- **Context-switching tax:** counted in the focus factor; visible in retros if it grows.

---

## Capacity Monitoring

**Weekly tracking**

- Actual vs. planned velocity (rolling 3-sprint).
- Availability deltas (leave, on-call shifts, other-project encroachment).
- Scope changes in points (added or descoped).
- Buffer burn (how much of the project buffer is consumed vs. how much project time has elapsed).

**Re-planning triggers — no debate, just trigger the meeting**

| Trigger                                                                  | Action                                                                 |
|---------------------------------------------------------------------------|------------------------------------------------------------------------|
| Velocity < 80% of target for 2 consecutive sprints                        | Re-plan; consider Option 1 (contractor) or Option 2 (descope)          |
| Unplanned absence > 1 week within a sprint                                | Re-baseline that sprint’s scope; protect critical path                 |
| Scope increase > 50 points without an equal swap                          | Escalate to Product Director with Communication Scenario template      |
| Buffer consumed > 50% before 50% of project time elapsed                  | Status flips to **Amber**, escalate per stakeholder plan              |
| Critical-path work blocked > 5 working days                               | Tech Lead pulled in directly; if not unblocked in 1 sprint → Red      |

---

## One-page summary (for the VP Eng kickoff)

- **Plan against 4.8 FTE, not 6.** Anything else is wishful thinking.
- **Steady-state velocity: 25 pts/sprint.** Phase 1 is 20 due to ramp.
- **18-sprint plan is achievable** *only* with one of: Option 1 (contractor), Option 2 (descope two services), or genuinely faster Phase 1 ramp.
- **Recommendation:** Option 1 — $50K for 6 months, smallest roadmap disruption, restores margin.
- **Re-plan triggers are written down in advance** so we don’t debate them mid-sprint when emotions are high.
