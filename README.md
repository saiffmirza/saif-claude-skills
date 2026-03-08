# saif-claude-skills

Custom skills for [Claude Code](https://claude.com/claude-code).

## Skills

| Skill | Description |
|-------|-------------|
| `/e2e` | Analyze any project and generate Playwright end-to-end tests automatically |

## Setup

To use these skills, add them to your Claude Code configuration:

```bash
# From your project directory
claude config add skills /path/to/saif-claude-skills/skills/
```

Or symlink individual skills:

```bash
mkdir -p .claude/skills
ln -s /Users/saifmirza/saif-claude-skills/skills/e2e.md .claude/skills/e2e.md
```

## Usage

In any project, just run:

```
/e2e
```

Claude will analyze your project, identify screens/routes/auth, and generate Playwright tests in a `tests/` directory with a config file.
