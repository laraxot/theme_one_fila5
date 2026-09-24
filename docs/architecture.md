---
title: "One Theme Architecture"
type: architecture
tags: [theme, architecture, one]
created: 2026-08-04
updated: 2026-08-04
---
# One Theme — Architecture

## Purpose
One theme architecture and design patterns for Laraxot PTVX.

## Core Components

**Views:**
- Blade templates for base layouts
- Component-based structure

**Assets:**
- Vite build pipeline
- Tailwind CSS compilation

**Providers:**
- ThemeServiceProvider registration

## Quality Gates
- Build passes without errors
- Components render correctly
- Performance optimized

---

<!-- Merged from ARCHITECTURE.md, which collided with this file on case-insensitive filesystems. -->

---
title: "One Theme Architecture"
type: architecture
tags: [theme, architecture, one, frontend]
created: 2026-08-04
updated: 2026-08-04
---
# One Theme — Architecture

## Purpose
Minimal theme skeleton for future frontend development and customization

## Core Components

**Views:**
- Blade templates for One-specific layouts
- Component-based structure
- Filament integration patterns

**Assets:**
- Vite-based build pipeline
- CSS/JS compilation with Tailwind

**Providers:**
- `OneThemeServiceProvider` — Theme registration
- View namespace configuration

## Design Decisions

| Decision | Rationale |
|----------|-----------|
| Blade templates | Laravel-native, component-friendly |
| Tailwind utility-first | Rapid, consistent styling |
| Vite bundler | Fast HMR, optimized builds |

## Integration Points
**Depends On:** Laravel, Blade, Tailwind CSS, Vite
**Active Theme:** Applied system-wide or tenant-specific

## Quality Gates
- **Build**: npm run build passes
- **Lint**: Tailwind/Pug linter checks
- **Preview**: Theme renders correctly in browser
