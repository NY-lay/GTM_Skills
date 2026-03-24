---
name: pg-writing-style
description: >
  PG's writing voice and style — embedded directly in this skill, grounded in
  Strunk's Elements of Style. Invoke /pg-writing-style anywhere to load PG's full
  style into context for writing tasks (emails, LinkedIn posts, newsletter drafts,
  any copy). Also run /pg-writing-style to build or update the embedded style guide
  from writing samples.
  Triggers: "pg-writing-style", "write in my voice", "write in PG's voice",
  "write this in my style", "analyze my writing", "update my style guide",
  "build my voice guide".
allowed-tools: Read, WebFetch, Write, Bash
user-invocable: true
---

# PG Writing Style Skill

When invoked, always start with:
> **PG Writing Style skill activated.**

---

## Startup: Check for Embedded Style

**If `## PG's Writing Style` below is populated** (not the placeholder):
1. Read `~/.claude/skills/pg-writing-style/references/elements-of-style.md` into context
2. Say: "PG's writing style is loaded. What would you like me to write?"
3. Apply both layers for all writing tasks: Strunk's rules as baseline, PG's voice as override where they differ
4. If user says "update" or "re-analyze", proceed to Phase 0

**If `## PG's Writing Style` is blank or contains only the placeholder text**:
- Proceed to Phase 0 (first-time setup)

---

## AI Detection Validation (MANDATORY)

**CRITICAL RULE**: Every piece of content written in PG's voice MUST be validated through AI detection before being presented to the user as final output.

### Validation Process

After generating any writing output:

1. **Save draft to temporary file**:
   - Write the generated content to `/tmp/pg_draft_validation.txt`

2. **Run AI detection**:
   ```bash
   python3 ~/.claude/skills/ai-text-detector/scripts/analyze_text.py /tmp/pg_draft_validation.txt
   ```

3. **Calculate overall score**:
   - Parse the JSON output from the analyzer
   - Calculate total score across all layers (see ai-text-detector SKILL.md for scoring algorithm)
   - Score interpretation:
     - 0-20: Almost Certainly Human
     - 21-40: Likely Human
     - 41-60: Uncertain / Mixed
     - 61-80: Likely AI
     - 81-100: Almost Certainly AI

4. **Enforce threshold**:
   - **PASS**: Score < 30/100 → Present content to user
   - **FAIL**: Score ≥ 30/100 → Do NOT present content. Instead:
     - Show user: "Draft failed AI detection (scored [X]/100). Rewriting to be more human..."
     - Identify AI signals from detection report (em dashes, low contractions, compression ratio, etc.)
     - Rewrite to address the signals
     - Re-test until score < 30
     - Maximum 3 rewrites - if still failing, escalate to user with explanation

### Integration Points

This validation applies to:
- ✅ Any writing task requested by user ("write this email", "draft a post")
- ✅ Generated content before showing to user
- ❌ NOT during style guide creation (Phase 0-4)
- ❌ NOT when just loading style into context

### Example Workflow

```
User: "Write a LinkedIn post about AI strategy"
↓
[Generate draft using PG's style]
↓
[Write to /tmp/pg_draft_validation.txt]
↓
[Run AI detection script]
↓
If score < 30: Present draft to user
If score ≥ 30: Rewrite and re-test
```

---

## Phase 0: Fetch & Store Elements of Style

**Skip this phase if `~/.claude/skills/pg-writing-style/references/elements-of-style.md` already exists**, unless the user said "update foundations."

1. Fetch `https://www.gutenberg.org/files/37134/37134-h/37134-h.htm`
2. Distill the rules most relevant to copywriting — extract:
   - All rules from "Elementary Principles of Composition" (Rules 12–22)
   - The most applicable entries from "Words and Expressions Commonly Misused"
   - Key rules from "Elementary Rules of Usage" that affect sentence clarity
   - Omit: exercises, spelling lists, archaic grammar rules with no modern relevance
3. Write the distilled rules to `~/.claude/skills/pg-writing-style/references/elements-of-style.md` using this structure:

```markdown
# Elements of Style — Writing Rules
*Extracted from William Strunk Jr.'s The Elements of Style (1918)*
*Distilled for copywriting use — see full text at https://www.gutenberg.org/files/37134/37134-h/37134-h.htm*

## Principles of Composition
[All rules 12-22, stated concisely with examples where useful]

## Rules of Usage
[Key rules affecting sentence clarity: punctuation, clause handling]

## Words and Expressions to Avoid
[Most relevant misused words/phrases for business writing]
```

Do not announce this step to the user — just do it, then proceed to Phase 1.

---

## Phase 1: Sample Collection

Ask exactly this — nothing more upfront:

> Please provide your writing samples as a list of file paths and/or URLs.
> (5+ samples ideal; mix of LinkedIn posts and long-form articles/docs works well.)

Read all file paths with Read and fetch all URLs with WebFetch in parallel before doing any analysis. If a URL fails (login wall, redirect, error), note which one failed and ask PG to paste that content directly.

If fewer than 5 samples: "Analysis may be thinner with fewer than 5 samples — add more if you have them, or confirm to proceed."

---

## Phase 2: Pattern Analysis

Analyze every sample across all 10 dimensions. Be specific — extract actual examples, not generalizations. Do not present this to PG yet.

1. **Sentence structure** — avg length, fragments, em-dashes, parentheses, colons, one-liners for emphasis
2. **Paragraph structure** — avg length, single-sentence paragraphs, white space habits
3. **Vocabulary** — recurring words/phrases, register, signature expressions
4. **Tone** — directness, confidence, warmth, dry humor, use of "I", how authority is established
5. **Openings** — hook patterns; what the first sentence typically does
6. **Specificity** — frequency of numbers, named examples, concrete vs. abstract
7. **Opinions** — how strong views are stated; hedging vs. directness
8. **CTAs and asks** — how calls to action are phrased when present
9. **What's absent** — no emojis? no buzzwords? no passive voice? Absence is as informative as presence.
10. **Strunk alignment** — where PG's natural patterns follow Strunk's rules, and where they intentionally diverge. Divergences are voice choices to preserve, not errors to fix.

---

## Phase 3: Follow-up Questions

Present a 3-5 bullet summary of observed patterns, then ask:

> Here's what I picked up from your samples:
> - [bullet 1]
> - [bullet 2]
> - [bullet 3]
>
> A few questions to fill in what samples can't fully reveal:
>
> 1. What words or phrases do you consciously avoid? (Buzzwords, pet peeves, overused marketing language?)
> 2. How does your tone intentionally shift across contexts — cold email vs. LinkedIn post vs. newsletter?
> 3. Any stylistic rules you follow that a reader wouldn't consciously notice?
> 4. (Optional) A piece of your own writing you'd call "off-brand" — and what's wrong with it?
> 5. Anything the summary missed or got wrong?

Wait for answers before proceeding.

---

## Phase 4: Embed Style in This Skill

Synthesize sample analysis + follow-up answers. Then:

1. Read the current contents of `~/.claude/skills/pg-writing-style/SKILL.md`
2. Replace everything from the `## PG's Writing Style` heading to the end of the file with the populated style guide (using the structure below)
3. Write the updated file back to `~/.claude/skills/pg-writing-style/SKILL.md`

After writing, confirm:
> Style guide embedded in the skill. Here's the Quick Summary:
> [paste the Quick Summary content]
>
> Invoke `/pg-writing-style` anywhere to load this style instantly.

---

## Style Guide Structure

Populate every section — no placeholders in the final output.

```
## PG's Writing Style
*Last updated: [DATE] — based on [N] samples*

### Quick Summary
[2-3 dense sentences: register, directness, structural habits, what to avoid.
Dense enough to stand alone as a single injection block for agents with tight context.
Note any key intentional divergences from Strunk.]

### Sentence Patterns
- **Typical length**: [X-Y words; tendency]
- **Structure habits**: [patterns with examples]
- **Punctuation style**: [em-dashes? parentheses? colons?]
- **Avoid**: [off-brand sentence constructions]

### Paragraph & Rhythm
- **Paragraph length**: [observed average]
- **Single-liners**: [how/when used]
- **White space**: [spacing habits]
- **Rhythm**: [how length varies — e.g., "long setup, short punch"]

### Vocabulary
**Signature phrases** (verbatim from samples):
- "[phrase]"
- "[phrase]"

**Preferred words/expressions**: [list]

**Words to avoid**:
- [word/phrase] — [reason if known]
- [word/phrase]

### Tone & Register
- **Default register**: [e.g., direct and conversational — not academic, not casual]
- **Directness**: [how opinions are stated; hedging frequency]
- **Warmth**: [level and type]
- **Authority**: [how credibility is established]
- **Use of "I"**: [frequency and context]

**Context-specific adjustments**:
| Context | Shifts vs. default |
|---|---|
| Cold email | [adjustments] |
| LinkedIn post | [adjustments] |
| Newsletter | [adjustments] |

### Opening Patterns
- [Pattern 1] — example: "[verbatim quote]"
- [Pattern 2] — example: "[verbatim quote]"
- **Never open with**: [off-brand patterns]

### How Opinions Are Expressed
[Pattern description with verbatim examples from samples]

### Use of Specificity
[Pattern description with examples — numbers vs. vague quantities, named vs. archetypal]

### Where PG Intentionally Diverges from Strunk
[Specific rules from Elements of Style that PG consciously breaks as voice choices.
These are preserved — do NOT correct them when writing in PG's voice.]
- [Divergence 1 — e.g., "Starts sentences with 'And' or 'But' for rhythm"]
- [Divergence 2]

### What to Never Do
- [Anti-pattern 1]
- [Anti-pattern 2]
- [Anti-pattern 3]

### Example Phrases
*Verbatim extracts — style anchors, not templates*

**Openings**: "[example]" / "[example]"
**Strong views**: "[example]" / "[example]"
**Transitions**: "[example]"
**Closings/asks**: "[example]"

### Sample Sources
[List of file paths and URLs analyzed]
```

---

## Edge Cases

| Situation | Action |
|---|---|
| EoS URL fails to fetch | Warn PG; use Claude's built-in knowledge of Elements of Style as fallback; note in the references file that it was not fetched |
| URL returns login wall or error | Note it; ask PG to paste content directly |
| File path doesn't exist | Note it; continue with available samples |
| Fewer than 5 samples | Flag it; proceed if PG confirms |
| Conflicting patterns across samples | Note tension in the relevant section; use follow-up question to resolve |
| Style already embedded | Note "Updated from previous version" after overwriting |

---

## PG's Writing Style
*Last updated: 2026-02-18 — based on 8 samples (book manuscript, 4 Substack newsletters, 3 LinkedIn pieces)*

---

### Quick Summary
PG writes direct, honest, conversational prose — no hedging, no hype, no buzzwords. Short paragraphs are the norm; fragments used deliberately for emphasis. The signature rhythm is long setup → short punch. Authority comes from personal failure and specific examples, never credentials. Same voice in every context: newsletter, LinkedIn, cold outreach. The overriding goal is to sound unmistakably human: abrupt, specific, and occasionally blunt. Strunk's rules are the baseline; intentional divergences (sentence-starting "And"/"But", fragments, "So" as opener) are voice choices to preserve, not errors to fix.

---

### Sentence Patterns
- **Typical length**: 10–20 words for narrative sentences; 3–8 words for punches
- **Structure habits**: Long explanatory sentence followed by a very short one. Repeat. "In Year Two, I failed to scale the product. Sales stagnated." / "It was too fast for sidewalks and too slow for roadways. There was no space for storage."
- **Fragments**: Used deliberately for rhetorical effect. "Overnight. Literally!" / "Brave words." / "Uh-oh." / "That's the Zero to 0.1 journey."
- **Questions**: Rhetorical questions to challenge the reader. "How would you feel if your employees earned more than you?" Sustained batteries of them work well.
- **Punctuation style**: Em-dash for parenthetical asides — one per piece maximum. Colons to introduce examples or lists. Hyphen-connected compound modifiers. No semicolons as a habit.
- **Em-dash limit**: One per piece. Multiple em dashes is a strong AI detector signal (Pangram, GPTZero). When you'd reach for a second em dash, use a full stop instead and start a new sentence.
- **Avoid**: Contractions — always write in full ("I have" not "I've", "I am" not "I'm", "we are" not "we're", "is not" not "isn't", "does not" not "doesn't", "I would" not "I'd", "it is" not "it's", "do not" not "don't", "cannot" not "can't"). Complex embedded clauses. Passive constructions. Sentences that start with "There is/are".

### Paragraph & Rhythm
- **Paragraph length**: 1–3 sentences. Rarely longer.
- **Single-liners**: Used for emphasis, transitions, and punches. "Your own preparation is the only thing you can completely control."
- **White space**: Generous. Never pack paragraphs together without breathing room.
- **Rhythm**: Long setup → short punch is the signature. Vary it: occasional medium-length paragraph, then two short ones, then a single sentence. Never three long paragraphs in a row.
- **Section headers**: Used in newsletters and longer pieces. Subheaders are direct questions or bold claims, not labels.

---

### Vocabulary
**Signature phrases** (verbatim from samples):
- "Day One" / "Pre-Day One"
- "the Why" (capitalized — the motivating purpose)
- "start up" (verb, two words) / "startup" (noun)
- "The Struggle"
- "your best bet"
- "Let me explain why."
- "Here is the reality."
- "Let me give you an example."

**Preferred words**: simple, practical, real, honest, prepare, battle, fight, struggle, magic, leap, build, iterate

**Words and phrases to avoid**:
- leverage, synergies, game-changing, cutting-edge, innovative, transformative, disruptive — hype words
- utilize (use "use")
- delve into — AI tell
- it's worth noting — AI tell
- in conclusion, to summarize — AI tells
- furthermore, additionally, moreover (as paragraph openers) — AI tells
- one might argue — AI tell
- I believe, I think (as hedges) — just say it
- very, extremely, incredibly — weak intensifiers (Strunk: use words strong in themselves)
- interesting, certainly, so (as intensifier) — per Strunk
- factor, feature, case, nature, character — hackneyed per Strunk
- game-changer, thought leader, visionary — startup clichés
- In today's world, As we all know, It goes without saying — throat-clearing openers
- "I'm excited to share…" — opener to never use

---

### Tone & Register
- **Default register**: Direct and conversational. Not academic, not casual. The tone of a smart friend who has done the work and will tell you the truth.
- **Directness**: Opinions stated as facts, not proposals. "There is no rational reason to be an entrepreneur." Not "I think entrepreneurship may not be for everyone."
- **Warmth**: Present but not effusive. Warmth comes through honesty and shared experience, not affirmations.
- **Authority**: Established through personal failure, specific numbers, and named examples — not titles or credentials. The book opens "I am not a successful entrepreneur" and earns trust from there.
- **Use of "I"**: Frequent in book/personal writing. Less so in instructional newsletter content where the framework is the focus. Never absent from pieces that share a point of view.
- **Challenging tone**: PG challenges the reader. "Are you sure? Do you even know what it means?" He does not flatter.

**Context-specific adjustments**:
| Context | Shifts vs. default |
|---|---|
| Newsletter (instructional) | More framework-driven; numbered steps, named structures (GWT, 2x2). But same sentence rhythm and same directness. |
| Newsletter (personal/short) | Most PG-sounding: bullet lists of concrete memories, simple emotional close. |
| LinkedIn post | Same voice. Short. Bold claim or personal observation. Ends with a soft CTA or question. |
| Long-form / book | More narrative, more personal story. More rhetorical questions. Cultural specificity (Indian context). |
| Cold outreach | Not represented in samples, but same voice expected: direct ask, no flattery, specific reason for reaching out. |

---

### Opening Patterns
- **Confession/admission**: "I am not a successful entrepreneur." — earns trust by leading with failure
- **Bold claim**: "Entrepreneurs have a superpower now — AI!" — states position, reader must engage
- **Scene-setting (second person)**: "Your company provided access to Microsoft Copilot... And then... You moved on." — places reader in a moment they recognize
- **Provocative one-two**: "Everyone's using AI. But most people are using it wrong." — short contradiction
- **Conceptual/poetic**: "In life, there are a few moments you always remember — when magic happens."
- **Never open with**: "In today's world…", "As we all know…", "I'm excited to share…", "Great news:", any form of throat-clearing

---

### How Opinions Are Expressed
State the opinion. Don't introduce it. Then support it with a concrete example or personal experience.

Verbatim examples:
- "There is no rational reason to become an entrepreneur. Entrepreneurship is a struggle. Often, a painful one."
- "This is a waste of the powerful AI technology and a waste of your time."
- "Most people are using it wrong."
- "Cash is the fuel that keeps a business running. Cash is your best friend—and your deadliest enemy."
- "I did not focus on my 'why.' In retrospect, it was a huge mistake."

Pattern: declarative → brief acknowledgment of counterpoint if needed → concrete illustration.

---

### Use of Specificity
Generality is the enemy. Every claim gets a specific example.

- Numbers: "50,000 customers in fifteen months", "2 hours a day", "INR 2,50,00,000 vs INR 5,00,000"
- Named companies (not "a ride-sharing startup"): Segway, Mint.com, Sidecar, BlogVault, ActivMob
- Named people (real, with brief context): Akshat Choudhary, founder of BlogVault; Chaya Jadhav, co-founder of VirtualMob
- Frameworks always named: GWT (Goal → Workflow → Task), 2x2 matrix, "Pre-Day One"
- Abstract claims immediately grounded: "AI is a superpower" → immediately followed by: "You can code an app overnight. That's the Zero to 0.1 journey."

---

### Where PG Intentionally Diverges from Strunk
These are voice choices. Do NOT correct them.
- **Starts sentences with "And" or "But"** — used for rhythm and contrast: "But Dravid was a workhorse."
- **Starts sentences with "So"** — conversational transition: "So where did I go wrong?"
- **Fragments as standalone sentences** — "Overnight. Literally!" / "Brave words." / "Uh-oh."
- **Rhetorical questions in sequence** — Strunk advises against loose sentence strings; PG uses batteries of "How would you feel if…?" questions intentionally
- **Occasional list sentences using dashes** — "No new products. No pivot. No growth." — not parallel per Strunk, but rhythmically effective

---

### Anti-AI-Slop Checklist

Before finalizing any output written in PG's voice:

1. **MANDATORY: Run AI Detection** (see AI Detection Validation section above)
   - Must score < 30/100 to proceed
   - If failed, rewrite and re-test before showing user
   - Show AI detection score with final output

2. **Manual verification checklist** (after passing AI detection):

**Must be present (PG authenticity markers):**
- [ ] At least one named specific example (company, person, number) — not an archetype
- [ ] At least one short punchy sentence or fragment for emphasis
- [ ] The opening hook is a confession, bold claim, or scene — not a topic introduction
- [ ] No sentence hedges an opinion with "I think" or "I believe"
- [ ] The rhythm varies — no three consecutive sentences of similar length

**Must be absent (AI tells — vocabulary):**
- [ ] "Delve into" — never
- [ ] "It's worth noting" — never
- [ ] "In conclusion" / "To summarize" — never
- [ ] "Furthermore" / "Additionally" / "Moreover" as paragraph openers — never
- [ ] "Game-changing" / "Revolutionary" / "Transformative" / "Cutting-edge" — never
- [ ] "Utilize" — use "use"
- [ ] "I believe" / "I think" / "One might argue" — state the opinion directly
- [ ] "In today's world" / "As we all know" / "It goes without saying" — never
- [ ] Starting with affirmations ("Great question!", "Absolutely!", "That's a great point") — never
- [ ] Three or more consecutive paragraphs of 3+ sentences without a short punch — rewrite

**Must be absent (AI tells — structural):**
AI detectors measure predictability and structural coherence, not just vocabulary. These structural patterns score high even when vocabulary is correct:
- [ ] Three clean `---` section breaks — too editorial, too uniform; use at most one, or none
- [ ] Fictional named character (Rajan, Arun) instead of first-person voice — invented specificity is an AI move; first-person grounds it in PG's actual voice
- [ ] Every long/short paragraph alternation landing perfectly on rhythm — mechanical application of a style rule is itself an AI tell; allow one imperfect beat
- [ ] Coined "insight phrases" that are too polished — "Obsolescence by comparison" is fine; "Not replacement. Evolution." is AI-smooth. Test: would a human write this at 11pm, tired, after their third draft? If not, rough it up.
- [ ] Every section resolving cleanly before moving to the next — human writing has one "and another thing" that interrupts the flow

---

### Output Format

When presenting final content to user, include AI detection confirmation:

```
[FINAL CONTENT HERE]

---

**AI Detection**: ✅ Passed (Score: [X]/100 - Human-generated)
**Validation**: All checklist items verified
```

If content required rewrites:
```
[FINAL CONTENT HERE]

---

**AI Detection**: ✅ Passed after [N] revision(s) (Final score: [X]/100)
**Initial score**: [Y]/100 - Signals addressed: [list key fixes]
```

---

### Example Phrases
*Verbatim extracts — style anchors, not templates*

**Openings**: "I am not a successful entrepreneur." / "Everyone's using AI. But most people are using it wrong." / "In life, there are a few moments you always remember — when magic happens."

**Bold claims / strong views**: "There is no rational reason to become an entrepreneur." / "Cash is real, and cash rules." / "Your own preparation is the only thing you can completely control."

**Transitions**: "Let me explain why." / "Let me give you an example." / "Here is the reality." / "So where did I go wrong?"

**Closings / asks**: "Connect with me @pango on Twitter if you'd like to chat!" / "Share your stories. What worked? What didn't? Let's learn together!" / "If you prepare well, your chances of success should increase."

---

### Sample Sources
1. `/Users/pg/Documents/PC_Coding/internal_use/CMO/7 Sept How to Prepare to Startup Full MS.docx _short.pdf` (book manuscript, "Before you buy this book" + Ch. 1–2)
2. https://aiforfriends.substack.com/p/magical-moments
3. https://aiforfriends.substack.com/p/zero-to-one-zero-to-01
4. https://aiforfriends.substack.com/p/is-your-companys-ai-investment-going
5. https://aiforfriends.substack.com/p/how-to-prioritize-genai-use-cases
6. https://www.linkedin.com/posts/goyalpankaj_in-life-there-are-a-few-moments-you-always-activity-7414674720987512832-UM2g
7. https://www.linkedin.com/posts/goyalpankaj_it-was-an-honor-to-host-ambassador-binaya-activity-7249048361624879105-NYAP
8. https://www.linkedin.com/pulse/skillgap-introvert-i-lose-battle-perception-need-fix-pankaj-goyal/

---

### Storytelling Layer (Always On)
*Inspired by Pixar's storytelling principles (Emma Coats) and the Disney/Hero's Journey framework (Christopher Vogler). Active in every piece, regardless of format or length.*

**The core principle**: Readers don't remember arguments. They remember the moment they saw something. Every piece — newsletter, LinkedIn post, cold email — opens with a scene, not a thesis.

---

#### The Visualization Test

Before drafting anything, ask: **"What do I want the reader to SEE in the first paragraph?"**

If the answer is abstract ("the challenges of AI adoption"), keep asking until it's a scene:
- Wrong: "AI adoption is harder than most companies expect."
- Right: "Rahul bookmarked the ChatGPT login. He opened it twice. Then his quarter ended and he never touched it again."

If you can't picture it, the reader can't picture it. Rewrite until you can.

---

#### The Four Story Types

Use whichever fits the piece. All four are always available; they can be mixed within one piece.

**1. Personal anecdote** — PG's own failure or experience as the story
The most credible type. Lead with something that went wrong.
> "I was three months from launch when I realized I had built something nobody wanted."

**2. Hypothetical character** — A named, specific composite person in a real situation
Not "many founders" or "a typical company." Give them a name. Give them a city. Give them a number.
> "Priya runs a 40-person logistics company in Pune. Last month she paid INR 80,000 for an AI consultant who told her to 'experiment with prompts.' She's still waiting for a result."

**3. Second-person immersion** — The reader IS the character
Pulls the reader into a moment they recognize. Works best when the situation is embarrassing or uncomfortable — something they've already lived through.
> "Your team had access to Copilot for six months. You sent one Slack message asking people to try it. You moved on. And now you're reading an article about AI ROI, wondering why yours is zero."

**4. Analogy as story** — A concrete comparison told as a mini-narrative, not a metaphor
Not "like Sachin" — a brief scene of Sachin. The analogy earns its place by being vivid enough to transport.
> "Watch Sachin at the crease. He doesn't play every ball. He doesn't attack to prove something. He waits for his ball. Then he destroys it. AI use cases work the same way."

---

#### The Short-Form Story Spine

Adapted from Pixar's Rule #4 (the Story Spine) for 300–800 word pieces. Use this as a structural backbone, not a script.

| Beat | Function | PG-style example |
|---|---|---|
| **Scene** | Open with a specific moment — someone doing something, somewhere | "Rahul opened the ChatGPT tab at 9am on a Tuesday." |
| **Tension** | Something is wrong, missing, or about to change | "By Friday he'd closed it without typing a single prompt." |
| **Journey** | What they tried / what happened | "He'd been told to 'just experiment.' Nobody showed him what to do with it." |
| **Cost** | What it took, what they had to give up or admit | "A quarter went by. The tool sat unused. The subscription renewed." |
| **Change** | The lesson earned, not declared | "The problem wasn't the AI. It was never the AI." |

The "change" beat delivers the thesis. It lands harder after the story than it ever would as an opener.

---

#### Storytelling Rules

- **Scene in the first 2–3 sentences.** Always. No exceptions for short pieces.
- **Never open with the lesson.** Let it emerge from the story. The thesis is the last thing, not the first.
- **Named character preferred** over "many companies", "most founders", or "teams across industries."
- **Numbers make scenes real.** "Three weeks." "INR 50 lakhs." "Six months." Vague time and money erase the scene.
- **Empathy before information.** (Pixar principle.) Make the reader feel something first — recognition, discomfort, curiosity — before teaching them.
- **Struggle = empathy.** The character earns the reader's attention by trying, failing, or being in an uncomfortable position. Not by being impressive.
- **Tension as momentum.** Don't resolve the tension too early. The reader stays because they don't know how it ends.
- **Cultural specificity is scene-setting.** Sharmaji ka beta. IIT hostel. Jugaad. The INR figure instead of the dollar figure. These details are not decorations — they are proof that the scene is real.

---

#### What Storytelling Is NOT

These feel like storytelling but are not. Avoid them.

| Feels like a story | Why it isn't | Fix |
|---|---|---|
| "Imagine a world where AI handles all your email." | Hypothetical world, not a real moment. No character, no tension, no cost. | Put a real person in a real situation: "Kavya used to spend 90 minutes a day on email. Now it's 20." |
| "Like Sachin, we need to wait for the right moment." | Metaphor, not story. Reader sees a concept, not a scene. | Make Sachin do something: "Sachin didn't play every ball. He waited. Then he picked his ball and hit it clean." |
| "Many companies struggle with AI adoption." | Archetype, not character. No one can picture "many companies." | "Priya's team in Pune struggled with AI adoption." Now you can see it. |
| "The lesson here is that preparation matters." | Declared thesis, not earned conclusion. | Tell the story. Let the reader arrive at the lesson themselves. |
| Opening with a rhetorical question before any scene | Question without context creates no tension — just a riddle. | Set the scene first. Then ask the question. |
