---
title: "Indice documentazione — Theme One"
type: index
theme: One
status: active
created: 2026-10-21
updated: 2026-10-21
tags: [theme, one, docs, index, bmad, wiki]
qmd: "theme one indice documentazione bmad wiki architecture stories filament blueprint"
related:
  - ./README.md
  - ./bmad/index.md
  - ./wiki/index.md
---

# Indice documentazione — Theme One

Ingresso attivo: [README.md](./README.md). Questo `index.md` e' l'indice navigabile
per il tema One; non introduce una seconda fonte di verita'.

## Struttura

- [`bmad/`](./bmad/) — dossier BMAD, guide, report e pianificazione.
- [`bmad/stories/`](./bmad/stories/) — story BMAD del tema.
- [`stories/`](./stories/) — story feature storiche.
- [`wiki/`](./wiki/) — concetti, regole, fonti e roadmap.
- [`architecture/`](./architecture/) — ingresso alle decisioni architetturali.
- `epics/` e `roadmap/` — cartelle vuote, mantenute per compatibilita'.

## Documenti chiave

- [Architettura](./bmad/architecture.md) e [regole architetturali](./wiki/architecture-rules.md)
- [Filament blueprint](./bmad/filament-blueprint.md)
- [Scopo](./bmad/scopo.md) / [purpose](./bmad/purpose.md)
- [PRD](./bmad/prd.md), [tech spec](./bmad/tech-spec.md), [roadmap](./bmad/roadmap.md)
- [PHPStan nel tema](./phpstan-level10-analysis.md)
- [Audit qualita'](./bmad/quality-audit.md)
- [Indice wiki](./wiki/index.md)

## Regole

1. Un solo canonico per argomento; i duplicati sono `superseded` o in `_archive/`.
2. Nomi kebab-case minuscoli, senza date.
3. Ogni `.md` ha frontmatter YAML con `qmd`.
4. Il tema resta presentazione: nessuna business logic, nessun modello, nessuna
   policy.
