---
name: tailor-resume
description: Generate a tailored resume PDF for a specific job posting. Takes a job description and produces a one-page PDF highlighting the most relevant experience.
argument-hint: <paste the job description or provide a file path>
---

# Tailor Resume

Generate a one-page tailored resume PDF from a job description.

## Context

The user maintains a resume points bank at `~/Documents/playon-resume-points.md` containing all quantified accomplishments from their career, organized by project/feature. Their general resume PDF is at `~/portfolio/public/SaifMirzaResume.pdf`.

Career-intelligence docs to also consult when relevant:
- `~/Documents/kiyas.md` — positioning advice for the Kiyas MCP server (the lead open-source asset)
- `~/Documents/playon-questionnaire.md` — scope/outcome/mechanism numbers the user may be progressively filling in
- `~/Documents/playon-resume-findings.md` — cross-repo git + Jira findings from the user's last 12 months at PlayOn (2026-04-24). Source of truth for the Lambda→EKS migration scope, tournament-pass framing (NOT "Tournament Creation Flow with bracket generation"), gofan-emailer ownership, platform tooling authored, and the 13 WCAG accessibility tickets. Read this before writing any Playon bullet; it corrects earlier stale framings.

## Inputs

The job description is provided via `$ARGUMENTS`. If it's a file path, read the file first.

## Process

### Step 1: Analyze the job description

Identify:
- Required skills and technologies (exact matches to highlight)
- Nice-to-have skills
- Key themes (e.g., payments, mobile, infrastructure, AI, security, trading)
- Seniority signals (years of experience, leadership expectations)
- Role family (frontend / full-stack / prompt-eng / infra / mobile) — this decides which summary line to use

### Step 2: Gather all source material

Read ALL of these to get the full picture:

1. **Playon findings (authoritative for Playon work)**: `~/Documents/playon-resume-findings.md`. This overrides the points bank on any disagreement about Playon work.
2. **Resume points bank**: `~/Documents/playon-resume-points.md`
3. **Current general resume**: `~/portfolio/public/SaifMirzaResume.pdf`
4. **Portfolio experience data**: `~/portfolio/src/lib/experience.ts`
5. **GitHub repos**: Run `gh repo list saiffmirza --limit 20 --json name,description,primaryLanguage,stargazerCount,url` to get the latest public projects.
6. **Kiyas positioning advice** (`~/Documents/kiyas.md`) if the role is frontend / AI / dev-tools adjacent.

Use GitHub data for accurate, up-to-date project descriptions. If a repo is relevant to the job and not in the points bank, include it.

### Step 3: Draft a tailored summary line (new)

Write one or two sentences that go immediately below the header, above Skills. This is the top third of the resume — recruiters eye-track it for 6–11 seconds. Rules:

- One line if possible, two max. Keep under 180 characters total.
- Lead with seniority-appropriate title that matches the role ("Software Engineer," "Prompt Engineer," "Full-Stack Engineer"). **Title guardrail**: Saif is currently Software Engineer II at PlayOn (~5 years total experience). Do NOT mirror titles like "Senior Software Engineer," "Staff Engineer," "Lead," or "Principal" even when the JD lists them. Only use a title if the resume evidence supports it. If the JD asks for senior level, lead with "Software Engineer with 5+ years..." rather than claiming the senior title.
- Follow with 2–3 comma-separated specialization phrases that mirror the job description's exact vocabulary.
- Never use the same summary across job types. Re-draft per application.

Examples of how to shape it per role family:

- **Frontend / AI product surface**: "Software Engineer specializing in AI-native product surfaces — streaming chat, tool-calling UX, MCP integration, and design systems across React and React Native."
- **Prompt Engineer**: "Software Engineer and power user of Claude Code building agent-adjacent tooling, prompt scaffolding, and behavioral evaluations in TypeScript and Python."
- **Full-stack generalist**: "Software Engineer with 5+ years shipping consumer-facing web and mobile products across payments, ticketing, and AI integration."
- **Mobile / React Native**: "Software Engineer specializing in React Native and Expo — end-to-end feature ownership from design partnership through LaunchDarkly rollout on apps serving thousands of users."

### Step 4: Select and order bullets

Pick the strongest bullets that match the job. Rules:
- Playon section: 5–9 bullets. **Prefer 6–7 excellent bullets over 9 crowded ones.** Quality beats quantity; if you can't find 9 strong JD-relevant bullets, stop at 6 or 7.
- Carputty: 3 bullets max
- M&T Bank: 2 bullets max
- Reorder bullets within each section so the most relevant ones come first
- If the job has a specific domain (payments, trading, AI, etc.), lead with those bullets
- Cross-reference the points bank with the current resume to avoid missing strong bullets already in use
- Prefer outcome-driven phrasing (scope → outcome → mechanism) when the points bank has the numbers to support it

**Bullet linter — reject before writing:**
- Weak starters: "Helped," "Worked on," "Responsible for," "Assisted with," "Participated in," "Involved in," "Contributed to" (without specific contribution)
- Vague verbs: "Handled," "Managed" (unless leading people/budget), "Supported," "Maintained" (unless that's the actual scope)
- Buzzword stuffing without outcomes: "Leveraged synergies," "Drove impact," "Owned end-to-end" without concrete artifact
- Replace each with action + task + result (PAR pattern). Example: "Worked on the checkout flow" → "Rebuilt checkout flow in React Native, cutting drop-off rate from 12% to 4% over Q3."

### Step 5: Select projects

Pick 3 projects based on relevance to the job. Source projects from:
1. GitHub repos (prefer these for accurate, current descriptions)
2. The points bank or current resume (for projects not on GitHub)

**Default priority** (override only if the role is a poor fit for one of these):
1. **Kiyas** — lead project for any frontend / AI / dev-tools / design-system / MCP-adjacent role. Use the framing from `~/Documents/kiyas.md` and cite concrete metrics if available (npm installs, GitHub stars, Loom link).
2. **saif-claude-skills** — lead project for any agentic-tooling / prompt-eng / DX role.
3. **Miraya** — use for native / multimodal / iOS / image-pipeline roles. Honest framing: it's a SwiftUI iOS photo editor with a MetalPetal GPU pipeline, custom `CIColorKernel` shaders, fp16 working textures, non-destructive editing, and a read-only Instagram Graph API integration via `ASWebAuthenticationSession` with OAuth short→long-lived token exchange and refresh lifecycle. It does NOT publish to Instagram. Do not claim publishing or upload queues.
4. **FridgeChef** — reserve for LLM-integration / structured-output roles when Kiyas doesn't fit.

Write concise one-line descriptions. Include the tech stack and any notable metrics (stars, users, npm downloads).

### Step 6: Tailor skills (new format: grouped lines)

Skills must be presented as **four grouped lines**, not a flat tag cloud. Groups:
- **Languages**
- **Frameworks**
- **AI / LLMs**
- **Tooling**

Rules:
- Reorder within each group so the job's required technologies appear first.
- Mirror the job description's exact phrasing (e.g., "AI SDK, MCP, Anthropic API, OpenAI API, Claude Code").
- Don't list more than 6–8 items per group. Skills sections with 30+ technologies read as anxious, not experienced.
- Only list skills backed by experience bullets. If the job asks for something Saif doesn't have, leave it out rather than fake it.

Skills Saif can honestly claim across groups:
- **Languages**: TypeScript, JavaScript, Python, Swift, C#, SQL
- **Frameworks**: React, React Native, Next.js, Node.js, Expo, SwiftUI, ASP.NET Core
- **AI / LLMs**: Claude Code, MCP, Anthropic API, OpenAI API, Google Gemini, Prompt Engineering
- **Tooling**: Jest, LaunchDarkly, Stripe Terminal, AWS / EKS, PostgreSQL, GraphQL, REST APIs, CircleCI, Figma

### Step 7: Generate the PDF

Create an HTML file at `~/Documents/tailored-resume.html` using this exact CSS template:

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Saif Mirza - Resume</title>
<style>
  @page { size: letter; margin: 0.5in 0.55in; }
  * { margin: 0; padding: 0; box-sizing: border-box; }
  body { font-family: Arial, Helvetica, sans-serif; font-variant-ligatures: none; font-size: 10pt; line-height: 1.35; color: #2a2a2a; }
  .header { padding-bottom: 8px; border-bottom: 2px solid #2D8B5E; margin-bottom: 8px; }
  .header h1 { font-size: 22pt; font-weight: 700; color: #1a1a1a; letter-spacing: 0.5px; }
  .header .tagline { font-size: 10pt; color: #2D8B5E; font-weight: 500; margin-top: 1px; }
  .header .contact { margin-top: 6px; font-size: 9pt; color: #555; }
  .header .contact a { color: #555; text-decoration: none; }
  .header .contact span { margin-right: 10px; }
  .summary { font-size: 9.5pt; color: #333; line-height: 1.4; margin-bottom: 8px; padding: 0 1px; }
  .section { margin-bottom: 8px; }
  .section-title { font-size: 8.5pt; font-weight: 700; text-transform: uppercase; letter-spacing: 2px; color: #2D8B5E; padding-bottom: 4px; border-bottom: 1px solid #ddd; margin-bottom: 6px; }
  .skills-grouped { display: flex; flex-direction: column; gap: 3px; }
  .skill-row { font-size: 9pt; line-height: 1.4; color: #333; }
  .skill-label { font-weight: 700; color: #1a1a1a; display: inline-block; min-width: 76px; }
  .edu-row { display: flex; justify-content: space-between; font-size: 9.5pt; }
  .edu-row .school { font-weight: 600; }
  .edu-row .year { color: #777; font-size: 9pt; }
  .job { margin-bottom: 8px; }
  .job:last-child { margin-bottom: 0; }
  .job-header { display: flex; justify-content: space-between; align-items: baseline; margin-bottom: 4px; }
  .job-title { font-weight: 700; font-size: 10pt; color: #1a1a1a; }
  .job-company { font-weight: 400; color: #555; }
  .job-date { font-size: 8.5pt; color: #777; white-space: nowrap; }
  .job-bullets { padding-left: 14px; }
  .job-bullets li { margin-bottom: 1.5px; font-size: 9.5pt; line-height: 1.4; color: #333; }
  .project { margin-bottom: 3px; }
  .project:last-child { margin-bottom: 0; }
  .project-name { font-weight: 700; font-size: 9.5pt; color: #1a1a1a; display: inline; }
  .project-desc { font-size: 9pt; color: #555; display: inline; }
</style>
</head>
```

Use this header for every resume:
```html
<div class="header">
  <h1>Saif Mirza</h1>
  <div class="tagline">Software Engineer</div>
  <div class="contact">
    <span>Atlanta, GA</span>
    <span>917-244-3090</span>
    <span>saifalimirza@live.com</span>
    <span><a href="https://linkedin.com/in/saifmirza">linkedin.com/in/saifmirza</a></span>
    <span><a href="https://github.com/saiffmirza">github.com/saiffmirza</a></span>
    <span><a href="https://saifmirza.com">saifmirza.com</a></span>
  </div>
</div>
```

Immediately below the header, before the Skills section, insert the tailored summary from Step 3:
```html
<div class="summary">{{TAILORED SUMMARY LINE FROM STEP 3}}</div>
```

Skills section uses the grouped format:
```html
<div class="section">
  <div class="section-title">Skills</div>
  <div class="skills-grouped">
    <div class="skill-row"><span class="skill-label">Languages:</span> TypeScript, Python, JavaScript, Swift</div>
    <div class="skill-row"><span class="skill-label">Frameworks:</span> React, React Native, Next.js, Node.js, Expo</div>
    <div class="skill-row"><span class="skill-label">AI / LLMs:</span> Claude Code, MCP, Anthropic API, OpenAI API, Prompt Engineering</div>
    <div class="skill-row"><span class="skill-label">Tooling:</span> Jest, LaunchDarkly, Stripe Terminal, AWS / EKS, PostgreSQL</div>
  </div>
</div>
```

Education is always:
```html
<div class="edu-row">
  <span class="school">Syracuse University (Syracuse, New York) - B.Sc. Computer Science</span>
  <span class="year">2019</span>
</div>
```

Experience section format:
- Playon Sports: "Software Engineer II" / Apr 2023 - Present
- Carputty: "Software Engineer, Full-Stack" / Aug 2021 - Feb 2023
- M&T Bank: "Software Engineer" / Jul 2019 - Aug 2021

Bullet style:
- Every bullet should start with an action verb (no "I" pronoun, no "we" pronoun).
- Where possible, follow the scope → outcome → mechanism pattern.
- No em dashes. Use commas, colons, periods, or parentheses instead.

Convert to PDF using Chrome headless:
```bash
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless --disable-gpu --no-sandbox --print-to-pdf="$OUTPUT_PATH" --no-pdf-header-footer ~/Documents/tailored-resume.html
```

Do NOT delete `~/Documents/tailored-resume.html` yet. Keep it until Step 8 passes — it's the debug artifact if the PDF is wrong.

### Step 8: Verify

Check page count with macOS Spotlight metadata (no extra tooling required):
```bash
mdls -name kMDItemNumberOfPages "$OUTPUT_PATH"
```
Expected output: `kMDItemNumberOfPages = 1`. If `mdls` returns `(null)`, the index hasn't caught up — wait a second and re-run, or fall back to reading the PDF directly with the Read tool.

If it spills to two pages, tighten in this order, re-rendering after each step and re-checking page count:
1. Reduce summary to one line if it's two
2. Trim the weakest Playon bullet (down to a floor of 6)
3. Shorten the longest project description
4. Drop the weakest project (down to 2 projects minimum)
5. Trim a Carputty bullet (down to 2)
6. As a last resort, drop to 5 Playon bullets — flag this in the Step 9 critique as a forced trim and tell the user

Do NOT shrink fonts below the template defaults to fit content. The template is already at the floor of recommended sizes (10pt body, 9.5pt bullets). Trimming content is always preferred over shrinking type.

Never cut the summary entirely. Never drop below 2 projects. Never go below 5 Playon bullets. If the resume still won't fit after step 6, stop and tell the user which constraint is binding rather than silently shipping a two-page PDF.

**Parseability gate.** After page count passes, run the Read tool on the PDF and confirm the extracted text contains: (a) "Saif Mirza" and the contact line (verifies the header rendered), (b) the first verb of the lead Playon bullet, and (c) at least 3 of the JD's required-skill keywords. Do NOT check for the target company's name — it doesn't belong in the resume. If any of (a)–(c) are missing, the PDF didn't render text correctly (rasterized output, font substitution issue) — investigate before shipping. Chrome headless normally produces selectable text, so a failure here means something is wrong.

**Readability gate.** After parseability passes, sanity-check the layout: did the trim ladder force you to step 5 or 6 (Carputty trim or 5-bullet Playon)? Did spacing collapse below ~1.5 line-height anywhere? If yes to either, surface this in the Step 9 critique as "shipped near visual floor — consider whether less content would read stronger."

Once all gates pass, delete `~/Documents/tailored-resume.html`.

### Step 9: Self-critique against the JD

Before reporting success, evaluate the draft against the job description. This is the quality check the user sees, not internal reasoning. Produce a short critique with these parts, in this order:

1. **Stretch-role flag (if applicable).** If two or more required JD skills are missing from the resume, OR the JD asks for a seniority level above Software Engineer II, OR the JD's domain has no supporting evidence in Saif's history (e.g., "5 years of game dev"), open the critique with one sentence: "This role is a stretch because X. The strongest version of the resume for this JD is below, but the gap to flag is Y." If none of those triggers fire, skip this section.

2. **JD evidence map.** Take the top 5–7 requirements from the JD. For each, name the single strongest piece of evidence in the resume that supports it: summary, skills line, specific bullet (quote first 5 words), or specific project. If a hard requirement has NO evidence, mark it "MISSING" — do not soften this. This is the most important section; recruiters and ATS both scan for these mappings.

3. **Bullets cut.** List the 2–4 strongest bullets from the points bank or findings doc that were considered but did not make the page, and why each was cut (space, weaker JD fit, redundancy with another bullet). This surfaces whether the cut was correct or whether a kept bullet should be swapped out.

4. **Summary check.** Quote the summary line. State which JD phrases it mirrors and which it doesn't. If the JD has a dominant theme the summary doesn't lead with, flag it. Confirm the title used is honest (per the Step 3 guardrail).

5. **Bullet linter pass.** Confirm zero bullets start with "Helped," "Worked on," "Responsible for," "Assisted with," "Participated in," "Involved in," "Contributed to," or vague "Handled/Managed/Supported/Maintained." If any slipped through, list them and rewrite suggestions.

6. **Layout warnings (from Step 8 gates).** If the trim ladder forced step 5 or 6, or the readability gate fired, surface that here.

7. **Weakest link.** One sentence on the part of the resume least likely to land for this specific JD (e.g., "no production payments experience and the JD opens with payments," or "skills group lists Gemini but no bullet substantiates it").

8. **Gap remediation.** For each "MISSING" item from the JD evidence map AND the weakest link, propose one concrete close-the-gap move that's realistic in days-to-weeks (not months). Tie to existing assets where possible. The bar is *specific and actionable*, not aspirational. Examples by gap type:
   - **Domain (e.g., crypto, fintech, gamedev)**: "ship one PR to a Solana program-examples repo," "add a Web3-themed example to Kiyas," "write a build-log post on dev.to about a small wallet-flow prototype"
   - **Surface (e.g., browser extension, native iOS, CLI)**: "ship a small MV3 + React + Vite extension to your portfolio (one weekend)," "publish a Swift Package extracted from Miraya"
   - **Tech (e.g., Rust, Go, Kafka)**: "do the official tutorial and commit a working sample to a public repo," "add it as a CI step in saif-claude-skills or Kiyas"
   - **Scale/system (e.g., realtime, observability, multi-region)**: "extend Kiyas with a TradingView-style live-data demo," "add OpenTelemetry instrumentation to one of your repos and write up the trace"
   - **Skip remediation entirely** if the gap is structural (years of experience, degree mismatch, vertical-specific years). Don't fake a fix.

Keep the critique under ~400 words total. Plain prose, no scores out of 10, no rubric tables.

## Output

Save the PDF as `~/Documents/SaifMirza-[CompanyName].pdf` where CompanyName is extracted from the job description.

Tell the user:
- Where the file is saved
- What tailoring choices you made (summary wording, bullet reordering, skills emphasis, project selection)
- The Step 9 self-critique in full
