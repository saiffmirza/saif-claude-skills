---
name: explain
description: After writing or modifying code, provide a detailed breakdown of what was added, new concepts to research, and hands-on challenges.
---

# /explain — Learn What Was Built

After writing or modifying code, provide a detailed breakdown so the user understands what was added and what to research further.

## When to use
- Automatically after any significant code generation, new file creation, or feature implementation
- User invokes `/explain` to get a breakdown of the most recent changes

## Steps

1. **Identify what changed:**
   - Review all files created or modified in the current session
   - Group changes by category (new files, modified files, new dependencies)

2. **For each significant change, explain:**

   **What it does (plain English):**
   - What problem does this code solve?
   - How does it fit into the larger project?
   - What would happen if this file/function didn't exist?

   **How it works (technical breakdown):**
   - Walk through the key logic step by step
   - Explain non-obvious patterns (e.g., "this is the provider pattern", "this is a custom hook", "this uses server components")
   - Call out any design decisions and why they were made over alternatives

   **New concepts introduced:**
   - List any patterns, APIs, or techniques that appeared for the first time in this project
   - For each concept, provide:
     - A one-sentence explanation
     - Why it was used here
     - A specific thing to search/read to understand it deeper (e.g., "Read the React docs section on `useMemo` — focus on when it actually helps vs. premature optimization")

3. **New dependencies added:**
   - For each new package installed, explain:
     - What it does and why it was chosen
     - What the alternative options were
     - One thing worth reading in its docs (link a specific section if possible)

4. **Concepts to research for deeper understanding:**
   - List 3-5 focused topics the user should look into based on what was built
   - For each topic, provide:
     - The concept name
     - Why it matters (not just "it's important" — explain the real-world consequence of not understanding it)
     - A concrete learning action (e.g., "Try removing the `useMemo` wrapper and see what happens to re-renders in React DevTools")

5. **Challenge prompts:**
   - Suggest 2-3 small modifications the user could try making on their own to test understanding
   - These should be achievable in 15-30 minutes without AI help
   - Example: "Try adding a new section to the landing page with its own scroll animation — you'll need to use the same Framer Motion pattern from the About section"

## Format

Use this structure for the output:

```
## What was built

[Brief summary of all changes]

## Breakdown

### [File or feature name]
**What:** [plain English explanation]
**How:** [technical walkthrough]
**New concepts:** [list with explanations]

### [Next file or feature]
...

## New dependencies
| Package | Why it's here | Worth reading |
|---------|--------------|---------------|
| ...     | ...          | ...           |

## Go deeper
1. **[Concept]** — [Why it matters]. Try: [concrete action].
2. ...

## Try it yourself
1. [Challenge 1]
2. [Challenge 2]
3. [Challenge 3]
```

## Important
- Don't be surface-level. "This is a React component" is useless. Explain *what kind* of component pattern it uses and *why*.
- Prioritize concepts the user is likely encountering for the first time based on their stack (React, React Native, TypeScript, Node.js)
- Be honest about complexity — if something is genuinely advanced (e.g., Three.js shader materials), say so and suggest a learning path rather than oversimplifying
- Don't overwhelm — if 20 files were changed, group related files and explain the pattern once, not per-file
- The goal is to make the user a better engineer, not just a faster one
