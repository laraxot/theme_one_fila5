---
title: "Organizzazione docs — Theme One"
type: story
status: done
theme: One
epic: docs-governance
story_id: "theme-one-docs-organization"
track: quick-flow
created: 2026-10-21
updated: 2026-10-21
tags: [docs, theme, one, bmad, deduplication, frontmatter, links]
qmd: "theme one docs organization canonical index duplicates stale locks frontmatter qmd link audit filament blueprint"
related:
  - ./navigationicon-themes-audit.story.md
  - ../../../../Three/docs/bmad/stories/docs-organization.story.md
  - ../../../../Zero/docs/bmad/stories/docs-organization.story.md
  - ../../../../../Modules/Xot/docs/bmad/stories/phpstan-modules-swarm-20261021.story.md
---


# Organizzazione docs — Theme One

## Obiettivo

Rendere la documentazione del tema One navigabile e coerente: un indice canonico,
nessun duplicato case-only, frontmatter/qmd completi, blueprint Filament esplicito
e debito storico tracciato senza riscrivere il contenuto di dominio.

## Baseline verificata

- 115 file `.md`; 3 senza frontmatter, 48 senza `qmd`.
- 19 `.lock` stale del task `docs-100-merge` (2026-10-05, PID non attivi).
- Coppie che collidevano su filesystem case-insensitive:
  `ARCHITECTURE.md`/`architecture.md`, `FRAMEWORKS.md`/`frameworks.md`,
  `PRD.md`/`prd.md`, `README-en.md`/`readme-en.md`, `SCHEMA.md`/`schema.md`.
- Duplicati di contenuto: `duplicate_methods*`, `charts-integration`,
  `html2pdf-integration` tra `bmad/` e `roadmap/`.
- `INDEX.md` e gli indici `bmad/`/`wiki/` con link non allineati alla struttura reale.

## Acceptance criteria

- [x] Nessun `.lock` stale nella docs del tema.
- [x] Nessuna coppia di nomi che differisce solo per la maiuscola.
- [x] Un solo indice canonico: `docs/index.md`; `bmad/readme.md` è solo l'ingresso del dossier.
- [x] Contenuto unico: i duplicati sono assorbiti o rimossi dopo verifica di contenimento.
- [x] Frontmatter YAML valido e `qmd` presente in tutti i `.md` attivi.
- [x] `filament-blueprint.md` descrive il contratto Filament del tema.
- [x] Nessun link relativo rotto negli indici e nei README del tema.

## Lavoro eseguito

| Area | Azione | Esito |
| --- | --- | --- |
| Lock | Rimossi 19 `.lock` stale verificati | Nessun lock attivo residuo |
| Case-only | Tenuto il file minuscolo, rimosso l'upper dopo diff di contenimento | 0 coppie residue |
| Duplicati | Rimossi `bmad/ARCHITECTURE.md`, `FRAMEWORKS.md`, `PRD.md`, `duplicate_methods*`, `wiki/SCHEMA.md` | Contenuto utile già nel canonico |
| PRD | Aggiunto il vincolo `Laravel 12+` | Coerente con il codice |
| Indici | Riscritti `INDEX.md`, `bmad/index.md`, `wiki/index.md`; `bmad/readme.md` ridotto a ingresso | Navigazione unica |
| Frontmatter | Aggiunto a `bmad/readme-en.md` e alla story `navigationicon-themes-audit` | 0 mancanti |
| Link | Rebase automatico dei link con basename univoco + fix manuale degli indici | 0 rotti in indici/README |
| Blueprint | Creato `bmad/filament-blueprint.md` | Contratto XotBase + widget FO espliciti |
| Architettura | Creato `architecture/README.md` | Cartella non più vuota |

## Verifica

```bash
find laravel/Themes/One/docs -name '*.lock' -print          # vuoto
find laravel/Themes/One/docs -type f | tr 'A-Z' 'a-z' | sort | uniq -d  # vuoto
# frontmatter/qmd: 112 file attivi, 0 senza frontmatter, 0 senza qmd
# link relativi: 352 totali, 115 rotti residui (debito storico, non negli indici)
git diff --check -- laravel/Themes/One/docs                  # solo whitespace storico
```

Nessun codice applicativo toccato: Pest e PHPStan non applicabili a un diff
docs-only. Nessun commit/push.

## Debito residuo

- 115 link relativi rotti in documenti storici: puntano a file di moduli assenti
  nel checkout (`Progressioni`, `IndennitaResponsabilita`) o a documenti rimossi
  in passate pulizie. Non sono negli indici/README e non bloccano la navigazione.
- Il contenuto di One resta in gran parte dichiarativo: il tema è uno skeleton e
  non ha ancora codice applicativo proprio.
