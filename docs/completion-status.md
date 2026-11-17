---
qmd: "one completion status md"
title: "One: cosa manca per completare"
type: status
module: One
updated: 2026-10-28
repository: "https://github.com/provtv/base_ptv_fila5_mono"
github_issue: "https://github.com/provtv/base_ptv_fila5_mono/issues"
github_discussion: "https://github.com/provtv/base_ptv_fila5_mono/discussions"
related:
  - ../../../Modules/Xot/docs/project-completion-status.md
---

# One: cosa manca per completare

Fotografia misurata il 2026-10-28 (sola lettura). Si rigenera con gli stessi controlli: story nel frontmatter,
PHPStan livello 10, blade troncate, traduzioni, test. Riepilogo di progetto: `Modules/Xot/docs/project-completion-status.md`.

## Indicatori

| Indicatore | Valore |
|---|---|
| File PHP in `app/` | 0 |
| Errori PHPStan livello 10 | 0 |
| Blade (troncate in testa) | 20 (0) |
| File di test (`*Test.php`) | 0 |
| TODO/FIXME nel codice | 0 |
| Traduzioni it / en (solo in it) | 2 / 2 (0) |
| Story/epic BMAD (aperte) | 6 (4) |

## Problemi noti e prossimi passi

Nessun problema bloccante emerso dai controlli del 2026-10-28 oltre agli indicatori sopra e alle story aperte.

Problemi trasversali (valgono per tutto il progetto): vedi `project-completion-status.md` in Xot.

## Story aperte (per stato)

| Stato | Story |
|---|---|
| backlog | ['Staff portal: read-only Scheda view'](docs/stories/3.6.staff-portal-readonly-view.story.md) |
| backlog | [Evaluation criteria publish (staff portal visibility)](docs/stories/4.4.evaluation-criteria-publish.story.md) |
| backlog | ['Transparent scoring: staff see scores + criteria mapping'](docs/stories/4.5.transparent-scoring-view.story.md) |
| active | [navigationicon themes audit.story](docs/bmad/stories/navigationicon-themes-audit.story.md) |
