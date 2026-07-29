---
title: "ide helper — confine PHPDoc tema One"
module: "One"
type: concept
tags: [ide, helper, phpdoc, theme, quality]
created: 2026-07-15
updated: 2026-07-15
related:
  - "../../Modules/Xot/docs/ide-helper-philosophy.md"
  - "./code-quality-tools.md"
  - "./model-docs-governance.md"
---

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

Regola già in [model-docs-governance](./model-docs-governance.md): i doc del tema devono referenziare **classi PHP reali**; ide-helper mantiene allineati i nomi e le proprietà.

## Confine di responsabilità

```text
Moduli (Lang, User, Ptv, …)  →  generano @property sui model
Tema One                      →  consuma tipi, non rigenera PHPDoc
Xot                           →  governance comando e wave
```

Il tema **non esegue** `ide-helper:models` su path propri (non ci sono `app/Models`). Partecipa alla wave **leggendo** gli esiti e aggiornando doc quando un model consumato cambia contratto.

## Wave 2026-07-15 — impatto indiretto

Segnalazioni attive su `TranslationFile` e token OAuth **non bloccano** il build del tema, ma:

- Filament/Lang che espone `TranslationFile` in admin perde autocompletamento finché la classe non è analizzabile
- Flussi OAuth documentati in User restano tipizzati parzialmente su `OauthToken`

Per dettaglio: [ide-helper-philosophy](../../Modules/Xot/docs/ide-helper-philosophy.md).

## Checklist tema (post-wave moduli)

1. Se una Folio page usa proprietà model, verificare che esista `@property` nel modulo sorgente
2. Aggiornare [common-errors](./common-errors.md) se emergono mismatch connessione DB (es. `Scheda` Progressioni)
3. Non duplicare PHPDoc nel tema — link al modulo

## Collegamenti

- [code quality tools](./code-quality-tools.md)
- [Xot — ide helper governance](../../Modules/Xot/docs/ide-helper-models-governance.md)
- [Zero — stesso confine](../Zero/docs/ide-helper-phpdoc-boundary.md)
