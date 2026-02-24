---
name: vue
description: Scaffold a new Nuxt project with pnpm and Tailwind CSS
user-invocable: true
disable-model-invocation: false
allowed-tools: Bash, Read, Write, Edit, Glob, AskUserQuestion
---

# Nuxt Project Scaffold

## Package Manager: pnpm

All packages must be managed via `pnpm add` / `pnpm add -D`. Do NOT edit `package.json` directly then run install.

## Task

Project name: $ARGUMENTS

**Only ask for the project name if not provided. No other questions.**

## Steps

1. Create Nuxt project:

```bash
pnpm create nuxt@latest {project_name}
```

During setup: select **pnpm**, skip Nuxt DevTools.

2. Install Tailwind CSS:

```bash
cd {project_name}
pnpm add -D tailwindcss
```

3. Create `assets/css/main.css`:

```css
@import "tailwindcss";
```

4. Update `nuxt.config.ts`:

```typescript
export default defineNuxtConfig({
  compatibilityDate: "2025-01-01",
  devtools: { enabled: false },
  css: ["~/assets/css/main.css"],
});
```

6. Write `app.vue`:

```vue
<template>
  <NuxtLayout>
    <NuxtPage />
  </NuxtLayout>
</template>
```

7. Create `layouts/default.vue`:

```vue
<template>
  <div>
    <slot />
  </div>
</template>
```

8. Create `pages/index.vue`:

```vue
<template>
  <h1 class="text-2xl font-bold">Hello World</h1>
</template>
```

9. Create Makefile:

```makefile
.DEFAULT_GOAL := help

help: ## Show available commands
	@grep -E '^[a-zA-Z_-]+:.*?## .*$$' $(MAKEFILE_LIST) | awk 'BEGIN {FS = ":.*?## "}; {printf "\033[36m%-20s\033[0m %s\n", $$1, $$2}'

dev: ## Run development server
	pnpm dev

build: ## Build for production
	pnpm build

preview: ## Preview production build
	pnpm preview
```

10. `git init && git add .` (do NOT commit)

11. Show a summary of what was created
