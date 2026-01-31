# Claude Code Commands

A collection of custom command specifications for [Claude Code](https://github.com/anthropics/claude-code), Anthropic's official CLI for Claude.

## Overview

This repository provides reusable command templates that extend Claude Code's capabilities with pre-configured instructions for automating common development workflows.

## Commands

### commit

Generates commit messages from staged changes following the [Conventional Commits](https://www.conventionalcommits.org/) specification.

**Features:**

- Analyzes staged changes using `git diff --cached`
- Generates messages with proper type prefixes (feat, fix, refactor, chore, docs, test, build)
- Enforces 72-character subject line limit
- Uses imperative mood
- Requires confirmation before committing

**Usage:**

```
/commit
```

### fix-github-issue

Automates the workflow for addressing GitHub issues from analysis to PR creation.

**Features:**

- Fetches and analyzes issue details via GitHub CLI
- Creates feature branches with naming convention: `feat/issue-{number}-{description}`
- Searches codebase and implements changes
- Runs tests and linting
- Creates commits and pull requests

**Usage:**

```
/fix-github-issue <issue-number>
```

## Installation

1. Clone this repository or copy the `commands/` directory to your project
2. Claude Code will automatically detect commands in the `commands/` directory

## License

MIT
