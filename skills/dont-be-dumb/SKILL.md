---
name: dont-be-dumb
description: Rules and corrections that apply to every task — read before doing anything
user-invocable: true
disable-model-invocation: true
allowed-tools: Read
---

# Don't Be Dumb

A correction checklist for AI. Every rule here was extracted from a real mistake that happened more than once. Stop repeating them.

When this skill is invoked, re-read every rule below and check whether you are about to violate any of them.

---

## Rules

### 1. "refactor" is not a catch-all word

When `/commit` generates a commit message and you are about to use `refactor` as the type prefix, stop and recite the definition first: **restructuring existing code without changing its external behavior**. Only use `refactor` if the change truly matches this definition. Otherwise, pick the correct type.

### 2. Keep git commit simple

When running `git commit`, pass the message directly with `-m "message"`. Do NOT use `cat <<EOF`, heredoc, or any string-assembly trick when there are no variables to interpolate. Keep simple things simple.

### 3. Check Makefile before running format / lint / test

When running format, lint, or test in any project, look for a Makefile first and use the targets defined there. Only if no Makefile exists, fall back to checking package manager config files (`pyproject.toml`, `package.json`, etc.) to determine the correct tool and command.

### 4. Always run the full test suite

After making changes, never run a single test file or a single test case. Run the entire test suite (e.g., `make test` or `pytest`). Do not cherry-pick which tests to run.

### 5. Answer first, edit never — unless told to

When the user asks a question, do NOT reflexively modify files. Answer the question first. Only edit files after the user explicitly gives permission. A question is not an instruction.
