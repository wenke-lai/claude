---
name: nuxt-ui
description: Setup and develop with Nuxt UI — install, build pages, components, and UI/UX
user-invocable: true
disable-model-invocation: false
allowed-tools: Bash, Read, Write, Edit, Glob, AskUserQuestion
---

# Nuxt UI

Setup, develop, and build UI/UX with Nuxt UI. This skill covers both initial installation and ongoing development (pages, views, components, layouts, etc.).

## Package Manager: pnpm

All packages must be managed via `pnpm add` / `pnpm add -D`. Do NOT edit `package.json` directly then run install.

## Prerequisite

A Nuxt project must already exist. If `nuxt.config.ts` is not found, inform the user to run the **vue** skill first and stop.

## Documentation Reference

When working with Nuxt UI components (building pages, creating components, developing UI/UX), consult:
- Quick reference: https://ui.nuxt.com/llms.txt
- Full guidelines: https://ui.nuxt.com/llms-full.txt

Use `WebFetch` to read these for component usage, props, slots, theming, etc.

## Steps

1. Check that `nuxt.config.ts` exists. If not, stop and tell user to use `/vue` first.

2. Install dependencies:

```bash
pnpm add -D @nuxt/ui tailwindcss
```

3. Update `nuxt.config.ts` — add `@nuxt/ui` to modules, add `css` for tailwind:

```typescript
export default defineNuxtConfig({
  compatibilityDate: "2025-01-01",
  devtools: { enabled: false },
  modules: ["@nuxt/ui"],
  css: ["~/assets/css/main.css"],
});
```

Preserve any existing config and merge — do NOT overwrite the entire file.

4. Create `assets/css/main.css` (if not exists):

```css
@import "tailwindcss";
```

5. Update `app.vue` — wrap content with `UApp`:

```vue
<template>
  <UApp>
    <NuxtLayout>
      <NuxtPage />
    </NuxtLayout>
  </UApp>
</template>
```

6. Create `app.config.ts` with icon configuration:

```typescript
export default defineAppConfig({
  ui: {
    icons: {
      arrowDown: "i-tabler-arrow-down",
      arrowLeft: "i-tabler-arrow-left",
      arrowRight: "i-tabler-arrow-right",
      arrowUp: "i-tabler-arrow-up",
      caution: "i-tabler-alert-square-rounded",
      check: "i-tabler-check",
      chevronDoubleLeft: "i-tabler-chevrons-left",
      chevronDoubleRight: "i-tabler-chevrons-right",
      chevronDown: "i-tabler-chevron-down",
      chevronLeft: "i-tabler-chevron-left",
      chevronRight: "i-tabler-chevron-right",
      chevronUp: "i-tabler-chevron-up",
      close: "i-tabler-x",
      copy: "i-tabler-copy",
      copyCheck: "i-tabler-copy-check",
      dark: "i-tabler-moon",
      drag: "i-tabler-grip-vertical",
      ellipsis: "i-tabler-dots",
      error: "i-tabler-square-rounded-x",
      external: "i-tabler-external-link",
      eye: "i-tabler-eye",
      eyeOff: "i-tabler-eye-off",
      file: "i-tabler-file",
      folder: "i-tabler-folder",
      folderOpen: "i-tabler-folder-open",
      hash: "i-tabler-hash",
      info: "i-tabler-info-square-rounded",
      light: "i-tabler-sun",
      loading: "i-tabler-loader-2",
      menu: "i-tabler-menu",
      minus: "i-tabler-minus",
      panelClose: "i-tabler-layout-sidebar-left-collapse",
      panelOpen: "i-tabler-layout-sidebar-left-expand",
      plus: "i-tabler-plus",
      reload: "i-tabler-reload",
      search: "i-tabler-search",
      stop: "i-tabler-player-stop",
      success: "i-tabler-square-rounded-check",
      system: "i-tabler-device-desktop",
      tip: "i-tabler-bulb",
      upload: "i-tabler-upload",
      warning: "i-tabler-alert-triangle",
    },
  },
});
```

7. Show a summary of what was set up.
