---
title: "Docs zen: convenzioni .md del tema One"
type: story
status: done
module: One
epic: docs-second-brain
created: 2026-11-25
updated: 2026-11-25
qmd: "one docs zen convenzioni md kebab frontmatter qmd duplicati alias template fabbricati bonifica"
related:
  - ../../../../../Modules/Xot/docs/bmad/stories/docs-zen-conventions-swarm.story.md
---

# Docs zen: One

## Perche'

Story ombrello `laravel/Modules/Xot/docs/bmad/stories/docs-zen-conventions-swarm.story.md` (lane D).
Rumore nei docs (alias, copie, template inventati, nomi non conformi) degrada QMD e confonde gli agenti.

## Prima / Dopo

| Metrica | Prima | Dopo |
|---|---:|---:|
| file .md | 120 | 111 |
| copie esatte (md5) | 0 | 0 |
| nomi datati | 0 | 0 |
| nomi non kebab | 2 | 2 |
| senza frontmatter | 0 | 0 |
| senza `qmd` | 0 | 0 |

Eccezioni volute (non rinominate): `adr/INDEX.md`, `contracts/INDEX.md`, `contracts/_template.md` sono letti per nome da `bashscripts/tools/harness/harness-audit.py`; `wiki/SCHEMA.md` viene ricreato da `bashscripts/docs/setup-llm-wiki-structure.sh` se manca; `wiki/AGENTS.md` e' il nome convenzionale letto dagli agenti.

## Cosa e' stato eliminato/fuso e perche'

- Eliminati 9 template fabbricati in `bmad/` (product-strategy, product-requirements, product-launch-plan, launch-plan, sprint-planning, sprint-planning-meeting, user-research, duplicate-methods, duplicate-methods-report): nessun riferimento a classi/viste reali del tema (26 file PHP verificati), date sprint e percentuali inventate; `duplicate-methods-report` era il report grep globale, non del tema. Il dato reale (0 corpi duplicati) resta in `wiki/concepts/duplicate-method-bodies.md`.
- `bmad/index.md`: voci rimosse/riallineate (PRD, roadmap, theme-analysis restano).
- Aggiunto `title` a 1 file.

Link aggiornati con mappa vecchio→nuovo su `laravel/Modules/*/docs`, `laravel/Themes/*/docs`, `docs/`, `bashscripts/ai/wiki`; link verso file eliminati senza canonico trasformati in testo o rimossi dagli indici. Verifica finale: 0 link markdown verso path rimossi.

## Casi lasciati in dubbio

- `wiki/sources/theme-one-product-and-roadmap-docs.md` riassume i documenti di strategia rimossi: tenuto (sintesi wiki), da rivalutare.

## Gate

Solo file `.md` sotto `docs/`: PHPStan/Pint/Pest non applicabili (skip documentato; PHPStan gia' 0 da story ombrello). Nessun commit eseguito dall'agente.
