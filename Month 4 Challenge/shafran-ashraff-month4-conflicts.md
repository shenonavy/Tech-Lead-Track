# Conflict Resolution Playbook

## Personal Assessment

Before getting into frameworks, I need to be honest about my own patterns. Self-awareness is the foundation here.

**My Default Conflict Style:** Avoiding → Competing

When conflict arises, my first instinct is to avoid it. I'll hope it resolves itself, focus on technical work instead, or reframe it as "not that big a deal." But when avoidance stops working and the issue forces itself, I can swing to competing — getting defensive, over-relying on being technically right, and pushing my position harder than necessary.

**My Triggers:**
- Being blindsided in meetings (someone raises a problem they never mentioned privately)
- Feeling like my technical judgment is being dismissed without engagement
- When people are passive-aggressive instead of direct
- Scope creep disguised as "small asks" that accumulate
- When someone takes credit for shared work

**My Blind Spots:**
- I sometimes mistake silence for agreement — not everyone pushes back verbally
- I can be too focused on being "right" technically when the real issue is about relationships or feelings
- I tend to over-prepare arguments instead of genuinely listening first
- I sometimes miss that someone's resistance is about a past hurt, not the current issue

**My Escalation Criteria (when to bring in my manager):**
- The conflict is affecting delivery timelines and we've tried resolving directly
- There's a power imbalance that makes direct resolution unfair
- The other person refuses to engage in good faith
- It involves ethical concerns or policy violations
- Two attempts at direct resolution have failed

---

## Conflict Type 1: Priority Disagreement (Engineering vs Product)

### Scenario

Product wants Feature A (customer-facing real-time alerts) shipped in 2 weeks because an enterprise client renewal depends on it. Engineering believes Feature B (event processing reliability layer) is a prerequisite — without it, alerts will be unreliable and generate false positives. Feature B takes 4 weeks minimum.

### Why This is Hard

Both sides are right from their perspective. Product is responding to real business pressure. Engineering is protecting system integrity. The classic tension: ship fast vs. ship right.

### Resolution Framework

**Step 1: Understand Both Positions Fully**

Don't jump to solutions. First make sure I actually understand the full picture.

- *Product perspective:* Client X is a $200K/year account. Their renewal is in 6 weeks. The champion at Client X specifically asked for real-time alerts in the last QBR. Without this, CSM says there's renewal risk.
- *Engineering perspective:* The event processing layer currently drops ~3% of events under load. If we build alerts on top of this, customers will get false positives or miss critical alerts. This erodes trust worse than not having the feature.

**Step 2: Identify Common Ground**

Both sides want:
- Customer X to renew
- A product that works reliably
- Not to create more problems by rushing

Both sides are constrained by:
- Time (6 weeks to renewal)
- Resources (fixed team size)
- Quality expectations

**Step 3: Generate Options Together**

Don't come in with THE answer. Come with options and evaluate together.

| # | Option | Pros | Cons |
|---|--------|------|------|
| 1 | Feature B first, then A (6 weeks total) | Reliable, proper architecture | Tight for renewal, no margin |
| 2 | Feature A only, accept risk (2 weeks) | Fast, meets immediate ask | Unreliable alerts damage trust |
| 3 | Minimal B (reliability for alerts path only) + A (4 weeks total) | Good enough reliability, faster than full B | Some tech debt, doesn't cover all future use cases |
| 4 | Feature A with caveats (2 weeks) + B in parallel | Client gets something quickly | Alert with known limitations, needs client communication |
| 5 | Negotiate timeline with client (buy 2 more weeks) | Proper solution, no shortcuts | May not be possible, CSM risk |

**Step 4: Evaluate Together with Data**

Bring this to a joint discussion with Product. My recommendation is Option 3, but I present all options with trade-offs and let us decide together.

"Here's how I see the trade-offs. Option 3 gets us to a reliable alert system in 4 weeks — that's 2 weeks before renewal. It means we take on some tech debt for the broader event processing layer, but the alerts path specifically will be solid. I think this balances speed and quality. What do you think? Am I missing something about the client's timeline?"

**Step 5: Commit and Follow Through**

Once we agree, commit fully. Don't relitigate. If the decision was Option 3:
- Immediately break down the 4-week plan
- Identify what specifically is "minimal B" and get engineering sign-off on it being actually reliable
- Set up a midpoint check at week 2 to confirm we're on track
- Communicate the plan to the client team so they can manage expectations

### Key Principle

The goal is not to "win" the argument. The goal is a decision that serves the business and that both sides can commit to. If Product feels steamrolled, they'll route around me next time. If I feel steamrolled, I'll lose trust in the partnership.

---

## Conflict Type 2: Resource Competition with Another Tech Lead

### Scenario

Raj, another tech lead, needs Alex (a senior backend engineer with streaming expertise) for his critical payment processing project. I also need Alex for the real-time analytics pipeline. Both projects are high-priority. There's only one Alex.

### Why This is Hard

This is textbook zero-sum unless we can find creative solutions. Both projects are legitimate priorities. Going to management to decide often means neither person gets what they want, and the relationship between tech leads gets damaged.

### Resolution Framework

**Step 1: Don't Let It Become Personal**

Internal reframe: This isn't "Raj vs. me." This is "two important projects competing for a scarce resource." We're both trying to do right by our teams and the company.

**Step 2: Have the Direct Conversation First**

Don't go to management before talking to Raj. That's an escalation that damages trust.

"Raj, I realize we both need Alex for the next few weeks. Rather than putting this on our managers to figure out, can we talk through it and see if there's a solution that works for both of us?"

**Step 3: Understand Their Situation Genuinely**

Questions to ask Raj:
- What specifically does he need Alex for? (Maybe it's not the whole person, just their expertise)
- What's his timeline pressure? Is it the same as mine or different?
- Are there alternatives for his project? (Other engineers who could be ramped up?)
- What happens if he doesn't have Alex? How bad is it?

Share my situation honestly too. Don't exaggerate my need.

**Step 4: Explore Creative Solutions**

| Solution | How It Works | When It Works |
|----------|-------------|---------------|
| Time-split | Alex does 60/40 or 3 days/2 days | When both projects can absorb the slowdown |
| Sequential | One project gets Alex first, then the other | When timelines can be staggered by 2-3 weeks |
| Knowledge transfer | Alex ramps up someone else for one project | When Alex's value is expertise, not just capacity |
| Scope adjustment | Reduce one project's scope to need fewer specialized skills | When scope is flexible |
| Temporary contractor | Bring in external help for the less specialized parts | When budget allows and ramp-up is fast |

**Step 5: Propose a Specific Solution**

"What if Alex spends weeks 1-3 setting up the streaming architecture for analytics (that's the part where we really need his specific expertise), and then transitions to your payment project for weeks 4-6? In the meantime, I can have Pradeep shadow Alex during weeks 1-3 so she can continue the work after he moves. Does that timeline work with your payment delivery date?"

**Step 6: If We Can't Agree — Escalate Constructively**

If direct conversation doesn't resolve it:
- Go to our shared manager together (not separately)
- Present the problem jointly with options we've already discussed
- Make clear this isn't a complaint about each other — it's a prioritization decision
- Accept the decision once made

**What NOT to Do:**
- Don't go above Raj's head without telling him
- Don't try to "claim" Alex by assigning work first
- Don't bad-mouth Raj's project to make yours seem more important
- Don't make it about seniority or who asked first

---

## Conflict Type 3: Past Grudge Affecting Current Work

### Scenario

Jennifer (Data Team Lead) is resistant to collaborating on the analytics platform because engineering blamed her team during the last project. Her responses are delayed, her engineers push back on reasonable requests, and she avoids joint planning meetings.

### Why This is Hard

The current conflict isn't really about the current project. It's about unresolved hurt from the past. Addressing only the symptoms (slow responses, pushback) without addressing the root cause (broken trust) means the problem will keep recurring.

### Resolution Framework

**Step 1: Name It Directly**

Don't pretend everything is fine. Don't try to work around the tension. Address it head-on, but with empathy and ownership.

"Jennifer, I want to be direct. I feel like there's some hesitation about working together on this project, and I think I understand why. The recommendation engine project didn't end well for your team, and I don't think engineering handled the aftermath fairly."

**Step 2: Listen Without Defending**

This is the hardest part. When she explains her frustration:
- Don't interrupt
- Don't explain why it happened
- Don't justify or minimize
- Don't say "but" after acknowledging her point
- Just listen and reflect back what you hear

"It sounds like your team felt blamed for something that was a shared failure, and that nobody from our side acknowledged that publicly. That would make me hesitant too."

**Step 3: Take Responsibility**

Be specific about what engineering did wrong:
- "We didn't communicate requirement changes that affected your timelines"
- "When the post-mortem framing blamed Data, I (or we) should have corrected it"
- "We didn't treat your team as equal partners"

Don't over-apologize or be dramatic. Be matter-of-fact and sincere.

**Step 4: Ask What She Needs**

"What would need to be different this time for you to feel good about collaborating?"

Let her set some of the terms. She might say:
- "I need to be in the room when timelines are set"
- "I need engineering to own their side publicly when things slip"
- "I need clear interface contracts before we start building"

These are reasonable requests. Agree to them specifically.

**Step 5: Demonstrate Changed Behavior Consistently**

Words don't rebuild trust. Actions do, over time.

| Commitment | How I'll Demonstrate |
|------------|---------------------|
| Include Data early | Invite Jennifer to architecture kickoff, share designs in draft |
| Share credit publicly | In every status update, name Data team contributions |
| Own our failures | If engineering causes a delay, say so explicitly in standup |
| Respect their expertise | Ask for their input on pipeline design, don't prescribe |
| Give buffer | Build 20% timeline buffer for integration points |

**Step 6: Create Accountability**

"I know words are easy and actions are what matter. How about we check in on how the collaboration feels after 2 weeks? If I'm falling into old patterns, I genuinely want you to tell me directly."

---

## Conflict Type 4: Architectural Disagreement Within Team

### Scenario

Two senior engineers on my team disagree on whether to use Kafka Streams or Apache Flink for the real-time processing layer. Both have valid technical arguments. The disagreement is creating tension and blocking progress.

### Resolution Framework

**Step 1: Separate the Technical from the Personal**

Check: is this really about technology, or is it about ego, recognition, or influence? Often "architectural disagreements" are actually about who gets to shape the system.

**Step 2: Create Fair Evaluation Criteria (Before Evaluating)**

Define success criteria before looking at solutions. Get both parties to agree on what matters:
- Throughput requirements (events per second)
- Operational complexity (team expertise, debugging, monitoring)
- Latency requirements
- Ecosystem fit (what we already run)
- Team familiarity and ramp-up time

**Step 3: Evidence-Based Evaluation**

"Let's both build a small proof-of-concept over 2 days against our actual use case, and evaluate against the criteria we agreed on."

This removes opinion and replaces it with evidence. It also gives both people a fair shot.

**Step 4: Make the Decision Clearly**

After evaluation, make a clear decision and explain the reasoning. Thank both parties for their input. Explicitly acknowledge the strengths of the approach we didn't choose.

"We're going with Flink based on the latency benchmarks. But Amir's point about operational complexity is valid — we're going to invest in proper monitoring from day one to mitigate that."

**Step 5: Commit as a Team**

Once decided, everyone commits. No "I told you so" if the chosen approach hits issues. No passive undermining.

---

## De-escalation Techniques

### When a Conversation Gets Heated

These are my go-to moves when I feel (or see) emotions rising:

**1. Pause and Breathe**
"Let's take 10 minutes. I want to think about what you said before I respond."

This isn't weakness. It's preventing damage. Nothing good comes from responding reactively.

**2. Name the Dynamic**
"I notice we're both getting frustrated. I think it's because we both care about this. Can we step back and figure out what we're actually disagreeing about?"

Naming what's happening often defuses it.

**3. Move the Venue**
"This is getting complex. Want to grab coffee and continue? I think better away from a screen."

Physical movement and change of context can reset the emotional temperature.

**4. Summarize and Check**
"Let me make sure I understand your position: [summary]. Did I get that right?"

People feel less combative when they feel heard. Often escalation comes from feeling unheard, not from the actual disagreement.

**5. Find the 5% Agreement**
"I think we actually agree on [X]. Where we differ is [Y]. Can we focus on Y specifically?"

Narrowing the disagreement makes it more manageable.

**6. Bring in a Neutral Third Party**
"I think we could use a fresh perspective. Would you be open to having [name] help us think through this?"

Not an escalation — a facilitation request. Choose someone both parties respect.

### Warning Signs I Watch For

| Signal | What It Means | My Response |
|--------|---------------|-------------|
| Repeating the same point louder | They don't feel heard | Stop arguing, actively listen and summarize back |
| Arms crossed, leaning back | Defensive posture, emotionally withdrawing | Ask an open question, create safety |
| "Fine, whatever" | Giving up, not agreeing — resentment building | Don't accept this. "I don't want you to just agree — tell me what's not working" |
| Personal attacks ("you always...") | Issue has become personal, trust is damaged | Name it: "Let's keep this about the problem, not each other" |
| Going silent in a group setting | Power dynamic making them uncomfortable | Follow up 1:1 afterward |
| CC'ing managers on emails | Trust broken, looking for cover | Have a direct conversation about what's wrong |

---

## My Conflict Resolution Commitments

Things I'm going to practice deliberately:

1. **Address conflict within 48 hours.** My avoidance tendency means I let things fester. New rule: if something bothers me for more than a day, I address it directly.

2. **Lead with curiosity, not conclusions.** Instead of "you did X wrong," start with "help me understand what happened with X."

3. **Separate intent from impact.** Someone might not have intended harm, but the impact was real. Acknowledge impact without assuming intent.

4. **Check my assumptions.** Before responding to perceived slights, verify. "When you said X in the meeting, I interpreted it as Y. Was that what you meant?"

5. **Make it safe.** People won't be honest if they fear retribution. Create an environment where raising problems is welcome.

---

## Quick Reference Card

```
BEFORE engaging in conflict:
  □ Am I emotionally regulated? (If not, wait)
  □ What's the actual issue? (Not the symptom)
  □ What's my goal? (Resolution, not winning)
  □ Which approach fits? (Collaborate/Compromise/Accommodate/Compete/Avoid)

DURING conflict:
  □ Listen first, talk second
  □ Summarize their position before sharing mine
  □ Look for common ground
  □ Generate options together
  □ Check emotional temperature — de-escalate if needed

AFTER resolution:
  □ Document the agreement
  □ Follow through on commitments
  □ Check in later on how it's going
  □ Reflect: what would I do differently?
```
