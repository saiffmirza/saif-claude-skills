# saif-claude-skills

Custom skills for [Claude Code](https://claude.com/claude-code).

## Skills

| Skill | Description |
|-------|-------------|
| `/e2e` | Analyze any project and generate Playwright end-to-end tests automatically |
| `/explain` | Get a detailed breakdown of what was built, new concepts to research, and hands-on challenges |
| `/tailor-resume` | Generate a one-page tailored resume PDF from a job description |

## Installation

Clone this repo and copy the skills to your user-level Claude Code skills directory. This makes them available globally across all your projects.

```bash
# Clone the repo
git clone https://github.com/saiffmirza/saif-claude-skills.git

# Create the skill directories
mkdir -p ~/.claude/skills/e2e ~/.claude/skills/explain

# Copy each skill
cp saif-claude-skills/skills/e2e.md ~/.claude/skills/e2e/SKILL.md
cp saif-claude-skills/skills/explain.md ~/.claude/skills/explain/SKILL.md
```

The key is the directory structure — each skill needs its own folder with a `SKILL.md` file:

```
~/.claude/skills/
├── e2e/
│   └── SKILL.md
└── explain/
    └── SKILL.md
```

### Updating

When new skills are added, pull the latest and copy any new files:

```bash
cd saif-claude-skills
git pull

# Copy all skills at once
for skill in skills/*.md; do
  name=$(basename "$skill" .md)
  mkdir -p ~/.claude/skills/"$name"
  cp "$skill" ~/.claude/skills/"$name"/SKILL.md
done
```

## Usage

Once installed, these skills are available in any Claude Code session. Just type:

```
/e2e        # Generate Playwright tests for your project
/explain    # Get a learning breakdown of recent code changes
```

## Contributing

Each skill is a single markdown file in `skills/`. To add a new skill:

1. Create `skills/your-skill-name.md` with the skill instructions
2. Add it to the table above
3. Copy it to `~/.claude/skills/your-skill-name/SKILL.md` for local use
