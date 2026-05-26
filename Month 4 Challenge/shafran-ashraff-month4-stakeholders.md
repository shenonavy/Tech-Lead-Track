# Stakeholder Analysis: Real-Time Analytics Platform

## Context

We're building a real-time analytics platform that touches nearly every team in the org. As the tech lead on this, I need buy-in and active participation from Product, Design, Ops, Data, and Finance. The tricky part is that none of these teams report to me, and some have existing tensions with Engineering that I need to navigate carefully.

---

## Stakeholder Register

### Key Stakeholders

#### Sarah - VP Product
**Role:** Executive sponsor on Product side  
**Interest Level:** High  
**Influence Level:** High  
**Current Stance:** Supportive but pushing hard on timeline  
**Motivations:**
- Market differentiation — competitors are shipping analytics features
- Q3 revenue targets tied to enterprise client renewals
- Responding to customer feedback from NPS surveys about lack of reporting
- Wants to demonstrate Product's ability to drive strategic initiatives

**Concerns:**
- Engineering velocity — feels past projects slipped quietly
- Feature scope creep from engineering "gold plating"
- Competitive pressure from two direct competitors who launched dashboards last quarter

**Preferred Communication:** Weekly 1:1, concise updates with data. She hates lengthy docs without a clear recommendation. Prefers options with trade-offs laid out.

**Engagement Strategy:**
- Weekly progress updates with key metrics (velocity, blockers, scope)
- Involve her in architecture decision trade-offs that affect timeline
- Align on MVP scope in first week — get written agreement on what's in/out
- Share competitive intelligence I find during technical research
- Give early warnings, never surprises

---

#### Mike - Design Director
**Role:** Controls design resource allocation across 4 product streams  
**Interest Level:** Medium (would be higher if he had bandwidth)  
**Influence Level:** Medium-High (can block us if no designer is assigned)  
**Current Stance:** Skeptical — his team is overloaded with the mobile redesign and checkout flow projects  
**Motivations:**
- Protecting his team from burnout (lost a senior designer last quarter)
- Delivering quality work, not rushed jobs
- Wants his team recognized for strategic contributions, not just "making things pretty"
- Interested in data visualization as a growth area for his designers

**Concerns:**
- Being pulled into another project that goes sideways
- Timeline commitments that box his team in
- Engineering changing requirements mid-design

**Preferred Communication:** Informal — prefers coffee chats over formal meetings. Values being consulted early rather than handed specs. Responds better to collaboration than requests.

**Engagement Strategy:**
- Start with relationship building — grab coffee, understand his current pain points
- Frame this as a strategic opportunity for his team (data viz is a growing skill)
- Propose phased commitment so it feels low-risk
- Offer engineering help with their current design system tech debt
- Include his designer in architecture discussions so design isn't an afterthought

---

#### Jennifer - Data Team Lead
**Role:** Owns data pipeline team (4 engineers), responsible for all data infrastructure  
**Interest Level:** Low currently (burned by past experience)  
**Influence Level:** Medium — her team owns the pipelines we need to integrate with  
**Current Stance:** Resistant — the recommendation engine project left a bad taste  
**Motivations:**
- Team autonomy and respect
- Clean data architecture (hates when other teams create shadow pipelines)
- Recognition for Data team's contribution to product success
- Avoiding being blamed when integration is complex

**Concerns:**
- Being treated as a "service team" rather than partners
- Engineering making pipeline decisions without consulting Data
- Repeating the blame dynamic from the recommendation engine project
- Being committed to timelines she didn't help estimate

**History:**
During the recommendation engine project (~6 months ago), there were integration delays. In the post-mortem, engineering framing put most blame on data pipeline readiness, but the real issue was unclear interface contracts and changing requirements. Jennifer's team felt thrown under the bus in front of leadership. No one properly acknowledged this.

**Preferred Communication:** Direct and honest. Respects technical depth. Doesn't want corporate-speak or empty promises.

**Engagement Strategy:**
- Acknowledge the past directly — take responsibility for engineering's part
- Include Data team in design/architecture from day one
- Establish clear interface contracts early with both teams signing off
- Share credit visibly in status updates and demos
- Let her team have ownership of the data pipeline architecture decisions

---

#### David - Operations Manager
**Role:** Manages infrastructure, deployment, and on-call for production systems  
**Interest Level:** Low — doesn't see this as his priority yet  
**Influence Level:** Medium — controls infrastructure provisioning and on-call staffing  
**Current Stance:** Neutral bordering on resistant — worried about operational burden  
**Motivations:**
- System stability and uptime (his team is measured on this)
- Manageable on-call load (they're already stretched)
- Clear ownership boundaries
- Not inheriting poorly built systems to maintain

**Concerns:**
- Real-time systems are complex to operate
- His team isn't staffed for another high-priority service
- Being expected to support something they had no input on designing
- Alert fatigue from yet another service

**Preferred Communication:** Structured, with clear asks. Values being included in operational design decisions early. Likes documentation.

**Engagement Strategy:**
- Involve Ops in architecture decisions specifically around operability
- Design for operability from the start — make this a selling point
- Offer to handle initial on-call rotation with engineering team
- Create clear runbooks before handoff
- Show him the operational design upfront to get input, not after-the-fact

---

#### Richard - Finance Director
**Role:** Approves project budgets above $50K  
**Interest Level:** Low  
**Influence Level:** High — can block or delay the project with budget holds  
**Current Stance:** Questioning ROI — asking hard questions about cloud costs  
**Motivations:**
- Clear ROI and payback period
- Cost predictability (hates runaway cloud bills)
- Alignment with company strategic priorities
- Governance and accountability

**Concerns:**
- Cloud infrastructure costs for real-time processing could be significant
- Past projects that went over budget without early warning
- Whether this duplicates existing BI tool capabilities

**Preferred Communication:** Formal presentations with numbers. Quarterly review format. Wants executive summary, not technical details.

**Engagement Strategy:**
- Build ROI case with concrete numbers (customer retention, revenue impact)
- Show cost projections with scenarios (low/medium/high usage)
- Reference existing customer requests and potential revenue at risk
- Get Sarah's support to co-present (business + tech alignment)
- Propose phase-gated budget approval (not all money upfront)

---

#### Priya - VP Engineering (my skip-level)
**Role:** My VP, overall engineering sponsor  
**Interest Level:** High  
**Influence Level:** High  
**Current Stance:** Supportive — championed this project in leadership  
**Motivations:**
- Demonstrating engineering can lead strategic initiatives
- Cross-functional collaboration improvement (mentioned in her OKRs)
- Building tech lead bench strength
- Platform thinking over point solutions

**Concerns:**
- Project becoming a political mess
- Underestimating complexity
- Cross-team conflicts reflecting poorly on engineering

**Engagement Strategy:**
- Bi-weekly updates, flag risks early
- Ask for coaching on tricky stakeholder situations
- Keep her informed enough to protect us politically if needed
- Don't escalate prematurely — handle what I can first

---

## Stakeholder Map

### Power/Interest Grid

```
                    Low Interest              High Interest
                ┌────────────────────────┬────────────────────────┐
                │                        │                        │
                │    KEEP SATISFIED      │    MANAGE CLOSELY      │
                │                        │                        │
  High Power    │  • Richard (Finance)   │  • Sarah (VP Product)  │
                │  • CTO                 │  • Priya (VP Eng)      │
                │                        │  • Mike (Design Dir)*  │
                │                        │                        │
                ├────────────────────────┼────────────────────────┤
                │                        │                        │
                │    MONITOR             │    KEEP INFORMED       │
                │                        │                        │
  Low Power     │  • Legal/Compliance    │  • Jennifer (Data)     │
                │  • Other team leads    │  • David (Ops)         │
                │  • Marketing           │  • Product Managers    │
                │                        │  • Individual devs     │
                │                        │                        │
                └────────────────────────┴────────────────────────┘
```

*Mike sits on the boundary — his power is high for this project because he controls the design resource we need, but his interest is only medium. If I can increase his interest, he moves firmly into "Manage Closely."

### Key Insight
Jennifer and David are in "Keep Informed" but their actual blocking power is higher than this grid suggests. They can't kill the project politically, but they can slow it down operationally. I'm treating them as higher priority than the grid alone would suggest.

---

## Relationship Map

```
                         ┌─────────────┐
                         │   Priya     │
                         │  (VP Eng)   │
                         │  SPONSOR    │
                         └──────┬──────┘
                                │ supports
                                ▼
               ┌─────────────────────────────────┐
               │           ME (Tech Lead)        │
               └──┬──────────┬──────────┬────────┘
                  │          │          │
         ally     │   need to│win    neutral
                  │          │          │
           ┌──────▼───┐  ┌───▼────┐  ┌──▼───────┐
           │  Sarah   │  │  Mike  │  │  David   │
           │(VP Prod) │  │(Design)│  │  (Ops)   │
           └──────┬───┘  └────────┘  └──────────┘
                  │
                  │ has influence over
                  ▼
           ┌──────────┐       ┌──────────┐
           │ Richard  │       │ Jennifer │
           │(Finance) │       │  (Data)  │
           └──────────┘       └──────────┘
                               ▲
                               │ past conflict (unresolved)
                               │
                         ┌─────┴──────┐
                         │Engineering │
                         │  (my team) │
                         └────────────┘
```

### Relationship Dynamics
- **Sarah → Me:** Strong working relationship, she trusts my technical judgment. I need to maintain this by delivering early wins.
- **Jennifer → Engineering:** Damaged trust. This is my biggest relationship risk. If I don't repair this, integration will be painful and slow.
- **Mike → Me:** Cordial but distant. He doesn't know me well enough to prioritize my asks over others.
- **David → Me:** Professional but transactional. He'll cooperate if I make it easy for him.
- **Sarah → Richard:** She can influence his budget decision if I arm her with the right data.

---

## Hidden Stakeholders

People who might not be obvious but could block or derail:

| Stakeholder | Why They Matter | Risk if Missed |
|-------------|----------------|----------------|
| Security team | Real-time data has PII implications | Late-stage security review blocks launch |
| Senior engineer on Data team | Technically influential, may resist | Passive resistance slows integration |
| Customer Success | They'll field questions about the feature | Poor rollout if they're not prepared |
| DevEx/Platform team | May have opinions on streaming infrastructure choices | Could push back on tech stack decisions |

---

## Engagement Plan

| Stakeholder | Priority | Next Action | Timeline | Success Indicator |
|-------------|----------|-------------|----------|-------------------|
| Sarah (VP Product) | Critical | Align on MVP scope | This week | Written scope agreement |
| Jennifer (Data) | Critical | 1:1 to address past, propose partnership | This week | She agrees to meet again |
| Mike (Design) | High | Coffee chat, understand his world | This week | He's open to discussion |
| Priya (VP Eng) | High | Brief on my stakeholder approach | Week 1 | She gives coaching input |
| David (Ops) | Medium | Include in architecture kickoff | Week 2 | He attends and gives input |
| Richard (Finance) | Medium | Prepare ROI case with Sarah | Week 2-3 | Meeting scheduled |
| Security | Medium | Early consultation on data handling | Week 2 | No surprises later |

---

## Stakeholder Communication Matrix

| Stakeholder | Format | Frequency | Content Focus |
|-------------|--------|-----------|---------------|
| Sarah | 1:1 + async Slack | Weekly | Progress, decisions needed, risks |
| Mike | Informal + email | Bi-weekly | Design needs, collaboration wins |
| Jennifer | 1:1 video call | Weekly during ramp | Partnership health, integration progress |
| David | Planning invite + docs | Bi-weekly | Operational design, ask for input |
| Richard | Formal presentation | Monthly | Budget tracking, ROI progress |
| Priya | 1:1 (existing) | Bi-weekly | Strategic risks, coaching |

---

## Reflection

The biggest lesson from mapping this out: my natural instinct as an engineer is to focus on the people I already have good relationships with (Sarah, Priya) and avoid the uncomfortable ones (Jennifer, Mike). But the project's success depends more on the relationships that need repair than the ones that are already working. I need to front-load the hard conversations.

Also, I initially underestimated David's importance. Ops can't kill the project politically, but operationally they can make it painful if they're not invested. Better to treat them as partners than as a team that "just needs to provision some infrastructure."
