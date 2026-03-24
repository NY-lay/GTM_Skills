---
name: marketing-plan
description: Conducts a structured marketing interview based on Allan Dib's 1-Page Marketing Plan framework and generates a comprehensive marketing_plan.md file. This file serves as the strategic foundation for all AI CMO agents — it defines the ICP, positioning, message, competitive landscape, channel strategy, and goals. Run this skill to create or refresh the marketing plan. Use /marketing-plan to start.
allowed-tools: Read, Write, AskUserQuestion
user-invocable: true
---

# Marketing Plan Interview Skill

Conduct a structured interview and generate `marketing_plan.md` — the strategic foundation for all AI CMO agents.

## Overview

This skill interviews you across the 9 squares of Allan Dib's 1-Page Marketing Plan, organized into three phases (Before, During, After). It produces `marketing_plan.md` — a single file that all agents read at startup to understand who to target, how to position, and what to say.

**The output file is the single source of truth for:**
- ICP scoring (research agent — who scores high vs. low)
- Personalization (email/DM agent — what to say and why)
- Content (content writer — what topics resonate with the ICP)
- Competitive context (why we win vs. alternatives)

**This skill challenges your answers.** Vague answers produce vague agent outputs. The skill uses Dib's own quality standards — derived from his book's good vs. bad examples — to push back when answers are weak and help you arrive at sharper answers before the plan is written.

## Quick Start

```
/marketing-plan
```

You will be interviewed through 4 phases. Answer as specifically as you can. Expect to be challenged on weak answers — that's by design.

**Estimated time**: 30–60 minutes (longer than without challenge mode, but the output is worth it).

**Output**: `marketing_plan.md` saved to the current working directory.

---

## Quality Standards Reference

This section defines what "weak" vs. "strong" looks like for every critical answer category. These are Dib's own contrasts from the book. The skill uses these standards to score answers at each phase gate and the final pre-flight check.

### Target Market / ICP

| Weak | Strong |
|------|--------|
| "Everyone" | "Post-natal women in the UK seeking cellulite treatment" |
| "Small businesses" | "B2B SaaS founders at Series A–B (50-200 employees) who just hired a VP Sales" |
| "Mid-market companies" | Specific title + company stage + industry + geography |
| "Anyone who needs our product" | One specific type of person you could find on LinkedIn and immediately know they're a fit |

**The test:** Could you find your ICP on LinkedIn right now using filters alone? If not, the definition is too vague.

### USP / Positioning

| Weak | Strong |
|------|--------|
| "Best quality" | Specific, quantifiable differentiator ("only X that guarantees Y in Z days") |
| "Great service" | Forces an apples-to-oranges comparison — they can't compare you to competitors on price |
| "Experienced team" | Names the unique mechanism — method, process, or technology competitors don't have |
| "We care about customers" | Prospects learn this after buying — useless as a pre-purchase differentiator |

**The test:** If you removed your name and logo, would anyone know it was you — or could it be any company in your industry?

**Banned words in a USP:** quality, service, best, experienced, trusted, leading, premier, dedicated, passionate.

### Elevator Pitch

| Weak | Strong |
|------|--------|
| Job title or abstract description ("I'm a senior growth consultant") | "You know how [specific problem]? Well, what we do is [solution]. In fact, [specific proof]." |
| Product-first ("We provide cloud-based analytics") | Problem-first (names the pain before the solution) |
| Generic ("We help companies grow") | Specific outcome + proof point in under 30 seconds |

**The formula (mandatory):** "You know how [frustrating problem]? Well, what we do is [solution]. In fact, [quantified proof]."

### ICP Psychographics

| Weak | Strong |
|------|--------|
| "They want to grow revenue" | "They lie awake worrying that their biggest competitor will close a deal they didn't even know was happening" |
| "They're frustrated with their tools" | "They feel stupid in front of their board because they can't explain why pipeline velocity dropped last quarter" |
| "They want to be efficient" | Names a specific emotion (fear, anger, desire, embarrassment) with a concrete situation |
| "They need better data" | Describes the moment of pain — what's happening when it hurts most |

**The test:** Could you use this psychographic answer verbatim in an email subject line that would make the recipient say "that's exactly how I feel"?

### Advertising / Lead Magnet

| Weak | Strong |
|------|--------|
| "Contact us for a free consultation" | "Free report: The 7 costly mistakes companies make when choosing a [product category] — and how to avoid them" |
| Generic call to action | Attracts only the ICP — self-selecting by the specificity of the problem it names |
| "Request a demo" | Offers genuine value before asking for anything in return |

**The test:** Would someone who is NOT your ICP request this? If yes, it's too generic.

### Offer / Guarantee

| Weak | Strong |
|------|--------|
| "Satisfaction guaranteed" | "We guarantee [specific outcome] or we'll [specific consequence]. If you aren't delighted, we insist you tell us and we'll [double your money back / redo it for free / etc.]" |
| "Money back guarantee" | Names the three specific fears of the prospect and reverses each one |
| No guarantee mentioned | The guarantee specifically addresses what the prospect is most afraid of about buying |

### Channel Selection

| Weak | Strong |
|------|--------|
| "Social media" | Named platforms with evidence: "LinkedIn — our ICP titles are there and I've booked 3 meetings via LinkedIn DMs" |
| "Content marketing" | Named communities, newsletters, subreddits, Slack groups, or events the ICP actually attends |
| "Email and LinkedIn" | Each channel has a reason and a watering hole: "LinkedIn Sales Navigator + [specific group]" |

### Emotional Resonance in Copy

| Weak | Strong |
|------|--------|
| Features list | Pain identification — "selling the cure, not the prevention" |
| "This tool has X features" | "You know how [specific painful thing]? Imagine if [desired outcome] instead." |
| Technically correct but bland | Pushes at least one of the 5 motivators: fear, love, greed, guilt, pride |

---

## Interview Phases

### Phase 0: Business Foundation

Ask these questions:

1. **What does your product/service do?** Describe it in plain language — what problem does it solve and for whom?
2. **What stage is the business at?** (Pre-revenue / first customers / scaling / established)
3. **What is your primary goal for the next 6–12 months?** Be specific — a number is better than a direction.
4. **What does a typical deal look like?** (price point, sales cycle length, contract type)
5. **Who are your current best customers, if any?** Name 2–3 and describe why they're the best.

---

#### Phase 0 Challenge Protocol

**Watch for these failure modes:**

| Answer pattern | Challenge |
|---|---|
| Product description uses technical jargon or is abstract | "Can you say that as if you were explaining it to someone at a party? Try the formula: 'You know how [problem]? Well, what we do is [solution]. In fact, [proof].'" |
| Goal is directional ("grow revenue", "get more customers") | "What specific number would make this year a success? Give me a revenue number, a customer count, or a meeting target." |
| Stage is "pre-revenue" but they describe a fully built product | Probe: "What's the real blocker — is this a market discovery problem or a go-to-market problem?" |
| "Best customers" description is vague ("they pay well") | "What specifically makes them great? Title, company type, what they actually said about working with you?" |

**Minimum bar before proceeding to Phase 1:**
- Product description passes the "party test" — a non-expert could repeat it
- Goal has at least one measurable number
- Best customer description is specific enough to find a similar person on LinkedIn

---

### Phase 1: The "Before" Phase — Prospects

#### Square 1: Target Market

**Goal**: Identify the specific niche and build a detailed ICP profile.

**Step 1 — PVP Index** (run if serving multiple segments or unsure which to focus on)

Present this table and ask PG to score each segment out of 10:

| Segment | Personal Fulfillment (1-10) | Value to Marketplace (1-10) | Profitability (1-10) | Total |
|---|---|---|---|---|
| [Segment A] | | | | |
| [Segment B] | | | | |

- **Personal Fulfillment**: How much do you enjoy working with this type of customer?
- **Value to Marketplace**: How much do they value your work? Willing to pay well?
- **Profitability**: How profitable is the work for this segment?

Highest total = primary target. Explain why this matters: "A 100-watt light bulb lights a room. A 100-watt laser cuts through steel. Same energy, very different result. Niching is the laser."

**Step 2 — ICP Demographic Deep Dive**

- What is the typical job title / role of your buyer?
- What company size (employees, revenue) are they at?
- What industry or industries?
- What geography?
- Seniority level (founder, VP, C-suite)?

**Step 3 — ICP Psychographic Deep Dive** (these feed the personalization agent — don't skip or rush these)

Ask all 8:
1. What keeps your ideal customer awake at night — the specific business problem that gnaws at them?
2. What are they afraid of? (Risk of failure, looking bad, losing their job, stagnating?)
3. What are they angry or frustrated about in their current situation or with current vendors?
4. What trends in their industry are they worried about or excited by?
5. What do they secretly want most? What would a win look like for them personally?
6. What does their day-to-day look like — where do they spend most of their time?
7. What is the dominant emotion they feel about the problem your product solves?
8. What is the ONE thing they would pay almost anything to have solved?

**Buying behavior:**
- Where do they research vendors?
- Who else is involved in the buying decision?
- What objections do they most often raise?

**Trigger events (critical for ICP scoring and outreach timing):**
- What specific events trigger the need for your product? (funding round, new hire, product launch, etc.)
- What signals visible from the outside suggest they are in buying mode?

---

#### Square 1 Challenge Protocol

**Watch for these failure modes:**

| Answer pattern | Challenge |
|---|---|
| Target market includes "anyone who needs X" or a broad category | "If I had a LinkedIn Sales Navigator account right now and wanted to find your ideal customer, what filters would I use? Give me title, company size, and industry." |
| Psychographic answers describe outcomes ("they want to grow") not emotions | "What does your ICP feel on a Tuesday morning when this problem is at its worst? Describe the emotion and the specific moment." |
| "What keeps them up at night" answer is generic ("they want to hit their numbers") | "Every VP wants to hit their numbers. What specific thing about your product's problem category is the gnawing fear — the thing they don't want to admit to their boss or board?" |
| Trigger event is internal and invisible ("when they decide to buy") | "What would I see on LinkedIn, in a press release, or in a job posting that would tell me this company needs you right now?" |
| ICP is "mid-market" or "enterprise" without specification | "Mid-market means 50-1,000 employees to some people and $50M-$500M revenue to others. Which is it — and which part of that range do you actually win in?" |

**Scoring criteria for Phase 1 Gate:**

| Answer | Green criteria |
|---|---|
| Target market definition | Could filter for this person on LinkedIn using title + company size + industry |
| Psychographic answers | At least 3 of the 8 questions answered with an emotion + specific situation (not just "they want X") |
| Trigger events | At least 1 event with a visible external signal (not just "when they need us") |
| Buying behavior | Objections are specific enough to address in a cold email |

---

#### Square 2: Crafting Your Message

**Goal**: Define the USP and core message used across all outreach.

1. **The two USP questions:**
   - Why should a prospect buy your type of solution at all? (Compelling reason to act — what's the cost of doing nothing?)
   - Why should they buy from you specifically rather than your nearest competitor?

2. **Unique mechanism:** What is the specific thing you do or have that competitors don't — a methodology, technology, process, or guarantee?

3. **Positioning test:** If someone removed your name and logo from your website, would it be identifiable as you — or could it be any company in your space?

4. **The result, not the feature:** What does their business/life look like after they buy? Not the product — the transformation.

5. **Elevator pitch:** Fill in this formula:
   > "You know how [describe the frustrating problem]? Well, what we do is [solution]. In fact, [specific proof point]."

6. **Competitors:** List 2–4 direct competitors. For each: how are they positioned? Where do you clearly win? Where do they sometimes beat you?

7. **Social proof:** What proof points do you have? (Specific metrics, case studies, notable customers, press)

---

#### Square 2 Challenge Protocol

**Watch for these failure modes:**

| Answer pattern | Challenge |
|---|---|
| USP contains: quality, service, best, experienced, trusted, leading, premier | "Those words are the default for every competitor in your space too. Remove them and tell me specifically: what can you do that they can't, or what do you guarantee that they don't?" |
| "We have better customer service" | "Prospects can't experience your customer service until after they buy. What can you show them before they buy that's different? What's in your offer or your process that's verifiably distinct?" |
| Competitors section: "We don't really have direct competitors" | "What does a prospect do today when they don't use you? Even if no one sells the exact same thing, there's always an alternative — spreadsheets, a different approach, doing nothing. Name those and tell me why you win." |
| Elevator pitch is product-first, not problem-first | "Try again: start with the frustrating problem, not your product. The prospect shouldn't hear your company name until the third sentence." |
| "We help companies grow" or abstract outcome | "What specific metric improves, by how much, in what timeframe? 'In fact, [proof]' needs a number or a named customer." |
| Social proof: "We have happy customers" | "Name one. What did they achieve specifically — in numbers — because of you?" |

**Scoring criteria for Phase 1 Gate (Square 2):**

| Answer | Green criteria |
|---|---|
| USP | Contains zero banned words; makes a specific claim that forces apples-to-oranges comparison |
| Elevator pitch | Follows problem → solution → proof formula; proof contains a number or named example |
| Competitors | At least 2 named with specific win/loss conditions |
| Social proof | At least one specific metric, case study reference, or named customer |

---

#### Square 3: Advertising Media / Channels

**Goal**: Identify which channels to prioritize and name specific watering holes.

1. Where does your ICP actually spend time? (LinkedIn, specific Slack communities, industry conferences, newsletters, subreddits?)
2. Where have you had success reaching them before — even anecdotally?
3. What channels are you willing to invest in?
4. What topics would your ICP find genuinely valuable to read — educational, not product pitches?
5. Is there a "watering hole" — one place where a large concentration of your ICP gathers?

---

#### Square 3 Challenge Protocol

**Watch for these failure modes:**

| Answer pattern | Challenge |
|---|---|
| "Social media" | "Which platform specifically? And why — do you know your ICP is active there, or are you guessing?" |
| "Content marketing" | "That's a tactic, not a channel. Where will the content be published, who will see it, and how do you know they're there?" |
| "LinkedIn and email" | "Good start. Now: which LinkedIn groups or communities? Which types of email lists? What conferences does your ICP attend?" |
| Content topics are product-adjacent ("why our category matters") | "Your ICP isn't searching for reasons to buy your category. What problem do they Google at 11pm that has nothing to do with you — and what would a useful answer look like?" |

**Scoring criteria for Phase 1 Gate (Square 3):**

| Answer | Green criteria |
|---|---|
| Channel selection | At least 2 channels named with specific reasons tied to ICP behavior |
| Watering holes | At least 1 specific community, newsletter, event, or platform named |
| Content topics | At least 2 topics that provide genuine ICP value without pitching the product |

---

### Phase 1 Validation Gate

**Run this gate before proceeding to Phase 2.**

Present a summary table:

```
Phase 1 Quality Check

| Answer area | Score | Issue |
|---|---|---|
| Target market specificity | 🟢/🟡/🔴 | [if not green] |
| Psychographic depth | 🟢/🟡/🔴 | [if not green] |
| Trigger events | 🟢/🟡/🔴 | [if not green] |
| USP / no banned words | 🟢/🟡/🔴 | [if not green] |
| Elevator pitch formula | 🟢/🟡/🔴 | [if not green] |
| Competitors named | 🟢/🟡/🔴 | [if not green] |
| Social proof | 🟢/🟡/🔴 | [if not green] |
| Channel specificity | 🟢/🟡/🔴 | [if not green] |
```

**If any Red:** "Before we move on, let's work on [topic]. [Use the specific challenge question from the Challenge Protocol above.] I won't be able to generate a useful marketing plan without this being sharper."

**Do not proceed to Phase 2 until all items are Green or Yellow.**

---

### Phase 2: The "During" Phase — Leads

#### Square 4: Lead Capture

1. How do you currently capture inbound leads?
2. Do you have a lead magnet or ethical bribe? If not — what would be most valuable to your ICP?
3. Where does lead information currently live?

#### Square 5: Lead Nurturing

1. Do you have a newsletter or regular touchpoint with leads who aren't ready to buy?
2. What is your follow-up cadence after initial interest?
3. What content would be most useful to prospects in research mode?

#### Square 6: Sales Conversion

1. What does your sales process look like step by step?
2. What is your typical conversion rate from first outreach to closed deal (rough estimate)?
3. What usually makes someone say yes? What is the actual tipping point?
4. What kills deals most often? What objection or situation do you lose to?
5. Do you have a formal proposal, trial, or demo process?

---

#### Phase 2 Challenge Protocol

**Watch for these failure modes:**

| Answer pattern | Challenge |
|---|---|
| Lead magnet: "Contact us for a free consultation" | "A free consultation requires them to talk to you before they know if you're worth talking to. What could they receive that provides genuine value with zero interaction required from them first?" |
| Lead magnet: broad/generic free resource | "Would someone who is NOT your ideal customer also want this? If yes, it's not specific enough — it doesn't filter for your ICP." |
| Sales process: "We do a demo call" (full answer) | "What happens between 'demo call' and 'signed contract'? What's the buying committee? What questions do they ask on the call that you lose to? What's the single thing that makes someone go from interested to signed?" |
| "Conversion rate" is unknown | "Take a rough guess — how many conversations do you have before you close one deal? Even an order-of-magnitude estimate matters for sizing the outreach target." |
| "Deals die because of budget" | "Budget is a proxy for prioritization. When budget killed a deal, what did they spend the budget on instead — and what did that tell you about your positioning?" |

---

#### Phase 2 Validation Gate

```
Phase 2 Quality Check

| Answer area | Score | Issue |
|---|---|---|
| Lead magnet specificity | 🟢/🟡/🔴 | |
| Lead magnet ICP self-selection | 🟢/🟡/🔴 | |
| Sales process detail | 🟢/🟡/🔴 | |
| What closes deals | 🟢/🟡/🔴 | |
| What kills deals | 🟢/🟡/🔴 | |
```

**If any Red:** Do not proceed to Phase 3.

---

### Phase 3: The "After" Phase — Customers

#### Square 7: Customer Experience

1. What happens immediately after a customer signs up?
2. What is the moment customers first feel they made the right decision?
3. What do your best customers consistently say about working with you?

#### Square 8: Customer Lifetime Value

1. What is the average LTV of a customer?
2. Do you have upsells or expansion opportunities?
3. What is your current churn rate (roughly)?
4. What triggers customers to expand or upgrade?

#### Square 9: Referrals

1. Do you currently get referrals? What triggers them?
2. Do you proactively ask? How?
3. Who are complementary businesses that serve your ICP before or after you do?

---

#### Phase 3 Challenge Protocol

**Watch for these failure modes:**

| Answer pattern | Challenge |
|---|---|
| "Customers are happy" (no specific quote or metric) | "What's the most specific thing a customer has said about the outcome they got — a quote with a number or a before/after description?" |
| Referral answer: "We get some word of mouth" | "Word of mouth is passive. Do you have a specific process that produces referrals, or are you hoping satisfied customers remember to mention you?" |
| Upsell: "We don't really have upsells" | "10% of your customer base would pay 10x more for a premium tier, according to Dib. What would that look like for you — what's the most valuable thing you could offer an existing customer?" |

---

#### Phase 3 Validation Gate

```
Phase 3 Quality Check

| Answer area | Score | Issue |
|---|---|---|
| Customer outcome (specific quote/metric) | 🟢/🟡/🔴 | |
| LTV estimate exists | 🟢/🟡/🔴 | |
| Referral approach | 🟢/🟡/🔴 | |
```

**If any Red:** Resolve before generating the plan.

---

## Final Pre-Flight Checklist

Before writing `marketing_plan.md`, run this 12-item checklist against all answers collected. Present results as a table.

```
Pre-Flight Quality Check — All Phases

| # | Check | Pass? | Issue |
|---|---|---|---|
| 1 | ICP is a specific person: title + company stage + industry (not a category) | ✅/❌ | |
| 2 | At least 1 trigger event defined with a visible external signal | ✅/❌ | |
| 3 | USP contains zero banned words: quality, service, best, experienced, trusted, leading, premier | ✅/❌ | |
| 4 | Elevator pitch follows problem → solution → proof formula | ✅/❌ | |
| 5 | At least 2 specific competitors named with win/loss conditions | ✅/❌ | |
| 6 | At least 1 social proof point with a number or named customer | ✅/❌ | |
| 7 | At least 3 psychographic answers contain an emotion + specific situation | ✅/❌ | |
| 8 | At least 2 content topics that help the ICP without pitching the product | ✅/❌ | |
| 9 | At least 1 trigger event mapped to a specific outreach opening hook | ✅/❌ | |
| 10 | ICP scoring criteria are concrete enough for the research agent (high/medium/low with specific signals) | ✅/❌ | |
| 11 | Primary channel selection has a specific reason tied to ICP behavior | ✅/❌ | |
| 12 | Goals section has at least one metric with a number | ✅/❌ | |
```

**If any ❌:**
- Name the failing item
- Show an example of what weak looks like vs. strong (using the Quality Standards Reference above)
- Ask PG to strengthen the answer
- Re-run only the failing checks after the answer is updated

**Only write the file when all 12 checks are ✅.**

State: "All 12 quality checks passed — generating marketing_plan.md now."

---

## Output: marketing_plan.md

After the pre-flight passes, generate `marketing_plan.md` in the current working directory:

```markdown
# Marketing Plan
*Last updated: [DATE]*

---

## 1. Business Overview

**Product/Service:** [1-2 sentence plain-language description]
**Stage:** [Pre-revenue / Early / Scaling / Established]
**Primary goal (next 6-12 months):** [Specific measurable goal]
**Deal economics:** [Price point, sales cycle, contract type]

---

## 2. Target Market (ICP)

### Primary Segment
[Segment name and brief description]

**Why this segment (PVP scores):**
| Dimension | Score (1-10) | Notes |
|---|---|---|
| Personal Fulfillment | | |
| Value to Marketplace | | |
| Profitability | | |
| **Total** | | |

### Demographic Profile
- **Role/Title:** [e.g., VP of Engineering, Founder, Head of Data]
- **Company size:** [e.g., 50-500 employees, Series A-C]
- **Industry:** [e.g., B2B SaaS, FinTech, Healthcare]
- **Geography:** [e.g., US/Canada, English-speaking, global]
- **Seniority:** [e.g., Founder or VP level]

### Psychographic Profile
*(Used by research agent for ICP scoring and by personalization agent for outreach)*

- **Biggest pain / what keeps them up at night:** [Specific description with emotion]
- **Fears:** [What they're afraid of]
- **Frustrations:** [What makes them angry about current situation]
- **Industry trends they worry about:** [Specific trends]
- **What they secretly want most:** [The dream outcome]
- **Their day-to-day:** [How they spend their time]
- **Dominant emotion around this problem:** [e.g., overwhelmed, frustrated, anxious]
- **The ONE thing they'd pay anything to solve:** [Single most acute pain]

### Buying Behavior
- **Research channels:** [Where they look for solutions]
- **Decision makers involved:** [Who else is in the buying process]
- **Common objections:** [Top 3 objections before buying]

### Trigger Events (ICP Scoring Signals)
*Visible signals that a prospect is in buying mode — used by research agent to score leads higher*

| Signal | Visibility | Weight |
|---|---|---|
| [e.g., Just raised Series A] | LinkedIn, press | High |
| [e.g., Hiring data engineers] | LinkedIn jobs | High |
| [e.g., New CTO/VP Eng hired] | LinkedIn | Medium |

### ICP Scoring Criteria
*Used by research agent to assign ICP score (0-100)*

**High score (80-100) — ideal prospect:**
- [Criterion 1]
- [Criterion 2]
- [Criterion 3]

**Medium score (50-79) — worth pursuing:**
- [Criterion 1]
- [Criterion 2]

**Low score (<50) — deprioritize:**
- [Criterion 1]
- [Criterion 2]

---

## 3. Positioning & USP

**Why buy this type of solution at all:**
[The compelling reason to act — the cost of inaction]

**Why buy from us specifically:**
[The unique differentiator — what we have that competitors don't]

**Unique mechanism:**
[The specific methodology, technology, or process that makes us different]

**The result we sell (not the feature):**
[The transformation — what their business/life looks like after buying]

### Elevator Pitch
> "You know how [specific frustrating problem]? Well, what we do is [solution]. In fact, [specific proof point]."

### Competitive Landscape

| Competitor | Their Positioning | We Win When | They Win When |
|---|---|---|---|
| [Comp 1] | | | |
| [Comp 2] | | | |
| [Comp 3] | | | |

### Social Proof Available
- [Case study / testimonial / metric 1]
- [Case study / testimonial / metric 2]
- [Notable customers or press mentions]

---

## 4. Core Messages
*(Used by personalization agent and content writer)*

### Primary message (cold outreach)
[The main message for first-touch outreach — problem + solution + proof in 2-3 sentences]

### Message variants by trigger event
| Trigger | Opening hook |
|---|---|
| [Trigger 1] | [How to open the conversation] |
| [Trigger 2] | [How to open the conversation] |

### Topics the ICP finds valuable (content strategy)
*(Used by content writer for LinkedIn posts and newsletter)*
1. [Topic 1]
2. [Topic 2]
3. [Topic 3]
4. [Topic 4]
5. [Topic 5]

### Language and jargon the ICP uses
[Specific terms, phrases, acronyms the ICP uses that should appear in copy]

---

## 5. Channel Strategy

| Channel | Priority | Notes |
|---|---|---|
| Cold email | [High/Med/Low] | [Notes] |
| LinkedIn outreach | [High/Med/Low] | [Notes] |
| LinkedIn content | [High/Med/Low] | [Notes] |
| Newsletter | [High/Med/Low] | [Notes] |
| Community engagement | [High/Med/Low] | [Notes] |
| [Other channel] | | |

**Primary watering holes (communities, forums, events):**
- [Community 1]
- [Community 2]

---

## 6. Lead Capture & Nurturing

**Lead magnet / ethical bribe:**
[What we offer to get prospects to self-identify — free audit, report, tool, etc.]

**Nurturing approach:**
[How we stay in touch with leads who aren't ready to buy — newsletter cadence, content topics, etc.]

---

## 7. Sales Process

**Step-by-step process:**
1. [Step 1]
2. [Step 2]
3. [Step 3]

**What makes deals close:** [The tipping point]
**What kills deals:** [Common objections or blockers]

---

## 8. Customer Economics

- **Average deal value:** [e.g., $X/month or $X one-time]
- **Average customer lifetime:** [e.g., 18 months]
- **Average LTV:** [e.g., $X]
- **Current churn rate:** [e.g., X% monthly]
- **Upsell opportunities:** [What customers can expand into]

---

## 9. Referral Strategy

**Current referral sources:** [How referrals currently come in]
**Trigger for referrals:** [What prompts someone to refer]
**Referral partner categories:** [Complementary businesses]

---

## 10. Goals & Success Metrics

**Primary goal (6-12 months):** [Specific, measurable goal]

| Metric | Current | Target |
|---|---|---|
| Leads per month | | |
| Outreach reply rate | | |
| Meetings booked per month | | |
| Deals closed per month | | |
| MRR | | |
| LTV | | |
```

---

## Interview Conduct Guidelines

- **One phase at a time.** Don't ask all questions at once.
- **Challenge actively.** Use the Challenge Protocol at every phase. "Can you be more specific?" and "Can you give me a concrete example?" are always appropriate. Accept vague answers.
- **Use Dib's examples.** When pushing back, reference a specific contrast from the book. "Dib says quality and great service is what everyone claims — it's a table stake, not a USP. What can you say that they can't?"
- **Summarize back at phase end.** Confirm accuracy before running the validation gate.
- **The psychographic section is the most important.** These feed the personalization agent. Shallow emotional answers produce flat outreach. Push hard here.
- **Hard gates.** If an answer is Red at a phase gate, do not move on until it's reworked. This is non-negotiable.
- **Only generate the file after the pre-flight passes.** State which checks passed and which failed. Don't write the file with any ❌.

---

## Example Session: Challenge in Action

```
User: /marketing-plan

Claude: Let's build your marketing plan. I'll interview you across the 9 squares of the 1-Page Marketing Plan framework. Expect me to challenge weak answers — that's how we ensure the agents that read this file can actually use it.

Let's start with the basics.

Phase 0: Business Foundation

What does your product do? Describe it in plain language — problem, solution, who it's for.

---

User: We provide AI-powered analytics for B2B companies.

Claude: That's a starting point, but it's not specific enough to use in marketing. Let's sharpen it with Dib's elevator pitch formula:

"You know how [specific frustrating problem]? Well, what we do is [solution]. In fact, [proof]."

Try filling that in. What's the frustrating problem your ICP has RIGHT NOW — not "they need analytics," but the specific situation that makes analytics painful for them at this moment?

---

User: You know how B2B sales teams can't figure out why deals are stalling in their pipeline? Well, what we do is show exactly where deals die and why, in real time. In fact, one customer cut their sales cycle by 30% in 90 days.

Claude: That's much better. Clear problem, specific solution, quantified proof. Let's continue.

What stage is the business at? And give me a specific goal for the next 6-12 months — a number, not a direction.
```

---

## Reference

This skill is based on Allan Dib's *The 1-Page Marketing Plan* (2016). Quality standards derived from Dib's own bad vs. good contrasts throughout the book.

Key frameworks used:
- **9-cell canvas** (3 phases × 3 squares each)
- **PVP Index** (Personal Fulfillment × Value × Profitability) for segment selection
- **14 psychographic ICP questions**
- **Two USP questions** (why buy? why from me?)
- **Elevator pitch formula** (problem → solution → proof)
- **Three M's** (Message × Market × Media match)
- **33 bad vs. good contrasts** (quality standards reference above)
- **Hard validation gates** (phase-level + final pre-flight)
