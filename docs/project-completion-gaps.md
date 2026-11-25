---
title: "Lacune di completamento — One"
type: audit
status: open
created: 2026-10-28
updated: 2026-10-28
tags: [project-readiness, documentation, theme]
qmd: "One theme lacune completamento progetto backlog documentazione qualità gate test integrazione"
related:
  - "../../../Modules/Xot/docs/project-completion-readiness.md"
---

# Lacune di completamento — One

## Esito

Questo censimento documentale non certifica il completamento funzionale del theme.
Il completamento resta **non dimostrato** finché non sono chiusi e verificati i criteri
sotto elencati e le story aperte del modulo/tema in `docs/sprint-status.yaml`.

## Evidenza documentale rilevata

- Markdown sotto `docs/`: **113**.
- Story BMAD trovate (`*.story.md`): **6**; il conteggio non implica che siano
  concluse né che coprano tutti i requisiti.
- Frontmatter iniziale presente: **113/113**.
- README/purpose mancanti: `purpose.md`
- Controllo frontmatter: Tutti i Markdown censiti iniziano con frontmatter; validità semantica completa non controllata per ciascun documento.

## Lavoro necessario per poter chiudere

1. Riconciliare i requisiti del theme con le story BMAD: nessun requisito senza AC,
   owner, dipendenze e stato verificabile.
2. Chiudere le story non concluse nel relativo sprint status; non dedurre `done` dal
   solo fatto che il codice o una story esistano.
3. Verificare le boundary del modulo/tema con i consumatori, permessi, tenant, dati e
   contratti di integrazione applicabili; registrare le prove nella story owner.
4. Eseguire i gate applicabili (Pest, PHPStan per modulo e controlli di qualità) e
   riportare comando, esito e limiti ambientali. Nessuna verifica funzionale è stata
   eseguita da questo censimento documentale.
5. Aggiornare i documenti e gli indici QMD dopo ogni chiusura; i nomi `.md` restano
   kebab-case stabili, senza date o timestamp.

## Criterio di chiusura

Story e acceptance criteria pertinenti chiusi; regressioni assenti nei gate applicabili;
integrazioni reali documentate; documentazione e QMD aggiornati. Questo file va aggiornato
solo con evidenze nuove, non con supposizioni.

## Story BMAD non concluse nel corpus owner

Lettura read-only delle 6 story locali (`*.story.md`): 4 hanno uno stato diverso da done/completed/superseded/invalid o non hanno stato esplicito. I conteggi descrivono il frontmatter delle story, non sostituiscono `docs/sprint-status.yaml`.

| Stato | Numero |
|---|---:|
| `active` | 1 |
| `backlog` | 3 |
| `done` | 2 |

### Esempi prioritari da riconciliare

- `active` — [`0003-navigationicon-themes-audit.story.md`](bmad/stories/navigationicon-themes-audit.story.md)
- `backlog` — [`3.6.staff-portal-readonly-view.story.md`](stories/3.6.staff-portal-readonly-view.story.md)
- `backlog` — [`4.4.evaluation-criteria-publish.story.md`](stories/4.4.evaluation-criteria-publish.story.md)
- `backlog` — [`4.5.transparent-scoring-view.story.md`](stories/4.5.transparent-scoring-view.story.md)

Prima di lavorare su questi elementi, verificare lo stato canonico nello sprint status, claim/lock e dipendenze. Una story senza `status` non va considerata automaticamente completata.
