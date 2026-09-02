---
title: "One Theme — Mappa Graphify"
type: guide
tags: [theme, one, graphify]
created: 2026-08-02
updated: 2026-08-02
qmd: "one theme one theme   mappa graphify"
---
# One Theme — Mappa Graphify

**Versione:** 1.0.0 | **Tema:** One | **Data:** 2026-08-02

---

## 📌 Cosa fa il tema One

Il tema **One** fornisce:
- Tema UI primario per portale e dashboard con componenti hero, sidebar, stats e testimonial

---

## 🏗️ Architettura Essenziale Tema

### Entry Points Visivi

| Tipo | File | Path |
|------|------|------|
| **View Layout** | `layouts/app.blade.php` | `resources/views/layouts/app.blade.php` |
| **View Layout** | `pages/home.blade.php` | `resources/views/pages/home.blade.php` |
| **View Layout** | `pages/index.blade.php` | `resources/views/pages/index.blade.php` |
| **Component** | `blocks/hero/main.blade.php` | `resources/views/components/blocks/hero/main.blade.php` |
| **Component** | `blocks/stats/overview.blade.php` | `resources/views/components/blocks/stats/overview.blade.php` |
| **Component** | `blocks/features/grid.blade.php` | `resources/views/components/blocks/features/grid.blade.php` |

### Dependencies (Incoming)

```
UI Module → Theme One (rendering componenti)
```

### Dependencies (Outgoing)

```
Theme One → Tailwind CSS
Theme One → Alpine.js
```

---

## 📊 Grafo Locale (Query Rapide Tema)

### Scoprire Componenti Tema

```bash
graphify query "One theme components and layouts"
```

### Tracciare Dipendenze CSS/Vite

```bash
graphify query "One theme CSS assets and dependencies"
```

---

## 🎯 Task Comuni Tema + Graphify

### Task 1: Personalizzazione Layout e Componenti

**Domanda Graphify:**
```bash
graphify query "One component architecture and Blade structure"
```

**Workflow:**
1. Ispeziona views in `resources/views/components/`
2. Modifica o crea nuovo componente Blade
3. Verifica la resa visiva

---

## 🚀 Comandi Rapidi Tema

```bash
# Esplora struttura tema
graphify query "One theme components"

# Dipendenze
graphify query "modules using One theme"
```

---

## 📚 Riferimenti

- **Graphify Central:** `docs/graphify-integration.md`
- **Theme Template:** `laravel/themes/GRAPHIFY_THEME_TEMPLATE.md`

---

**Responsabile:** @marco76tv | **Last updated:** 2026-08-02
