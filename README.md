# One: il tema che trasforma complessita in vantaggio operativo

One theme for Laraxot PTVX: minimal theme skeleton for future frontend development and customization.

## Perche guardarlo adesso

- Riduce attrito operativo con convenzioni Laraxot gia pronte.
- Porta documentazione, release e changelog nello stesso flusso verificabile.
- Aiuta team e agenti AI a capire subito scopo, confini e prossime mosse.
- E pensato per crescere: semantic versioning, auto release e changelog automatico sono gia configurati.

## Cosa promette

Questo tema non e solo codice: e una vetrina operativa. Mostra dove intervenire, cosa leggere, come rilasciare e come mantenere alta la confidenza tecnica.

## Release automation

- Workflow: [Semantic Release](./.github/workflows/semantic-release.yml)
- Config: [.releaserc.json](./.releaserc.json)
- Changelog: [changelog.md](./changelog.md)


## Documentazione tecnica

- [Indice docs](./docs/README.md) — mappa knowledge base locale (wiki, audit, regole)

## Documentazione essenziale

- [Second brain locale](./docs/wiki/index.md)
- [Audit ridondanza](./docs/code-redundancy-audit.md)
- [Protocollo confidenza](./docs/agent-confidence-protocol.md)
- [Disciplina agenti](./docs/agent-edit-discipline.md)
- [Advanced Manage Related Records](./docs/advanced-manage-related-records.md)
- [Architecture Rules](./docs/architecture-rules.md)
- [Charts Integration](./docs/charts-integration.md)
- [Code Quality Tools](./docs/code-quality-tools.md)
- [Common Errors](./docs/common-errors.md)
- [Docs Archive Policy](./docs/docs-archive-policy.md)

## Scopo e confini

One è il tema di sviluppo locale: la stessa superficie di Zero, servita su `localhost`
(`config/localhost/xra.php:10`), senza la catena di build che la produrrebbe — non ha
`vite.config.js`, `tailwind.config.js`, `package.json` né `theme.json`. Tutti gli host
reali usano Zero. Misurato il 2026-09-02: i 20 file Blade di One sono **byte a byte
identici** a quelli di Zero (0 differenze, 0 file esclusivi), e `resources/css/` contiene
42 file spuri `xotcov-*.css` / `dfa-*.css` che contengono solo `a{}`.

Misure e cinque mosse concrete: [`docs/scopo.md`](./docs/scopo.md).

## Filosofia

Scopo prima del codice. DRY prima dell'orgoglio. KISS prima dell'astrazione. La release automatica non sostituisce il giudizio: lo rende tracciabile.
