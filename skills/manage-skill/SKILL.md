---
name: manage-skill
description: Create, modify, and maintain Claude Code skills
user-invocable: true
disable-model-invocation: false
allowed-tools: Bash(mkdir *), Read, Write, Edit, Glob, Grep, AskUserQuestion
---

# Skill Manager

Manage skills in this repository. All skills are stored under `~/.claude/skills/` (symlinked from repo).

## Action

$ARGUMENTS

If no arguments provided, list all existing skills and ask what to do.

## Skill Directory Structure

Each skill is a directory with a required `SKILL.md`:

```
~/.claude/skills/{skill-name}/
├── SKILL.md           # Required: YAML frontmatter + instructions
└── *.md               # Optional: supporting reference files
```

## SKILL.md Format

```yaml
---
name: my-skill                        # Display name (defaults to directory name)
description: One-line description     # Shown in skill list, required
user-invocable: true                  # User can invoke with /skill-name (default: true)
disable-model-invocation: true        # Prevent Claude from auto-invoking (default: false)
allowed-tools: Read, Write, Edit      # Comma-separated tools this skill can use
---

Skill instructions in markdown...
Use $ARGUMENTS to accept user input after the slash command.
```

### Frontmatter Fields

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| name | string | dir name | Skill display name |
| description | string | **required** | One-line description for skill list |
| user-invocable | bool | true | User can invoke with `/skill-name` |
| disable-model-invocation | bool | false | Prevent Claude from auto-invoking |
| allowed-tools | string | — | Comma-separated list of allowed tools |

### Common allowed-tools Values

- `Bash` — shell commands (scoped: `Bash(git status:*)`, `Bash(uv:*)`)
- `Read`, `Write`, `Edit` — file operations
- `Glob`, `Grep` — file search
- `AskUserQuestion` — interactive prompts

### Including Supporting Files

To inline a sibling file into the skill prompt, use the exclamation-backtick syntax:
the exclamation mark, then a backtick-wrapped cat command pointing to the file path.

The file path should use the repo's actual path (not ~/.claude/skills/) to avoid sandbox restrictions.
Example: the repo path followed by /skills/scaffold/reference.md

Use this to keep SKILL.md focused while storing large reference data in separate files.

## Conventions

1. Directory names use **kebab-case**
2. One skill, one responsibility
3. Use `disable-model-invocation: true` for action skills (create files, run commands, commit)
4. Use `$ARGUMENTS` for user input
5. Keep SKILL.md concise; extract large reference data to supporting `.md` files
6. Use `user-invocable: false` for skills Claude should auto-detect (e.g., coding conventions)

## Operations

### Create

1. Ask for: skill name, purpose, whether user-invocable or model-invocable
2. `mkdir ~/.claude/skills/{name}/`
3. Write `SKILL.md` with frontmatter + instructions
4. Add supporting files if needed

### Edit

1. Read `~/.claude/skills/{name}/SKILL.md`
2. Understand the requested change
3. Edit the file

### List

1. Find all `~/.claude/skills/*/SKILL.md`
2. Show each skill's name and description

### Delete

1. **Always confirm** with user before deleting
2. Remove the skill directory
