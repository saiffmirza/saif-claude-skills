---
name: business-idea
description: Write a comprehensive markdown analysis doc for a business idea, product pivot, or new product direction. Output lands in ~/Documents/business ideas/ as a self-contained reference the user can revisit later. Use when the user says "save this as a business idea", "write this up as a pivot analysis", "make a doc for this idea", or when they've been discussing a product direction and want to formalize the thinking before deciding.
---

# Business idea analysis

Produces a comprehensive markdown analysis of a business idea and writes it to `~/Documents/business ideas/<slug>.md`. The output is meant to be a reference the user can revisit months later to remember the full reasoning, not just the conclusion.

## When to invoke

- User says: "make this a business idea doc", "save this as a pivot analysis", "write up this idea", "add this to business ideas"
- User has been discussing a product direction in conversation and wants to formalize the thinking
- User asks for a comparative analysis of multiple product directions and wants it durably saved

## Before writing — gather context

1. **Check existing docs in the folder.** Run `ls "$HOME/Documents/business ideas/"` to see what's already there. If a doc on this idea already exists (filename match or clearly the same concept), ask whether to update, replace, or create a new variant. If other unrelated ideas exist, note them — the new doc's "Other ideas considered" section may reference them.

2. **Discovery — walk every aspect of the idea before writing.** The goal: each of the aspects below has been *at least raised and considered*, even if the answer is "don't know yet" or "haven't thought about it." A doc full of "TBD" honestly labeled is better than a doc that silently skips dimensions. Don't fabricate; do prompt.

   Work through the checklist below. For anything the user has already covered in conversation, skip — don't re-ask. For everything else, ask. Batch related questions together (use `AskUserQuestion` for structured choice questions; free-form chat is fine when the answer is open-ended). Keep iterating in rounds until every aspect has at least been touched. It's normal to need 2–4 rounds of questions for a thin idea.

   When the user answers "I don't know" / "haven't thought about it" / "skip" — record that explicitly in the doc (e.g., "Target user: not yet defined") rather than inventing an answer. The point is that the dimension has been *surfaced*, not that it has been resolved.

   **Discovery checklist:**

   - **Core idea & one-line pitch** — what is it, in one sentence
   - **Target user** — who specifically, how they're currently solving this, why they'd switch
   - **Problem & alternatives** — what existing workflow/tool this replaces, why those fall short
   - **Differentiation** — what makes this not-just-a-feature-of-an-existing-product; named competitors and where each falls short
   - **Form factor & scope** — app, web, hardware, service; MVP surface area
   - **Starting point** — pivot from an existing codebase (which?), net-new build, or extension of something else
   - **Business model & monetization** — free / paid / freemium / ads / hardware-margin / subscription; rough price point if any
   - **Distribution** — how users will find it; organic, paid, viral, B2B sales, app store
   - **Technical feasibility & unknowns** — anything non-obvious to build; AI model choices, hardware constraints, platform limits
   - **Risks** — regulatory, cultural/religious sensitivity, technical, market saturation, strategic (does this fit the user's broader direction)
   - **Time horizon & commitment level** — exploratory daydream vs. near-term decision; how much time/money the user would actually spend
   - **Success signal** — what would make the user say "this is alive" in 4–8 weeks; what would say "this is dead"
   - **Alternatives considered** — other directions in the same conversation or sibling docs in the folder; why this one over those

   When in doubt whether to ask: if the answer would change the doc's recommendation or shape, ask. If it's a minor detail you can label "TBD", just label it and move on.

3. **Anchor on what's actually known.** If market data, user counts, or competitor pricing aren't known with confidence, say so in the doc using explicit labels ("rough estimate", "no verified data", "ballpark", "not yet defined"). Cite real numbers only when they have a real source.

## Doc structure

Adapt to the idea — not every section is relevant for every doc. The shape that consistently works:

1. **Header block** — date in YYYY-MM-DD, source (e.g., "conversation about X"), status (Exploratory / Decision-pending / Committed)
2. **Executive summary** — 3–5 bullets capturing what makes this idea worth considering. Lead with the strongest reasons. Honest about uncertainty.
3. **Key observations** — 2–4 paragraphs naming the load-bearing insights (specific, falsifiable claims that, if removed, would kill the idea). Not generic startup advice.
4. **Product positioning** — who's the target user, what's their current workflow, what the product replaces, what the one-line pitch is
5. **Build vs. reuse analysis** — if pivoting from an existing codebase, a table of what stays / what changes / what's net-new with rough effort estimates and percentages. If new from scratch, the equivalent "MVP scope" table.
6. **Competitive landscape** — name specific competitors and where each falls short. Avoid vague "the market is fragmented" language.
7. **Risks** — categorize: regulatory/legal, cultural/sensitivity, technical, market, strategic. Name uncomfortable risks honestly, including ones that might be tempting to skip.
8. **Monetization realism** — pricing comparable to named competitors, realistic scale ranges, ARR ballpark math. No fabricated TAM numbers.
9. **Phased roadmap (if pursued)** — phase 0 (deciding) through phase 3+ (growth). Concrete deliverables per phase, rough timeboxes in weeks.
10. **Concrete recommendation** — if pursuing, what's the very first deliverable that validates the thesis? What's the smallest demo that signals "this is alive" or "this is dead"?
11. **Honest summary** — 3–5 bullet recap of why this stands out (or doesn't)
12. **Other ideas considered** — comparative table of alternative directions discussed in the same conversation or existing as siblings in the folder. Future-self needs to see the alternatives, not just the conclusion.
13. **Reusable IP / patterns (if pivoting from existing code)** — extractable components that survive any pivot direction, not just this one

## Filename convention

`<product-or-codename>-<one-line-positioning>.md`

- Lowercase, hyphens for spaces
- No special characters, no spaces, no underscores
- Under ~50 chars total
- Self-describing on `ls` — future-self should know what's in the file without opening it

Examples that work:
- `miraya-for-muslim-creators.md`
- `notes-app-pivot.md`
- `quantkit-fintech-toolkit.md`
- `audio-journal-replacement-for-otter.md`

Examples that don't work:
- `idea-1.md` (not descriptive)
- `Business Idea - Photo App.md` (spaces, mixed case)
- `the-biggest-idea-ive-ever-had-about-changing-how-people-think-about-software.md` (too long, vague)

## Output location

Always write to: `~/Documents/business ideas/<slug>.md`

Note the space in the folder name. Quote the path in bash: `"$HOME/Documents/business ideas/"`.

Create the folder if missing: `mkdir -p "$HOME/Documents/business ideas"` (idempotent).

The folder is intentionally outside any git repo — strategy docs are personal notes, not codebase artifacts. They become out of date faster than code and don't belong in PR review.

## Writing principles

- **No hype.** State the case, name the risks, let the reader decide. Avoid superlatives ("revolutionary", "huge market", "massive opportunity") unless they're literally true with evidence.
- **No fabricated data.** Don't invent TAM numbers, user counts, or competitor MRR. If real data isn't known, say "rough estimate," "ballpark," or "no verified data" explicitly.
- **Specificity over abstraction.** Name specific competitors. Name specific technical components (e.g., `MTIImageEditor`, `PhotoStore`). Reference real file paths if relevant. Avoid generic startup-speak.
- **Self-contained.** The doc must be readable in isolation 6 months later, without the conversation context that produced it. Include the comparative alternatives at the bottom so future-self knows what else was on the table.
- **One file per primary idea.** Don't combine unrelated ideas in one doc. Comparative tables are fine, but each doc should have one main subject.
- **Date-stamp** at the top so staleness is visible. Market conditions, competitive landscape, and personal context all shift — a 2-year-old doc is suspect even if the analysis was right at the time.
- **Cite sources for any specific numbers.** "Tezza is $4.99/mo (published pricing)" is fine. "The Muslim creator market is $X billion" without a source is not.
- **Flag religious, cultural, regulatory, or ethical sensitivities prominently.** These are not afterthoughts — they belong in the Risks section with concrete mitigations.

## After writing

Briefly confirm to the user in 1–2 sentences:
- The filename written
- Whether the folder already had other idea docs (so they know if this is the first or part of a set)
- Any clarifying question that was deferred during writing and is worth raising now

Don't restate the doc's contents in chat — the file is the deliverable, not a chat summary of it.

## What this skill does NOT do

- Does not file Linear tickets, send Slack messages, or take any action on the idea beyond writing the doc. If the user wants to convert the doc into actionable tickets or a roadmap to execute, that's a separate ask.
- Does not commit the file to any git repo (the folder is outside repos by design).
- Does not generate code or scaffolding for the idea. The doc is strategic analysis; implementation is its own conversation.
- Does not validate the user's idea ("is this a good idea?"). It captures the analysis honestly; the decision is the user's.
