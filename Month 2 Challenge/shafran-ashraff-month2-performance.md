# Performance Reviews

*Practice documentation — align ratings and examples with your organization’s calibration process.*

## Performance Review: Alex Chen

**Review period:** H1 2026 (Jan–Jun)  
**Role:** Senior Software Engineer  
**Rating:** Exceeds expectations

### Summary

Alex sustained a high bar for technical quality while expanding into leadership behaviors that match our Tech Lead profile: clearer tradeoffs under ambiguity, more proactive stakeholder alignment, and dependable mentorship. The primary growth edge is balancing speed with delegation — sometimes owning too much of the critical path. Overall, Alex is a strong promotion candidate *when* role scope and stakeholder leadership are consistently demonstrated at the next level.

### Results (what)

**Key accomplishments**

1. **Payments reliability workstream** — Led design and rollout of idempotency safeguards and retry semantics for the checkout payment adapter. Cut payment-related incident pages by roughly 40% quarter-over-quarter (per on-call stats). Partnered with SRE to tighten dashboards and alerting.

2. **API contract hardening** — Drove versioning and deprecation policy for the internal billing API consumers. Reduced breaking changes caught late in QA by shifting failures left into contract tests and design reviews.

3. **Team multiplier** — Routinely turned complex reviews into teaching moments; paired with Casey on notification service work and left behind clearer patterns for error handling and testing seams.

**Metrics (illustrative — replace with your systems)**

| Metric | Target | Actual (H1) |
|--------|--------|----------------|
| Committed sprint work completed | 85% | 95% |
| Median PR review turnaround (team SLA) | 24h | 14h |
| Sev-1/Sev-2 incidents owned to resolution | n/a | 2 major, both within SLA |

### How (behaviors)

**Strengths**

- Systems thinking: surfaces edge cases early; writes decisions down.  
- Collaboration: earns trust across eng/product; disagrees professionally.  
- Quality: tests and observability are not afterthoughts.

**Development areas**

- Delegation: still tends to carry “hot” refactors solo — develop others by splitting ownership.  
- Facilitation: architecture discussions sometimes go deep before aligning on decision criteria and timebox.  
- Stakeholder management: strong 1:1 relationships; broaden to group settings (workshops, quarterly planning).

### Growth (progress on prior goals)

| Prior goal | Status | Evidence |
|------------|--------|----------|
| Lead a meaningful cross-team initiative | Met | Payments reliability + billing API consumers alignment |
| Improve operational readiness of owned services | Met | Runbook updates, alert tuning, postmortem follow-through |
| Grow facilitation / meeting leadership | Partial | Led several sessions; still building consistency |

### Impact

Alex’s work reduced customer-visible payment failures and lowered toil for on-call. Their reviews and pairing measurably improved Casey’s delivery confidence (Casey’s independent PR throughput increased after the pairing block).

### Future (next period)

**Goals (H2 2026)**

1. Own end-to-end technical narrative for one cross-team roadmap item (including stakeholder comms and milestone plan).  
2. Facilitate two architecture forums with explicit outcomes (decision log + follow-ups).  
3. Mentor Casey (or another junior) through one independently owned feature with lightweight oversight.

**Promotion readiness (Tech Lead)**

- **Readiness:** strong on technical leadership; growing on org leadership.  
- **Recommended focus before promotion packet:** sustained stakeholder leadership in group settings + delegation evidence.  
- **Suggested timeline:** promotion discussion realistic in [Q3/Q4 2026] *if* headcount and scope align — confirm with skip-level and HR.

---

## Performance Review: Riley Park

**Review period:** H1 2026 (Jan–Jun)  
**Role:** Senior Software Engineer  
**Rating:** Needs improvement (support plan in place)  

### Summary

Riley remains capable on paper — deep familiarity with our checkout domain — but delivery consistency and engineering hygiene slipped materially this period. Several gaps correlate with personal circumstances Riley disclosed; we responded with a support-oriented plan (reduced load, closer check-ins, pairing). The path forward requires *sustained* improvement on commitments, communication, and quality, with clear checkpoints. Nothing in this document should be news if ongoing 1:1s and feedback have been handled as agreed.

### Results (what)

**What went well**

- Contributed fixes during a stressful incident week; still willing to engage when pulled in directly.  
- Security-sensitive areas were escalated appropriately (no evidence of risky silence).

**Concerns (specific)**

1. **Missed three sprint commitments** in H1 on checkout-related work (slips communicated late or not at all).  
2. **Quality:** three P2 defects escaped to staging/production in delivered work (traceability + test gaps).  
3. **Throughput:** median PR review turnaround for Riley’s reviews regressed vs. team norm; documentation for two shipped items was incomplete enough that the next engineer needed rework.

**Metrics (illustrative)**

| Metric | Target | Actual (H1) |
|--------|--------|----------------|
| Sprint commitment completion | 80% | 55% |
| Median PR review turnaround | 24h | 72h |
| Bug escape rate (post-merge defects) | <5% | ~15% (elevated) |

### How (behaviors)

**Observed strengths**

- Domain knowledge is still valued by peers when Riley is engaged.  
- Interpersonal tone with teammates has remained respectful even under stress.

**Concerns**

- Reliability: missed meetings without timely notice; stakeholders lacked early warning on slips.  
- Communication: async updates sometimes absent during multi-day pushes.  
- Quality bar: reintroduced patterns Riley historically would have caught (race-y state handling, incomplete negative tests).

### Context (confidential / sensitive)

Personal factors affected capacity and focus during portions of H1. Details belong in HR/private notes where required; this review references only what is necessary to explain the support plan and expectations.

### Support plan (active)

**Immediate**

- Capacity targeted at **~70%** sprint load for 2 weeks, with explicit “must deliver” scope per sprint.  
- **Weekly** 30-minute check-ins (separate from standard cadence if needed).  
- Pairing with **Morgan** on checkout changes for design/test review discipline.  
- **EAP / flexibility** offered per policy.

**Checkpoint**

- **8-week** formal checkpoint: commitment hit rate, defect rate, meeting attendance, and communication early-warning behaviors.

### Path to good standing

**Clear expectations (examples — calibrate to HR guidance)**

1. Meet agreed sprint commitments at the adjusted capacity; if at risk, flag **≥24 hours** early with a proposed cut.  
2. Attend required meetings or provide notice *ahead* of time.  
3. Deliver work with tests and documentation that meet the senior bar checklist (link internal standard).

**Support offered**

- Pairing, smaller tickets, clearer acceptance criteria, and access to wellbeing resources.

### Future (next period)

If the support plan succeeds, H2 goals reset to sustainable senior-level ownership (one owned initiative + dependable reviews). If expectations are not met despite support, we will follow company performance policy with HR.

**Employee comments**

- Space for Riley to add perspective during review conversation
