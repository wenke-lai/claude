---
name: django-project
description: Scaffold a new Django project with django-ninja, django-environ, and CORS
user-invocable: true
disable-model-invocation: false
allowed-tools: Bash, Read, Write, Edit, Glob, AskUserQuestion
---

# Django Project Scaffold

## Architecture Reference

!`cat /Users/wenke.lai/Repositories/wenke-lai/claude/skills/django-project/django-project-pattern.md`

## Task

Project name: $ARGUMENTS

**Only ask for the project name if not provided. No other questions.**

## Steps

1. If no project name given, ask for one
2. Apply the **Architecture Reference** exactly, step by step
3. After scaffolding, run `make format` and `make test` to verify
4. Run `git init && git add .` (do NOT commit)
5. Show a summary of what was created
