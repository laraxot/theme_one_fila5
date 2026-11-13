---
title: "Filament Blueprint — Theme One"
type: filament-blueprint
status: active
theme: One
created: 2026-10-21
updated: 2026-10-21
tags: [bmad, filament, blueprint, theme, one, xotbase]
qmd: "filament blueprint theme one xotbase resource widget tenant policy phpstan gate"
related:
  - ./architecture.md
  - ./phpstan-level10-analysis.md
  - ../../../../Modules/Xot/docs/bmad/filament-blueprint.md
---

# Scopo

Contratto Filament del tema **One**. One e' oggi uno skeleton di sviluppo locale
(`app/` vuota, nessuna Resource o Widget PHP): il blueprint vale dal primo
componente Filament che verra' aggiunto e impedisce di introdurre eccezioni
rispetto ai moduli.

## Regole non negoziabili

1. Estendere solo `XotBaseResource`, `XotBaseWidget`, `XotBasePage` o le altre basi
   Xot; mai le classi Filament dirette.
2. Nessuna label hardcoded: niente `->label('...')`, chiavi in `lang/<locale>/`
   del tema o del modulo owner.
3. Logica di business nelle Queueable Action del modulo owner, non nel tema.
4. Il tema non interroga modelli e non possiede policy: espone solo presentazione.

## Resource e widget

- Resource PHP: nessuna in One; le Resource vivono nei moduli.
- Widget frontoffice: montaggio **esplicito** nella pagina o nel pannello; non
  usare `discoverWidgets` per il chrome del tema.
- Override di viste Filament ammesso solo in `resources/views/filament/`, senza
  duplicare la logica della Resource.

## Form, table e infolist

Se in futuro nasce una Resource nel tema, usare la triad `*Form`, `*Table`,
`*Infolist` e enum tipizzati al posto di array di opzioni. I campi readonly e i
valori calcolati seguono `readonly-field-styling.md`.

## Tenant e policy

Ogni query passa dal modulo owner e rispetta tenant e policy del modello. Nel
tema non si creano elenchi cross-tenant ne' scorciatoie per comodita' admin.

## Gate PHPStan

Il gate e' `cd laravel && php -d memory_limit=2G ./vendor/bin/phpstan analyse Modules`
con il solo `laravel/phpstan.neon`. Non si analizza il tema da solo e non si crea
un neon di tema. Dettaglio: [phpstan-level10-analysis.md](../phpstan-level10-analysis.md).

## Riferimenti

- Architettura del tema: [architecture.md](./architecture.md)
- Contratto Xot: [filament-blueprint.md](../../../../Modules/Xot/docs/bmad/filament-blueprint.md)
- Organizzazione docs: [../../../../Modules/Xot/docs/conventions/docs-organization.md](../../../../Modules/Xot/docs/conventions/docs-organization.md)
