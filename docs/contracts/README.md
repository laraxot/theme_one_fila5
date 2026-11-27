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

## Harness minimo: ownership, evidenza e recupero (2026-11-27)

I contratti di **theme_one_fila5** restano accanto alle Action, interfacce o superfici di questo package; root e Xot definiscono lo standard, non copiano le promesse. Un contratto comportamentale esplicita **Input, Output, Invarianti, Effetti collaterali, Errori, Non fa**; ogni ID di invariante punta a un group Pest effettivo oppure segnala `non dimostrata`. Se esiste la classe, il docblock deve rimandare al file con `@contract` e `@see`; per temi senza classi PHP non inventare Action/contratti.

- [Standard Xot](https://github.com/laraxot/module_xot_fila5/blob/dev/docs/contracts/contract-authoring-standard.md) · [ownership root](https://github.com/laraxot/base_ptvx_fila5/blob/dev/docs/adr/0001-harness-minimo-e-ownership.md) · [runbook ECC/Second Brain](https://github.com/laraxot/base_ptvx_fila5/blob/dev/docs/harness/README.md).
- **BMAD**: prima di cambiare una promessa, fissa nella story owner scope, esclusioni, evidenza e approvazioni richieste.
- **ECC**: i marker di merge rendono invalido l'indice; citare una suite non significa averla eseguita. Distingui `pass`, `fail`, `non eseguito` e registra il debito in [rollout #15](https://github.com/laraxot/base_ptvx_fila5/issues/15).
