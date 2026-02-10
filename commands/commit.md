---
description: Generate a commit message from staged changes (ask before committing)
allowed-tools: Bash(git status:_), Bash(git diff:_), Bash(git log:_), Bash(git commit:_)
---

## Context

- git status:
  !`git status`

- staged diff:
  !`git diff --cached`

- recent commits:
  !`git log --oneline -10`

## Task

1. Propose ONE commit message (prefer Conventional Commits: feat/fix/refactor/chore/docs/test/build).
2. Keep the subject line <= 72 chars, imperative mood.
3. Do NOT add any AI attribution (e.g. "Generated with ...")
4. Ask me to confirm the final message.
5. Only after I confirm, run: `git commit -m "<message>"`.

## Example

`feat(cms): add page management system with tree structure`

## !!IMPORTANT!!

When to use refactor:

Refactoring is strictly for internal structural changes with no change in external behavior. The inputs, outputs,
functionality, and user-visible results remain identical — only the internal implementation differs.

Valid examples:

- Extract shared function/component when behavior is already identical across all call sites
- Rename variables/files
- Move code between files or reorganize directory structure
- Eliminate code duplication

When NOT to use refactor:

- Adding behavior that didn't exist before → feat (e.g., adding breadcrumbs to pages that had none)
- Fixing incorrect existing behavior → fix (e.g., breadcrumbs missing the Home link)
- Mixed: both new behavior and structural changes → use feat or fix based on the primary behavioral change
