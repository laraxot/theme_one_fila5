---
title: "Overflow history (ceiling 100)"
type: digest
status: active
qmd: "digest ceiling 100 overflow-history"
---

# Overflow history (ceiling 100)

Overflow force-cap: 16 file oltre target 100.

### `bmad/advanced-manage-related-records.md` — Advanced ManageRelatedRecords - One Theme


# Advanced ManageRelatedRecords - One Theme

## The "Sexy" Experience
The 'One' theme elevates the related record management with refined aesthetics and modern interactive patterns.

## Visual Enhancements
### 1. Glassmorphism & Shadowing
- Relational tables are contained in clean cards with subtle shadows (`shadow-sm`) and rounded corners (`rounded-xl`).
- Hover effects on rows use a light primary tint (`bg-primary-50/50`) to provide immediate feedback.

### 2. Micro-interactions
- **Modal Animations**: Slide-overs are preferred for creating/editing relations to keep the parent record visible in the background.
- **Button Vibrancy**: Primary buttons use gradients and scale slightly on hover.

### 3. Rich Data Visualization
- **Counters**: Display record counts in the navigation label as 

### `bmad/document-root-public-html.md` — Document root: `public_html`, non `laravel/public`


# Document root: `public_html`, non `laravel/public`

**Regola canonica**: [Modules/Xot/docs/wiki/rules/public-path-public-html.md](./public-path-public-html.md)

## In una riga

`public_path()` risolve `{repo}/public_html/`. **Mai** `{repo}/laravel/public/`.

L'applicazione sta in `laravel/`, ma il web server serve `public_html/` un livello sopra.
`App\Application::publicPath()` lo garantisce, e `laravel/bootstrap/app.php` istanzia quella
classe e non quella stock di Laravel.

## Cosa significa per questo tema

Il tema pubblica gli asset con `public_path('themes/one/...')` — vedi `docs/html2pdf-integration.md`, dove il logo del PDF si risolve con `public_path('themes/one/assets/logo.png')`.

## Come si sbaglia

Usare `base_path('public')` o scrivere `laravel/public/` a mano. Entrambi pun

### `bmad/dry-kiss-matr-ente-relationships.md` — HasMany matr/ente Pattern - DRY + KISS


# HasMany matr/ente Pattern - DRY + KISS

## Sintesi Esecutiva

Pattern centralizzato per relazioni HasMany che uniscono `matricola` + `ente` evita duplicazione in 50+ modelli Sigma.

## Regola Fondamentale

> Ogni modello con `ente`/`matr` deve implementare `matrField()` e `enteField()` e usare `hasManyByEnteMatr()`.

## Architettura

```
BaseModel (implementa EnteMatrFieldsContract)
    ├── matrField() = 'matr' (override opzionale)
    ├── enteField() = 'ente' (override opzionale)
    └── hasManyByEnteMatr(RelatedClass)
            → Usa matrField/enteField
            → Applica filtro annFieldName() automatico

### `bmad/epics/one-epics-and-stories.md` — One Theme Epics and User Stories

# One Theme Epics and User Stories

## Epic 1: Base Theme Structure
As a Developer, I want a clean theme base so that I can extend it consistently.

### Story 1.1: Layout Structure
**Acceptance Criteria**:
- [ ] Master layout file created
- [ ] Common header/footer components
- [ ] Asset pipeline configured
- [ ] Build commands working

## Epic 2: Component Library
As a Designer, I want consistent components so that the UI looks unified.

### Story 2.1: Button Styles
**Acceptance Criteria**:
- [ ] Primary button style
- [ ] Secondary button style
- [ ] Disabled state

### `bmad/git-multi-org-sync-handoff.md` — Handoff — multi-org sync (STORY-003)


# Handoff — multi-org sync (STORY-003)

## Scopo

Allineare questo owner ai remote raggiungibili (**0 0**, working tree clean) e documentare decisioni di sessione 2026-07-21.

## Perché

Un tree dirty o un remote dietro/avanti **non** è sincronizzato, anche se l’altro org è a posto. Su PTVX i path vivono in `gitmodules.ini` con org `provtv` (+ `laraxot` se esiste).

## Link

| Tipo | URL |
|------|-----|
| Issue owner | https://github.com/provtv/theme_one_fila5/issues/6 |
| Discussion | https://github.com/provtv/theme_one_fila5/discussions/7 |
| Hub base issue | https://github.com/provtv/base_ptv_fila5/issues/203 |
| Hub base discussion | https://github.com/provtv/base_ptv_fila5/discussions/204 |
| Story monorepo | `docs/stories/STORY-003-multi-org-sync-geo-boundary-bashscripts.md` |

### `bmad/gitmodules-sync-session.md` — Gitmodules sync session


# Gitmodules sync session

Sessione orchestrata dal prompt `bashscripts/tools/prompts/02-gitmodules-sync.md` (v5.1) e da **STORY-003**.

## Cosa fare su questo owner

1. `git remote -v` — sync **tutte** le organizzazioni (`fetch` + `pull --ff-only` + `push`, mai `--force`).
2. Quality gates da `laravel/`: phpstan → phpmd → phpinsights (`--composer=composer.lock`).
3. Marker Git: risoluzione manuale forward-only (no `git restore`).

## Canon

- Story: [../../../../docs/stories/STORY-003-gitmodules-sync-conflict-sweep.md](../../../../docs/stories/STORY-003-gitmodules-sync-conflict-sweep.md)
- Report: [../../../../../bashscripts/ai/wiki/memories/git-sync-fleet-remotes.md#gitmodules-sync](../../../../../bashscripts/ai/wiki/memories/git-sync-fleet-remotes.md#gitmodules-sync)
- Issue base: http

### `bmad/ide-helper-phpdoc-boundary.md` — ide helper — confine PHPDoc tema One


# ide helper — confine PHPDoc tema One

## Scopo per il tema

Il tema One **non possiede model Eloquent di dominio**: è presentation layer (Folio, Blade, asset Vite). Tuttavia **consuma** model dei moduli in:

- pagine Folio con `@php` e type hint
- componenti Livewire referenziati da view
- widget Filament embedded nel frontend

I PHPDoc generati da `ide-helper:models` sui moduli alimentano l'autocompletamento anche nel codice PHP del tema.

## Perché importa al tema

| Senza PHPDoc aggiornati | Con PHPDoc aggiornati |
|-------------------------|----------------------|
| `$scheda->anno` opaco in Folio | Type inference corretta |
| PHPStan sul tema segnala mixed | Analisi incrociata modulo-tema |
| Refactor rischiosi su view | Navigazione sicura verso moduli |

### `bmad/laravel-13-composer-boundary.md` — Laravel 13 Composer boundary for Theme One


# Laravel 13 Composer boundary for Theme One

## Rule

Theme One owns presentation, visual components, and theme assets. It must not become a dumping ground for Laravel runtime packages.

Use `laravel/Themes/One/composer.json` only for theme-owned PHP dependencies or PSR-4 autoload that the runtime actually needs. Module features remain in module composer files.

## Laravel 13 migration impact

- Do not add `laravel/framework`, `nwidart/laravel-modules`, Passport, permissions, or debugbar to this theme composer.
- Debugbar is a cross-application dev tool owned by `Modules/Xot/composer.json` as `fruitcake/laravel-debugbar:^4.2.8`; themes must not declare `barryvdh/laravel-debugbar` or `fruitcake/laravel-debugbar`.
- If Theme One needs runtime PHP autoload, audit whether `Themes/*/composer.

### `bmad/model-docs-governance.md` — Theme One Docs Governance


# Theme One Docs Governance

## Objectives

1. Keep docs discoverable with stable filenames.
2. Keep module references aligned with real PHP class names.

## Rules

1. Use `kebab-case` filenames for new docs.
2. If a module model is singular (for example `Scheda`), docs in themes must reference the singular class name.
3. Keep one canonical doc per topic; move alternates to archive folders.
4. Maintain `README.md` as the canonical entrypoint for this folder.
5. Cross-module models (es. `Progressioni\Models\Scheda` che estende Ptv): documentare sempre la connessione DB del consumer, non quella ereditata. Vedi [common-errors](./common-errors.md#modello-scheda-su-database-errato-progressioni) e [database-connection-progressione](../../../Modules/Progressioni/docs/database-connection-progress

### `bmad/multi-org-sync-laraxot-provtv.md` — Sincronizzazione multi-organizzazione (laraxot + provtv)


# Sincronizzazione multi-organizzazione (laraxot + provtv)

## Cosa è stato fatto

Questo repository è tracciato da due remote GitHub (`laraxot` = org upstream canonica,
`provtv` = org operativa del progetto ptvx). Il 2026-07-21 è stata eseguita una
sincronizzazione completa seguendo `bashscripts/tools/prompts/02-gitmodules-sync.md`:
fetch di tutti i remote, quality gates (PHPStan L10, PHPMD), risincronizzazione dopo ogni modifica.

## Problemi riscontrati e risolti

- **Clone shallow**: il repo era stato clonato con storia troncata, causando push
  respinti (`did not receive expected object`). Fix: `git fetch --unshallow` su tutti i remote.
- **Storie scollegate ("unrelated histories")**: alcuni repo avevano un branch `dev`
  remoto rigenerato senza antenato comune con la storia locale. 

### `bmad/one-migration-themes-boundary.md` — Temi e migrazioni


# Temi e migrazioni

I temi (`Themes/One`, `Zero`, `Three`) **non** possiedono modelli Eloquent né
`database/migrations/`. La regola «1 modello = 1 migrazione» vive nei moduli under
`laravel/Modules/`.

UI/tema: asset e view; schema DB: solo modulo owner della tabella.

### `bmad/public-path-public-html.md` — Document root per i temi


# Document root per i temi

Gli asset del tema dopo `npm run build` + `symlink public_html/themes (npm run copy obsoleto)` devono finire in **`public_html/themes/{Theme}/`**.

`public_path()` Laravel punta a `public_html/`, **non** a `laravel/public/`.

SSoT: [public-path-is-public-html](../../../../../bashscripts/ai/wiki/memories/frontend-themes-css.md#public-path-is-public-html) · skill [public-path-public-html](./public-path-public-html.md).

### `bmad/readonly-field-styling.md` — Readonly Field Styling - UI/UX Pattern


# Readonly Field Styling - UI/UX Pattern

**Theme**: One  
**Date**: 2026-02-11  
**Status**: Standard attivo

---

## Panoramica

Pattern standard per lo stile visivo dei campi readonly (calcolati/computati) nei form Filament. Condiviso con il tema Zero per garantire coerenza cross-theme.

## Pattern Standard

### Classi Tailwind CSS

```php
->readOnly()
->extraInputAttributes([

### `bmad/release-marketing-standard.md` — Release e README marketing — One


# Release e README marketing — One

## Scopo

Ogni modulo/tema deve essere pubblicabile, comprensibile e desiderabile: workflow release, changelog automatico e README vetrina.

## File canonici locali

- `../README.md`
- `../.github/workflows/semantic-release.yml`
- `../.releaserc.json`
- `../changelog.md`

## Confidenza

La configurazione usa semantic-release con Conventional Commits, changelog, GitHub release e commit automatico del changelog.

### `bmad/spatie-permission-team-context.md` — Spatie Permission Team Context


# Spatie Permission Team Context

## Theme Boundary

Theme One is presentation. It must not override Spatie Permission configuration.

The User module owns:

- `Modules\User\Models\Permission`
- `Modules\User\Models\Role`
- `Modules\User\Models\Team`

## Rendering Rule

Use Laravel authorization APIs (`can()`, policies, Filament authorization hooks) and avoid role-name coupling in Blade/Livewire views.

If team switching is visible in the theme, the active team context is part of authorization state. After switching teams, User module code is responsible for resetting the active Spatie team id and reloading role/permission relations.

Spatie Permission v7 separates the configured team model from the active team id:

### `bmad/spatie-permission-teams-boundary.md` — Spatie Permission teams boundary


# Spatie Permission teams boundary

## Theme boundary

Theme One presents the admin and HR interface. It must not own Spatie Permission configuration.

Team-aware authorization belongs to:

- `Modules/User` for `Team`, `Role`, `Permission`, team switching, and auth widgets.
- `Modules/Xot` for framework-level class defaults.
- `config/permission.php` and local overrides for Spatie package wiring.

## Laravel 13 impact

Spatie Permission 7 requires `permission.models.team` when teams are enabled. Missing configuration can surface while rendering theme pages because Filament dashboard widgets mount before the page is fully displayed.

## Verification for theme work

If Theme One renders team-aware widgets, verify:
