---
name: interview-prep
description: Generate a tailored interview cheat sheet for a specific job description and round. Identifies knowledge gaps, drafts honest-gap-with-pivot answers BEFORE the interview, builds a multi-framing story bank, and ends with a post-call retrospective template.
---

# Interview Prep

Generate a tailored interview cheat sheet for a specific job description and interview round.

## Why this skill exists

The user has lost answers in real interviews because the gap between "I know I have a weak area" and "I have the pivot answer rehearsed" wasn't closed before the call.

Concrete failure mode this skill is designed to prevent:

- **Gametime EM round, 2026-05-04.** JD weighted heavily on Core Web Vitals and performance optimization. The user had honestly flagged "haven't owned a CWV sprint" as a gap in his cheatsheet — but didn't have the pivot answer ready. When the EM asked about a time he optimized performance, he answered "I plan things well so I haven't had to come back and adjust." That's a senior-IC red flag (real systems always need ongoing perf work). Worse: he had perf-adjacent stories ready in his points bank — AbortController for race-condition cancellation, server-time-synced clock to avoid round-trips, S3 image fallback that prevents layout shift — but he hadn't indexed those stories under "performance" framing. He had the material; he didn't have the index.

The skill must force three things:

1. **Multi-framing story indexing.** Every story gets framed under multiple tags, not just one.
2. **Pre-drafted pivot answers.** For every weak/gap area in the JD, the answer is rehearsed before the call.
3. **Junior/senior framing audit.** Common junior phrasings flagged with senior alternatives.

## Context

The user maintains career-intelligence docs:

- `~/Documents/playon-resume-points.md` — quantified accomplishments bank
- `~/Documents/playon-resume-findings.md` — authoritative source for PlayOn work (overrides points bank on disagreements about PlayOn)
- `~/Documents/kiyas.md` — positioning advice for the Kiyas open-source MCP server
- `~/Documents/playon-questionnaire.md` — scope/outcome/mechanism numbers
- `~/portfolio/src/lib/experience.ts` — portfolio experience data
- `~/Documents/SaifMirza-{Company}-*.md` — past interview cheatsheets (read these to learn from past prep + post-mortem any retrospective notes)

## Inputs

The user provides:

1. **Job description** — text in the prompt or a file path. If a URL, ask the user to paste the text (don't try to fetch).
2. **Company name** — for output filename.
3. **Round type** — one of: `Recruiter`, `EM30`, `EM60`, `Tech`, `SystemDesign`, `Panel`, `Final`. Ask if not specified.
4. **Optional: prior round notes** — if user has already done a round at this company, ask if there's a retrospective to read.
5. **Optional: specific weakness** — "I bombed the perf question last round" or "I'm worried about system design." If named, give that area extra prep.

If any of these aren't provided, ASK — don't guess.

## Process

### Step 1: Analyze the JD

Build a weighted requirements table. For each requirement, mark Saif's evidence level:

- **STRONG** — multiple resume points or stories support this directly
- **MEDIUM** — has adjacent experience, can build a credible answer
- **WEAK** — has tangentially related work, needs careful framing
- **GAP** — no supporting experience; honest-gap-with-pivot answer required

Weight by JD prominence — bolded skills, repeated phrases, named frameworks, and specific responsibilities count more than generic bullets.

The questions most likely to come up are the ones where Saif is in the WEAK or GAP buckets, because that's where the JD's central ask is and the interviewer wants to verify it.

### Step 2: Gather source material

Read in this order:

1. The JD analysis from Step 1
2. `~/Documents/playon-resume-findings.md` (authoritative for PlayOn)
3. `~/Documents/playon-resume-points.md`
4. `~/portfolio/src/lib/experience.ts`
5. Any prior cheatsheets for this company in `~/Documents/`
6. Any prior cheatsheets for similar role types

### Step 3: Build the story bank with multi-framing exercise

This is the critical step.

For each candidate story (target: 7 strong stories), brainstorm multiple framings. NOT every story has every framing, but most have 2-3 valid ones.

Framings to consider:

- **Technical depth** — "tell me about a hard technical problem"
- **Performance** — "tell me about a perf optimization"
- **Behavioral / leadership** — "tell me about a time you led"
- **Disagreement** — "tell me about a conflict"
- **Mistake / regret** — "tell me about a tradeoff you'd redo"
- **0-to-1** — "tell me about something you built from scratch"
- **Cross-functional** — "tell me about working with PM/design"
- **Mentoring** — "tell me about teaching or unblocking"
- **Ambiguity** — "tell me about handling unclear requirements"
- **Tight deadline** — "tell me about delivery pressure"
- **Ramp on unfamiliar tech** — "tell me about learning a new stack"

Output each story with the framings that fit, not just one tag.

Concrete example from the Saif story bank:

> **Ticket Redemption Flow** (GoFan):
> - Cross-platform / React Native (primary)
> - **Performance** — AbortController prevents wasted server work; server-time-sync avoids round-trip per render; S3 fallback prevents layout shift on missing images
> - Real-time / consumer surface
> - Tight deadline — game day stakes
> - Race condition handling — secondary technical depth framing
> - Design partnership — cross-functional framing

When the EM asks "tell me about a time you optimized performance," the user reaches for this story — even though he wouldn't have indexed it under "performance" by default.

### Step 4: Draft honest-gap-with-pivot answers (the most important step)

For every WEAK or GAP requirement from Step 1, draft the answer the candidate will give if asked.

Template:

> "I haven't owned [specific gap area] with measured before-and-after deltas, so I'll be honest about that gap upfront. What I have done is [specific adjacent work, named].
>
> [Concrete example 1 with technical detail.]
>
> [Concrete example 2 if available.]
>
> What I'd want to do at [Company] is build the explicit [gap area] muscle. [Specific tools/practices that would close the gap.] That's the growth I'd be coming for in this role."

Length: 60-90 sec when read aloud.

This answer must be IN the cheatsheet, ready to deliver verbatim. The failure mode is having identified the gap but not having the pivot rehearsed.

**Hard rule:** the answer is never "I don't have experience with that." Always pivot.

### Step 5: Junior/senior framing audit

For every drafted answer, check against the junior framings to avoid. Flag and rewrite if any appear:

| Junior framing (avoid) | Senior framing (use) |
|---|---|
| "I plan well so I haven't had to optimize" | "Performance work is continuous. Three examples I've worked on..." |
| "I don't have any experience with that" | "I haven't owned that, but here's adjacent work + the growth I'd want here" |
| "We never disagreed on the team" | "Here's a real disagreement and how I handled it" |
| "I just did what the PM said" | "I pushed back on scope. Here's what changed and why" |
| "My weakness is I work too hard" | Specific, real weakness + what I'm doing about it |
| "It just worked" | "Here's the tradeoff I made and what I gave up" |
| "I'd build it the right way" | "Here's the alternative I considered and rejected" |

### Step 6: Round-shape-specific structure

The cheatsheet shape must match the round duration and type. Don't pack a 60-min agenda into a 30-min round prep.

**Recruiter screen (15-30 min):**
- Tell-me-about-yourself (~60 sec)
- Why this company (~45 sec)
- Why leaving current role (~30 sec)
- Comp expectations (deflect if possible, give range if pressed)
- Timeline / availability
- 2-3 process questions to ask
- Skip technical depth

**EM / HM 30-min:**
- Tell-me-about-yourself (~60 sec)
- Why this company (~45 sec)
- 3-5 likely behavioral probes with story tags pre-mapped
- 1 technical probe scripted answer
- AI workflow probe if JD mentions
- 2 questions to ask (max)
- Pre-rehearsed honest-gap-with-pivot for the 2-3 most likely probes

**EM / HM 60-min:**
- Same as above plus:
- 2-3 deeper technical probes scripted
- Soft system-design probe section
- 4-5 questions to ask

**Technical screen / coding round:**
- Common live-coding shapes for the role's stack
- React/TS/whatever fundamentals refresh
- Domain-specific algorithmic patterns
- Tradeoff vocabulary

**System design round:**
- Common shapes for the company's domain (ticketing → search, real-time inventory, payment flow; fintech → real-time multi-client state, transaction reconciliation; etc.)
- Tradeoff vocabulary (consistency vs availability, latency vs throughput, cost vs reliability)
- Drawing-board fluency

**Panel / final round:**
- Mix of all above
- Often includes a "values" or leadership round — prepare for vision/motivation questions

### Step 7: Identify the 2-3 most-likely probes

Based on JD weight + Saif's gaps, identify the 2-3 questions most likely to come up. Pre-draft strong answers for each. These are the must-have-warm answers.

Surface these prominently in the cheatsheet — don't bury them.

### Step 8: Pre-call rapid-review checklist

End the cheatsheet with a 5-minute pre-call section:

- The 3 sections to re-read in the last 5 min
- The cold-answer scripts (TMAY = "tell me about yourself", "why this company")
- The story tags for behavioral mapping
- The honest-gap pivot answers
- The 2 questions to ask
- Logistics checklist (water, stand, smile, URLs)

### Step 9: Post-call retrospective template

Include this template at the bottom of every cheatsheet:

```
## Post-call retrospective (fill out within 1 hour)

What was asked vs what was prepared:
- [question]: [how I answered] → [strong / fine / weak]

Any answer that felt weak — draft a stronger version NOW (don't trust your future self):
- Question: ___
- What I should have said: ___

Decision: send corrective follow-up note?
- Yes if a key answer felt weak. Use the corrective-note template.
- No if everything was fine. Send standard thank-you note.

Thank-you note: send within 4 hours.
- Reference one specific thing they said
- Don't grovel
- Don't repeat resume

Next steps:
- [What the interviewer said happens next]
- [Calendar reminder for follow-up if no response in 5 business days]
```

## Output

File path: `~/Documents/SaifMirza-{Company}-{RoundType}-Cheatsheet.md`

Examples:
- `~/Documents/SaifMirza-Gametime-EM30-Cheatsheet.md`
- `~/Documents/SaifMirza-Phantom-Tech-Cheatsheet.md`
- `~/Documents/SaifMirza-Owner-Recruiter-Cheatsheet.md`

Format: markdown, plain.

Tone: per the user's preference — plain, warm, matter-of-fact. No grandiose framings. No em dashes. Use commas, colons, periods, parentheses.

## Templates

### Thank-you note (sent within 4 hours)

```
Subject: Thanks for the conversation

Hi [Name],

Thanks for taking the time today. [One specific reference to something they said — a codebase pain point, a team detail, a technical decision they mentioned.]

Looking forward to hearing about next steps.

Best,
Saif
```

### Corrective follow-up note (when an answer felt weak — send same day)

```
Subject: Quick follow-up — [topic] question

Hi [Name],

Thanks for the conversation today. I wanted to follow up on one answer.

When you asked about [topic], I gave a weaker framing than I should have. [Brief acknowledgment, one sentence max — no groveling.]

[Concrete example 1 with technical specificity.]

[Concrete example 2 if available.]

[Tie to honest gap if relevant — don't fake having done something you haven't.]

Looking forward to hearing about next steps.

Best,
Saif
```

The corrective note is the recovery move when a key answer landed badly. Used at Gametime EM round 2026-05-04 to recover from the perf-question weak answer.

### Recruiter follow-up (5 business days of silence)

```
Subject: Following up

Hi [Name],

Just checking in on next steps after my conversation with [previous interviewer]. Happy to provide anything else helpful.

Best,
Saif
```

Send once. If silent after that, accept the answer.

## Anti-patterns and pitfalls

### In the cheatsheet

- **Don't generate a cheatsheet that's longer than the user can review in 30 minutes.** Pre-call review must be feasible.
- **Don't pad the story bank with weak stories.** 7 strong stories beat 11 mixed-quality. Drop the thin ones.
- **Don't fake a story to match a topic.** If the JD asks for X and the user doesn't have X, draft the honest-gap-with-pivot answer, not a stretched fit.
- **Don't bury the honest-gap answers.** Surface them prominently.
- **Don't write a cheatsheet that the user has to read off live.** Practice arc, not script. Each answer is a 60-90 sec arc the user can reproduce in their own words.

### In the user's behavior (flag in cheatsheet)

- Ramble past 90 sec. Stop. Let the interviewer drive.
- Bash previous employer when asked "why are you leaving."
- Ask comp questions to the EM. Those go to the recruiter.
- Ask technical depth questions to the recruiter. Those go to the EM/team.
- Skip the thank-you note. It's the only post-call lever.
- Read into a recruiter's "we'll be in touch" too literally — it's standard language.

## Checks before reporting done

- [ ] All JD requirements have an evidence level (STRONG/MEDIUM/WEAK/GAP)
- [ ] Every WEAK and GAP requirement has a drafted honest-gap-with-pivot answer
- [ ] Every story is indexed under at least 2 framings
- [ ] The 2-3 most-likely probes are surfaced prominently with full answers
- [ ] Junior framings have been audited and rewritten if found
- [ ] Round-shape matches the duration (don't pack 60 min into 30)
- [ ] Cold answers for TMAY and "why this company" are written
- [ ] Pre-call rapid-review checklist is at the end
- [ ] Post-call retrospective template is at the end
- [ ] No em dashes. Tone is plain and matter-of-fact.

## When the user reports back after the interview

If the user shares notes from a real interview, do this:

1. **Identify the question(s) that landed badly.** Be honest, not reassuring. "I plan well so I don't need to optimize" is a junior framing — name it.
2. **Draft the corrective answer.** Use the structure: honest acknowledgment + concrete examples + honest gap + growth framing.
3. **Decide on a corrective follow-up note.** If a high-weight question landed badly, send the corrective note same-day. The window closes when the EM submits notes to the recruiter (usually within 24-48 hours).
4. **Update this skill.** If the failure mode is a new pattern, encode it in the anti-patterns section so the next cheatsheet prevents it.

## Skill maintenance

This skill should evolve with each interview. After each round:

- Did the cheatsheet predict the questions well? If not, what did it miss?
- Did any answer land badly? Why? Was the failure pattern preventable in prep?
- Did the pre-call rapid-review section work, or did the user end up scrambling?

Encode learnings in the anti-patterns section or in the relevant process step.

The "Why this skill exists" section at the top of this file is a real failure log. Add to it as new lessons emerge — concrete dates, concrete failure modes, concrete fixes. Resist abstracting too early.
