---
name: tailor-resume
description: Generate a tailored resume PDF for a specific job posting. Takes a job description and produces a one-page PDF highlighting the most relevant experience.
argument-hint: <paste the job description or provide a file path>
---

# Tailor Resume

Generate a one-page tailored resume PDF from a job description.

## Context

The user maintains a resume points bank at `~/Documents/playon-resume-points.md` containing all quantified accomplishments from their career, organized by project/feature. Their general resume PDF is at `~/portfolio/public/SaifMirzaResume.pdf`.

## Inputs

The job description is provided via `$ARGUMENTS`. If it's a file path, read the file first.

## Process

### Step 1: Analyze the job description

Identify:
- Required skills and technologies (exact matches to highlight)
- Nice-to-have skills
- Key themes (e.g., payments, mobile, infrastructure, AI, security, trading)
- Seniority signals (years of experience, leadership expectations)

### Step 2: Gather all source material

Read ALL of these to get the full picture:

1. **Resume points bank**: `~/Documents/playon-resume-points.md` (all quantified accomplishments)
2. **Current general resume**: `~/portfolio/public/SaifMirzaResume.pdf` (what's currently being used)
3. **Portfolio experience data**: `~/portfolio/src/lib/experience.ts` (website experience section)
4. **GitHub repos**: Run `gh repo list saiffmirza --limit 20 --json name,description,primaryLanguage,stargazerCount,url` to get the latest public projects with real descriptions, languages, and stars

Use the GitHub data to write accurate, up-to-date project descriptions rather than relying on stale hardcoded text. If a repo is relevant to the job and not in the points bank, include it.

### Step 3: Select and order bullets

Pick the strongest bullets that match the job. Rules:
- Playon section should have the most bullets (current role, 3 years)
- Carputty: 3-4 bullets max, pick only what's relevant
- M&T Bank: 2-3 bullets max, pick only what's relevant
- Reorder bullets within each section so the most relevant ones come first
- If the job has a specific domain (payments, trading, AI, etc.), lead with those bullets
- Cross-reference the points bank with the current resume to avoid missing strong bullets already in use

### Step 4: Select projects

Pick 3 projects based on relevance to the job. Source projects from:
1. GitHub repos (prefer these for accurate, current descriptions)
2. The points bank or current resume (for projects not on GitHub)

Write concise one-line descriptions. Include the tech stack and any notable metrics (stars, users, npm downloads).

### Step 5: Tailor skills

Reorder the skills list so the job's required technologies appear first. Add relevant skills, remove irrelevant ones. Don't list skills you can't back up with experience bullets.

### Step 6: Generate the PDF

Create an HTML file at `~/Documents/tailored-resume.html` using this exact CSS template:

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Saif Mirza - Resume</title>
<style>
  @page { size: letter; margin: 0.4in 0.5in; }
  * { margin: 0; padding: 0; box-sizing: border-box; }
  body { font-family: Arial, Helvetica, sans-serif; font-variant-ligatures: none; font-size: 9pt; line-height: 1.35; color: #2a2a2a; }
  .header { padding-bottom: 8px; border-bottom: 2px solid #2D8B5E; margin-bottom: 10px; }
  .header h1 { font-size: 22pt; font-weight: 700; color: #1a1a1a; letter-spacing: 0.5px; }
  .header .tagline { font-size: 9.5pt; color: #2D8B5E; font-weight: 500; margin-top: 1px; }
  .header .contact { margin-top: 6px; font-size: 8.5pt; color: #555; }
  .header .contact a { color: #555; text-decoration: none; }
  .header .contact span { margin-right: 10px; }
  .section { margin-bottom: 8px; }
  .section-title { font-size: 8pt; font-weight: 700; text-transform: uppercase; letter-spacing: 2px; color: #2D8B5E; padding-bottom: 4px; border-bottom: 1px solid #ddd; margin-bottom: 6px; }
  .skills { display: flex; flex-wrap: wrap; gap: 5px; }
  .skills span { font-size: 8pt; background: #f3f3f0; padding: 2px 8px; border-radius: 3px; color: #333; }
  .edu-row { display: flex; justify-content: space-between; font-size: 9pt; }
  .edu-row .school { font-weight: 600; }
  .edu-row .year { color: #777; font-size: 8.5pt; }
  .job { margin-bottom: 8px; }
  .job:last-child { margin-bottom: 0; }
  .job-header { display: flex; justify-content: space-between; align-items: baseline; margin-bottom: 4px; }
  .job-title { font-weight: 700; font-size: 9.5pt; color: #1a1a1a; }
  .job-company { font-weight: 400; color: #555; }
  .job-date { font-size: 8pt; color: #777; white-space: nowrap; }
  .job-bullets { padding-left: 14px; }
  .job-bullets li { margin-bottom: 1.5px; font-size: 8.5pt; line-height: 1.4; color: #333; }
  .project { margin-bottom: 3px; }
  .project:last-child { margin-bottom: 0; }
  .project-name { font-weight: 700; font-size: 9pt; color: #1a1a1a; display: inline; }
  .project-desc { font-size: 8.5pt; color: #555; display: inline; }
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

Education is always:
```html
<div class="edu-row">
  <span class="school">Syracuse University (Syracuse, New York) - B.Sc. Computer Science</span>
  <span class="year">2019</span>
</div>
```

Experience section format:
- Playon Sports: "Software Engineer" / Apr 2023 - Present
- Carputty: "Software Engineer, Full-Stack" / Aug 2021 - Feb 2023
- M&T Bank: "Software Engineer" / Jul 2019 - Aug 2021

Then convert to PDF using Chrome headless:
```bash
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless --disable-gpu --no-sandbox --print-to-pdf="$OUTPUT_PATH" --no-pdf-header-footer ~/Documents/tailored-resume.html
```

Do NOT delete `~/Documents/tailored-resume.html` yet. Keep it until Step 7 passes — it's the debug artifact if the PDF is wrong.

### Step 7: Verify

Check page count with macOS Spotlight metadata (no extra tooling required):
```bash
mdls -name kMDItemNumberOfPages "$OUTPUT_PATH"
```
Expected output: `kMDItemNumberOfPages = 1`. If `mdls` returns `(null)`, the index hasn't caught up — wait a second and re-run, or fall back to reading the PDF directly.

If it spills to two pages, tighten in this order, re-rendering after each step and re-checking page count:
1. Trim the weakest Playon bullet (down to a floor of 7)
2. Shorten the longest project description
3. Drop the weakest project (down to 2 projects minimum)
4. Trim a Carputty bullet (down to 2)
5. As a last resort, drop to 6 Playon bullets — flag this in the Step 8 critique as a forced trim and tell the user

Never drop below 2 projects. If the resume still won't fit after step 5, stop and tell the user which constraint is binding rather than silently shipping a two-page PDF.

Once verification passes, delete `~/Documents/tailored-resume.html`.

### Step 8: Self-critique against the JD

Before reporting success, evaluate the draft against the job description. This is the quality check the user sees, not internal reasoning. Produce a short critique with these four parts:

1. **Keyword coverage.** List the required skills/technologies from the JD. For each, mark whether it appears in the resume (and where: skills, bullet, project) or is missing. If something required is missing, say so plainly rather than glossing over it.

2. **Bullets cut.** List the 2-4 strongest bullets from the points bank that were considered but did not make the page, and why each was cut (space, weaker JD fit, redundancy with another bullet). This is the most useful part: it surfaces whether the cut was correct or whether a kept bullet should be swapped out.

3. **Skills check.** Note which JD-required technologies the skills section leads with vs. buries. If the JD has a dominant theme not reflected up front, flag it.

4. **Weakest link.** One sentence on the part of the resume least likely to land for this specific JD. Be honest. If the user's background is genuinely a stretch for the role, say that.

Keep the critique under ~200 words total. Plain prose, no scores out of 10, no rubric tables.

## Output

Save the PDF as `~/Documents/SaifMirza-[CompanyName].pdf` where CompanyName is extracted from the job description.

Tell the user:
- Where the file is saved
- What tailoring choices you made (bullet reordering, skills emphasis, project selection)
- The Step 8 self-critique in full
