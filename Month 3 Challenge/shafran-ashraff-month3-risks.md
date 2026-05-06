# Project Risk Assessment: Monolith → Microservices Migration

_Scoring: **Probability (1–5) × Impact (1–5)** = Risk Score (1–25). Bands: **Critical 16–25**, **High 9–15**, **Medium 4–8**, **Low 1–3**. Living document — reviewed at every sprint review and refreshed at every phase gate._

**Project at a glance**

- 9-month migration, monolith decomposed into 8 microservices.
- 99.9% uptime is non-negotiable.
- Team of 6 (≈4.8 FTE — see capacity plan).
- Hard constraints: Black Friday freeze (Nov), two engineers at 50%, limited shared test environments.

---

## Risk 1 — Data Consistency During Dual-Run / Cutover

**Category:** Technical / Data
**Probability:** 4 (High) — dual-write windows are inherently lossy without strong tooling.
**Impact:** 5 (Critical) — silent data drift on orders or payments is the worst class of incident we can ship.
**Risk Score:** **20 (Critical)**

**Description**
While both monolith and the new service are live, writes can diverge: the monolith commits, the new service rejects (or the inverse), and we end up with two versions of the truth. The Order and Payment slices are the highest-stakes places this can happen.

**Indicators / early warning**

- Reconciliation job reports >0.05% divergence over a 1-hour window.
- Dead-letter queue depth growing on the change-data-capture (CDC) stream.
- Customer support tickets referencing missing or stale order state.
- Drift between `monolith.orders` row count and `order-svc.orders` aggregate over a sliding window.

**Mitigation strategies**

1. **Primary — Outbox + CDC, not raw dual-write.**
   - Owner: Tech Lead
   - Timeline: completed before any write traffic moves (Phase 2 entry gate).
   - Cost: ~2 weeks engineering effort + 0.5 week SRE.
2. **Reconciliation job as a first-class service.** Hourly batch + on-demand for incident response.
   - Owner: Senior 1
   - Timeline: live before User Service cutover.
   - Cost: 1 week.
3. **Per-service feature flag + traffic-shaping** (1% → 10% → 50% → 100%) so we can drain back fast.
   - Owner: Senior 3
   - Timeline: enforced gate per service.
   - Cost: ~1 week per service (parallelised with build).

**Contingency**
If reconciliation breaches threshold: pause shifts, route 100% reads/writes to monolith, freeze cutover, run reconciliation, RCA before resuming. No “fix forward” on data integrity.

---

## Risk 2 — Black Friday Freeze Collides with Cutover Plan

**Category:** Schedule / Business
**Probability:** 5 (Very Likely) — the freeze window is fixed.
**Impact:** 4 (High) — losing 4 weeks of deploy capacity in our most aggressive phase.
**Risk Score:** **20 (Critical)**

**Description**
The mandatory freeze (1 Nov – 30 Nov) lands inside Phase 4 (cutover & decommission). Anything not stabilised by late October cannot move until December, which compresses the year-end and pushes operational risk into the Christmas peak.

**Indicators**

- Phase 3 burndown trailing plan by >15% at week 22.
- Any service still running below dual-traffic at week 24.
- Open Sev-2 production tickets per service > 3 entering October.

**Mitigation**

1. **Freeze-aware milestone planning.** All cutovers scheduled to complete by **Oct 24** (1-week safety margin before freeze).
   - Owner: Tech Lead
   - Timeline: locked in Phase 1 planning.
2. **Bring the riskiest cutovers forward.** Order and Payment go before Q4 traffic ramp, not after.
   - Owner: Tech Lead + Product Director.
3. **Pre-agreed “freeze exceptions” policy** with VP Eng — what counts as P1 hotfix during freeze, who approves, and the rollback bar.
   - Owner: Engineering Manager.
   - Timeline: documented by end of Phase 1.

**Contingency**
If we’re not stabilised by Oct 24: do not start a cutover. Hold the service on monolith, ride out freeze, resume Dec 1. Better to extend timeline by 4 weeks than be mid-cutover during peak traffic.

---

## Risk 3 — Distributed Transaction Complexity (Order/Payment/Inventory)

**Category:** Technical / Architecture
**Probability:** 4 (High) — three services touching one user action is the classic saga problem.
**Impact:** 4 (High) — partial failures = lost revenue or oversold stock.
**Risk Score:** **16 (Critical)**

**Description**
Once Order, Payment, and Inventory are separate services, an end-to-end checkout becomes a distributed workflow. Naïve synchronous calls give us the worst of both worlds: monolith coupling without monolith atomicity.

**Indicators**

- 5xx rates on checkout climbing as services split.
- Saga compensation events firing more than 1% of the time.
- Reconciliation discrepancies between “orders placed” and “payments captured”.

**Mitigation**

1. **Saga pattern with explicit compensations** (orchestrated, not choreographed — easier to debug).
   - Owner: Tech Lead (architecture), Senior 1 (impl).
   - Timeline: design ratified end of Phase 1; reference implementation by mid-Phase 2.
   - Cost: 2 weeks design + spike.
2. **Idempotency keys end-to-end** on every cross-service write.
   - Owner: Senior 3.
   - Timeline: before first cross-service production call.
3. **Chaos / fault-injection day per service** before promoting to 100% traffic.
   - Owner: Tech Lead.
   - Timeline: gate at every cutover.

**Contingency**
Fall back to “strangler with compatibility shim” — service-level decomposition without splitting the transactional boundary, accepting we won’t fully decompose Order/Payment/Inventory in this project window.

---

## Risk 4 — Performance Regression After Decomposition

**Category:** Technical / Performance
**Probability:** 4 (High) — network calls always cost something; we will hit it somewhere.
**Impact:** 3 (Medium) — recoverable, but visible to customers if not caught early.
**Risk Score:** **12 (High)**

**Description**
What was an in-process call becomes an HTTP/gRPC hop. Without care, p95 latency on critical paths (login, product page, checkout) will regress. If we discover this at cutover, we’re backed into a corner.

**Indicators**

- p95 on a migrated endpoint > monolith baseline + 20%.
- Error budget burn doubling against pre-migration baseline.
- Cache hit ratio dropping (a sign we lost a co-located in-memory cache).

**Mitigation**

1. **Performance baseline captured per endpoint _before_ migration**, with an explicit budget per service (e.g. Auth p95 ≤ 80ms).
   - Owner: Senior 2.
   - Timeline: Phase 1 exit gate.
2. **Synthetic load tests in CI for every service**, blocking merge on regression > threshold.
3. **Connection pooling, gRPC where it pays, caching at the edge.** Don’t re-litigate per service — set a default and document deviations.
4. **Cutover gate:** 24h of shadow traffic before flipping reads.

**Contingency**
If p95 regresses post-cutover: drop traffic to 10%, profile, optimise; if not recoverable in 1 sprint, route back to monolith and treat as a Phase 3 task.

---

## Risk 5 — Team Capacity Gap (Half-time Engineers + Tech Lead Split)

**Category:** Resource
**Probability:** 5 (Very Likely) — already true on day 1.
**Impact:** 3 (Medium) — manageable with discipline, painful if denied.
**Risk Score:** **15 (High)**

**Description**
Two engineers are at 50%, the Tech Lead is at 80%, and one mid is still ramping on Kubernetes. Effective capacity is ~4.8 FTE against a plan that quietly assumes 6. Every assumption error lands here.

**Indicators**

- Velocity below 80% of plan for 2 consecutive sprints.
- Carryover items > 20% of sprint scope.
- “Split” engineers context-switching back to their other project mid-sprint.

**Mitigation**

1. **Plan against 4.8 FTE, not 6.** All commitments use adjusted velocity (see capacity plan).
2. **No critical-path work assigned to 50% engineers as sole owners.** They pair, review, or own non-critical-path slices.
3. **Pre-approved contractor budget** ($50K, 6 months) — see capacity plan, Option 1.
4. **Weekly availability check** before sprint planning — vacations, on-call, other-project demands.

**Contingency**
If velocity sustains <80% for two sprints, trigger Option 1 (contractor) or Option 2 (descope two non-critical services). Decision owner: Tech Lead with VP Eng sign-off.

---

## Risk 6 — Knowledge Gaps (Kubernetes, Service Mesh, Observability)

**Category:** Resource / Capability
**Probability:** 4 (High) — only Tech Lead is K8s-fluent on day 1.
**Impact:** 3 (Medium) — slows Phase 1 and creates single-point-of-failure for ops.
**Risk Score:** **12 (High)**

**Description**
If only one person can debug a pod-level issue at 2am, we have an availability risk dressed up as a knowledge risk. Mid 1 is keen but learning, and the seniors have varied exposure.

**Indicators**

- Tech Lead pulled into >2 ops issues per week.
- PR queue stuck on K8s/Helm changes waiting for Tech Lead review.
- On-call escalations all routing to one person.

**Mitigation**

1. **Pairing schedule for Phase 1:** Mid 1 + Tech Lead on cluster setup, Senior 2 + Tech Lead on observability stack.
2. **Runbooks written _as we build_, not after.** Definition of Done for Phase 1 includes runbook + on-call playbook.
3. **Lunch-and-learn series, weekly, 30 min** — concrete topics (probes, RBAC, SLOs, tracing).
4. **Two-person rule for production change** by end of Phase 1.

**Contingency**
If knowledge spread is still narrow at end of Phase 1, pause Phase 2 entry by 1 week to invest in a deliberate knowledge transfer sprint. Cheaper than learning under fire.

---

## Risk 7 — Limited Shared Test Environment Capacity

**Category:** Operational / Tooling
**Probability:** 4 (High) — already a known constraint.
**Impact:** 3 (Medium) — bottlenecks integration testing across teams.
**Risk Score:** **12 (High)**

**Description**
With 8 services in flight and shared infrastructure, “who has the staging cluster this afternoon” becomes a daily question. Bad enough on its own, worse when it masks integration defects until late.

**Indicators**

- Scheduling conflicts logged > 2/week.
- Integration test failures attributed to “env state” > defects.
- QA cycles slipping a sprint because env wasn’t ready.

**Mitigation**

1. **Ephemeral environments per PR** (namespace-per-PR on the cluster) for service-level testing.
   - Owner: Senior 1 (DevOps lead).
   - Timeline: stood up by end of week 4.
2. **One protected staging slot per service**, booked in Azure DevOps as a resource.
3. **Contract tests + consumer-driven contracts** so most integration validation is moved left into CI rather than relying on shared envs.

**Contingency**
If ephemeral envs slip, agree a written booking discipline (1 service per slot, 4-hour blocks) and accept up to 1 week per phase of buffer for env contention.

---

## Risk 8 — Rollback Complexity After Schema or Contract Changes

**Category:** Technical / Operational
**Probability:** 3 (Possible)
**Impact:** 4 (High) — a forward-only schema change with bad data is a multi-day incident.
**Risk Score:** **12 (High)**

**Description**
We can deploy in seconds; we cannot un-migrate data in seconds. Backward-incompatible schema changes, destructive data shape changes, or breaking API versioning all trap us into “fix forward” because rollback is too expensive.

**Indicators**

- A migration PR that drops or renames a column without a transitional path.
- API change that bumps a major version without a deprecation overlap.
- Deployment runbook missing a tested rollback step.

**Mitigation**

1. **Expand-contract migration pattern** is the default. Drops only after two sprints of dual-read.
2. **API versioning policy** — N and N-1 supported, breaking changes require a 1-sprint deprecation window.
3. **Rollback rehearsal** per service in pre-prod before cutover. Untested rollback = no rollback.
4. **Backups verified, not just taken**, with a documented restore time per service.

**Contingency**
For any change that cannot be cleanly rolled back, require dual sign-off (Tech Lead + EM) and a written abort plan before deploy.

---

## Risk 9 — Observability Gap During Decomposition

**Category:** Operational
**Probability:** 3 (Possible)
**Impact:** 3 (Medium)
**Risk Score:** **9 (High)**

**Description**
Tracing across 8 services is a different sport than logging in a monolith. If we don’t invest early, an outage becomes a guessing game and MTTR balloons.

**Indicators**

- Incidents where root cause takes >2x baseline MTTR.
- Spans missing or trace context lost across hops.
- Dashboards drifting out of date as services evolve.

**Mitigation**

1. **OpenTelemetry from day 1** — instrumentation library standardised in Phase 1.
2. **SLO per service** (latency + error rate), reviewed in retros.
3. **Centralised dashboard per service in Azure DevOps / Grafana** — same template, no per-team flavour.
4. **Trace IDs propagated through every layer**, including async/queue paths.

**Contingency**
If observability is not in shape by end of Phase 1, do not enter Phase 2. Treat it as a hard gate, same as security review.

---

## Risk 10 — Stakeholder Misalignment on “Done”

**Category:** Stakeholder / Scope
**Probability:** 3 (Possible)
**Impact:** 3 (Medium)
**Risk Score:** **9 (High)**

**Description**
“Migration complete” means different things to engineering, product, and finance. Without a shared definition we ship and then argue, which kills credibility for the next big initiative.

**Indicators**

- New “must-have” showing up in month 6 that wasn’t in scope at kickoff.
- Product asking for feature work mid-migration that contradicts the freeze plan.
- Different stakeholders quoting different end dates back to us.

**Mitigation**

1. **Definition of Done per service** — agreed at Phase 1 exit, signed off by Product + Eng.
2. **Single source of truth** — the timeline and risk register in this folder; everything else is a copy.
3. **Change control** — any scope change must come with a swap (drop X to add Y), routed through Tech Lead + Product Director.
4. **Bi-weekly newsletter** so changes don’t arrive as surprises.

**Contingency**
If scope change pressure exceeds capacity, escalate to VP Eng with the Communication Scenario template (situation → root cause → 3 options → recommendation).

---

## Risk Matrix (5×5)

|                     | Impact 1 — Negligible | Impact 2 — Low | Impact 3 — Medium                     | Impact 4 — High            | Impact 5 — Critical |
| ------------------- | --------------------- | -------------- | ------------------------------------- | -------------------------- | ------------------- |
| **5 — Very Likely** |                       |                |                                       | **R2** (20)                |                     |
| **4 — Likely**      |                       |                | **R4** (12), **R6** (12), **R7** (12) | **R3** (16)                | **R1** (20)         |
| **3 — Possible**    |                       |                | **R9** (9), **R10** (9)               | **R5** (12)\*, **R8** (12) |                     |
| **2 — Unlikely**    |                       |                |                                       |                            |                     |
| **1 — Rare**        |                       |                |                                       |                            |                     |

\*R5 plotted at probability 5 / impact 3 (=15) but shown here in the column where impact aligns; placed in Possible-High row by impact for visual clarity. The score in the register is what counts.

**Distribution**

- **Critical (16–25):** R1, R2, R3 — 3 risks
- **High (9–15):** R4, R5, R6, R7, R8, R9, R10 — 7 risks
- **Medium (4–8):** 0
- **Low (1–3):** 0

If everything is critical, nothing is — but on a 9-month, 99.9% uptime migration with a fixed freeze, a top-heavy register is honest, not lazy. That is what we are signing up for.

---

## Risk Monitoring Plan

| Risk                          | Review frequency                               | Owner               | Escalation trigger                           |
| ----------------------------- | ---------------------------------------------- | ------------------- | -------------------------------------------- |
| R1 — Data consistency         | Daily during any cutover; weekly otherwise     | Tech Lead           | Any reconciliation drift > 0.05%             |
| R2 — BF freeze conflict       | Weekly from week 16 onwards                    | Tech Lead           | Phase 3 burndown >15% behind plan at week 22 |
| R3 — Distributed transactions | Weekly from start of Phase 2                   | Tech Lead           | Saga compensation rate > 1%                  |
| R4 — Performance regression   | Per-service cutover gate                       | Senior 2            | p95 regress > 20% vs. baseline               |
| R5 — Capacity gap             | Every sprint planning + retro                  | Engineering Manager | Velocity < 80% target for 2 sprints          |
| R6 — Knowledge gaps           | Bi-weekly                                      | Tech Lead           | Tech Lead pulled into >2 ops incidents/week  |
| R7 — Test env capacity        | Weekly (env owner)                             | Senior 1            | Env-related slips > 1 day in a sprint        |
| R8 — Rollback complexity      | Per-PR for migrations; per-service pre-cutover | Tech Lead           | Untested rollback path on a deploying change |
| R9 — Observability            | End of every phase                             | Senior 2            | Incident MTTR > 2x baseline                  |
| R10 — Stakeholder alignment   | Bi-weekly newsletter + monthly CTO sync        | Tech Lead           | New “must-have” raised mid-phase             |

---

## Summary

- **Critical risks:** 3 (R1 data consistency, R2 freeze conflict, R3 distributed transactions)
- **High risks:** 7
- **Medium risks:** 0
- **Low risks:** 0
- **Total mitigation budget (engineering effort):** ~10 weeks (≈12% of capacity)
- **Top three to talk about with VP Eng this week:** R1, R2, R5.

The honest read: on this project, the _operational_ risks (cutover, freeze, capacity) outweigh the _technical_ risks. We can write good services. We need to be relentless about how and when we cut them over.
