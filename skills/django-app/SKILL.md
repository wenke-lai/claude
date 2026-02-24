---
name: django-app
description: Create a Django app with model and CRUD APIs using django-ninja
user-invocable: true
disable-model-invocation: false
allowed-tools: Bash, Read, Write, Edit, Glob
---

# Django App Scaffold

Create a new Django app with model and CRUD APIs following a fixed architecture pattern.

## Architecture Reference

!`cat /Users/wenke.lai/Repositories/wenke-lai/claude/skills/django-app/django-app-pattern.md`

## Task

Input: $ARGUMENTS

Parse the user's request to determine:
- **App name** (e.g., "fund")
- **Model name** (e.g., "Fund")
- **Model fields** (from the description)

**Do NOT ask any questions.** Infer everything from the input. If fields are not specified, create sensible defaults based on the model name (e.g., `name`, `description`, timestamps).

## Steps

1. Read `server/settings.py` and `server/apis.py` to understand the current project state
2. Create the app with `uv run python manage.py startapp {app_name} apps/{app_name}`
3. Apply the **Architecture Reference** exactly:
   - Update `apps/{app_name}/apps.py` (set `name = "apps.{app_name}"`)
   - Write `apps/{app_name}/models.py`
   - Create `apps/{app_name}/schemas.py`
   - Create `apps/{app_name}/services.py`
   - Create `apps/{app_name}/apis.py`
   - Write `apps/{app_name}/admin.py`
   - Write `apps/{app_name}/tests.py`
4. Register in `server/settings.py`: add `"apps.{app_name}"` under `# Applications`
5. Register in `server/apis.py`: use string import `api.add_router("/{app_name}s/", "apps.{app_name}.apis.router")`
6. Check if `server/settings.py` has `CACHE_CONTROL` — if yes, add `@decorate_view(cache_control(**settings.CACHE_CONTROL))` to list/retrieve endpoints
7. Run `uv run python manage.py makemigrations && uv run python manage.py migrate`
8. Run `make test` to verify
9. Show a summary of what was created
