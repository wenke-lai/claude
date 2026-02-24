---
name: python
description: Scaffold a new Python project with uv and ruff
user-invocable: true
disable-model-invocation: false
allowed-tools: Bash, Read, Write, Edit, Glob, AskUserQuestion
---

# Python Project Scaffold

Create a bare Python project with uv, ruff, Makefile, and .gitignore.

## Task

Project name: $ARGUMENTS

**Only ask for the project name if not provided. No other questions.**

## Steps

1. Initialize project:

```bash
uv init {project_name}
cd {project_name}
rm hello.py
```

2. Add dev dependencies:

```bash
uv add --dev ruff
```

3. Configure pyproject.toml:

```toml
[tool.ruff]
target-version = "py312"
line-length = 120

[tool.ruff.lint]
select = ["E", "W", "F", "I", "B", "UP"]

[tool.ruff.lint.isort]
known-first-party = ["{project_name}"]
```

4. Fetch .gitignore:

```bash
curl -fsSL https://raw.githubusercontent.com/github/gitignore/main/Python.gitignore -o .gitignore
```

6. Create Makefile:

```makefile
.DEFAULT_GOAL := help
PYTHON = uv run

help: ## Show available commands
	@grep -E '^[a-zA-Z_-]+:.*?## .*$$' $(MAKEFILE_LIST) | awk 'BEGIN {FS = ":.*?## "}; {printf "\033[36m%-20s\033[0m %s\n", $$1, $$2}'

format: ## Format code with ruff
	$(PYTHON) ruff format .

lint: ## Lint code with ruff
	$(PYTHON) ruff check . --fix
```

7. Verify: `make format`

8. `git init && git add .` (do NOT commit)

9. Show a summary of what was created
