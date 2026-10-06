---
title: "Handoff multi-org sync (STORY-003)"
type: handoff
tags: [git, multi-org, bmad, story-003]
created: 2026-07-21
updated: 2026-07-23
module: "One"
issues:
  - "https://github.com/provtv/theme_one_fila5/issues/6"
discussions:
  - "https://github.com/provtv/theme_one_fila5/discussions/7"
---

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

## Regole rapide

1. `cd` owner → `git remote -v` → fetch tutti → merge senza force → push tutti
2. Dopo edit PHP: phpstan/phpmd/phpinsights scoped (prompt `02-gitmodules-sync.md`)
3. Mai `git restore` — forward-only
4. UI: non reintrodurre `InteractiveMap` (dominio Geo)

## Note owner

Tema: discussion locale abilitata.

### Playbook push dual-remote (2026-07-22)


### Caso User 2026-07-23 (unrelated)

`merge-base` vuoto vs un org → STOP. User: laraxot `3ea7273a` OK; provtv unrelated.
[../../../Modules/User/docs/wiki/troubleshooting/git-push-dual-remote-unrelated.md](../../../Modules/User/docs/wiki/troubleshooting/git-push-dual-remote-unrelated.md).

### Sync 2026-07-23 (batch 5-item)

- `laraxot` remote → **404 "Repository not found"** (unreachable, `git ls-remote` timeout/error), skip push.
- `provtv/dev` → 0 behind, 1 ahead (2 doc file già modificati da altra sessione: `git-multi-org-sync-handoff.md`, `multi-org-sync-laraxot-provtv.md`). Committato (`c2e5282`) e pushato → `provtv/dev` ora allineato a `c2e5282`.
- Nessun merge/conflitto necessario, nessuna rottura trovata.
- Stato finale: working tree clean, `laraxot` da riverificare quando torna raggiungibile.
