---
title: "Contratti — Theme One"
type: index
owner: One
updated: 2026-11-24
qmd: "Theme One contract presentation-contract assenti viste Blade anonime"
---

# Contratti — Theme One

Standard: [contract-authoring-standard](../../../../Modules/Xot/docs/contracts/contract-authoring-standard.md) (sezione «Contratti non-Action»).

## Stato

**Nessun contract in One.** Motivo: il tema non ha Action di dominio (`app/` contiene solo `.gitkeep`) e le sue superfici sono viste Blade anonime (`resources/views/components/layouts/*`, `components/blocks/*`, `pages/*`) senza classe PHP: un `presentation-contract` richiede `contract: <FQCN>` e un `@see` dalla classe. I contratti applicativi stanno nei moduli.

Se una vista diventasse un componente con classe, scrivere allora un `presentation-contract` con `contract: <FQCN>`.

## File presenti

- [INDEX.md](INDEX.md): registro operativo e backlog
