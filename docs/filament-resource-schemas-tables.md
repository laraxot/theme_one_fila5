---
title: "Filament Resource: Schemas e Tables (tema One)"
type: guide
description: "Convenzione Schemas/Tables Filament per tema One; eccezione scheda BaseSchedaForm/Infolist."
status: stable
tags: [filament, schemas, tables, theme-one]
module: "Themes/One"
created: 2026-07-14
updated: 2026-09-01
qmd: "filament resource schemas tables tema one BaseSchedaForm BaseSchedaInfolist"
related:
  - ../../Modules/Ptv/docs/scheda-resource-pages-inheritance.md
  - ../../Modules/IndennitaResponsabilita/docs/base-scheda-form-inheritance.md
  - ../../Modules/IndennitaResponsabilita/docs/base-scheda-infolist-inheritance.md
  - ../Zero/docs/filament-resource-schemas-tables.md
  - ../../../docs/wiki/rules/markdown-file-naming-and-frontmatter.md
---
# Filament Resource: Schemas e Tables (tema One)

## Scopo

Se il tema espone risorse Filament (`Themes\One\Filament\Resources\...`), usare la stessa struttura dei moduli Laraxot: cartelle `Schemas/` e `Tables/` accanto alla Resource.

## Struttura

```
Themes/One/app/Filament/Resources/{ResourceName}/
├── Schemas/
│   ├── {Entity}Form.php
│   └── {Entity}Infolist.php
├── Tables/
│   └── {Entities}Table.php
├── Widgets/                    # opzionale — stats overview su List*
│   └── {Entity}StatsOverview.php
└── {ResourceName}.php
```

## Widget stats su List*

Per riepiloghi in testata lista (Filament 5 [stats overview](https://filamentphp.com/docs/5.x/widgets/stats-overview)):

- Widget in `{ResourceName}/Widgets/`, estende `XotBaseStatsOverviewWidget`
- `List{plural}::getHeaderWidgets()` + `{Resource}::getWidgets()`
- Logica query in Action dedicata (non nel widget)

Esempio modulo: [Asz00f stats Progressioni](../../../Modules/Progressioni/docs/wiki/concepts/asz00f-filament-stats-overview.md).

## Regole

- Estendere `XotBaseResourceForm`, `XotBaseResourceInfolist`, `XotBaseResourceTable`.
- **Eccezione scheda:** se il model estende `BaseScheda`, il Form deve estendere `BaseSchedaForm` e l’Infolist `BaseSchedaInfolist` (non le classi Xot dirette); Edit/Create da `BaseEditScheda` / `BaseCreateScheda`. Riferimento: [Ptv — scheda pages inheritance](../../../Modules/Ptv/docs/scheda-resource-pages-inheritance.md), [IR Form](../../../Modules/IndennitaResponsabilita/docs/base-scheda-form-inheritance.md), [IR Infolist](../../../Modules/IndennitaResponsabilita/docs/base-scheda-infolist-inheritance.md).
- Nessun `->label()` / `->placeholder()` / `->helperText()`.
- Chiavi stringa negli array restituiti dai metodi get*.
- **`getPages()`:** omettere se la Resource ha solo `index` / `create` / `edit` e le Page seguono `List{plural}`, `Create{name}`, `Edit{name}` — [regola Xot](../../../Modules/Xot/docs/filament/getpages-redundancy-rule.md).

## Copia metodi tabella Page → `*Table`: override utili vs inutili

Spostando la config tabella dalla Page `List*` alla classe `*Table`:

- `getHeaderActions()` (Page) → `getTableHeaderActions()` (Table); `$this->getModel()` → FQCN esplicito; `$this->tableFilters` → `$this->tableFilters ?? []`. Niente `#[Override]`.
- **NON** creare metodi che sarebbero solo `return parent::getTableXxx();` (passthrough) o `return [];` (vuoto): equivalgono al default di `HasXotTable` → violano DRY+KISS. Override solo se aggiunge azioni/filtri/colonne custom.

Dettaglio e anti-pattern: [Progressioni — filament-resource-schemas-tables](../../../Modules/Progressioni/docs/filament-resource-schemas-tables.md#copia-metodi-tabella-page--classe-table-override-utili-vs-inutili).

## Riferimenti

- [UI — toggle layout lista/griglia](../../../Modules/UI/docs/actions/table-layout-toggle.md) (ereditato via `HasXotTable`, nessun override nel tema)
- [Xot — getPages ridondanza](../../../Modules/Xot/docs/filament/getpages-redundancy-rule.md)
- [Xot – Filament v5 hybrid pattern](../../../Modules/Xot/docs/wiki/concepts/filament-v5-hybrid-pattern.md)
- [Progressioni – migrazione in corso](../../../Modules/Progressioni/docs/filament-resource-schemas-tables.md)
- Select options: enum sul concetto + `EnumTrait` — [Ptv enum-naming-reusable](../../../Modules/Ptv/docs/enum-naming-reusable.md), [filament-select-options-enum](../../../Modules/Ptv/docs/filament-select-options-enum.md)
- [Progressioni – wire pilota Assenze](../../Modules/Progressioni/docs/filament-resource-wire-assenze.md)
- [Zero – stesso pattern](../../Zero/docs/filament-resource-schemas-tables.md)
- [Three – stesso pattern](../../Three/docs/filament-resource-schemas-tables.md)

*Ultimo aggiornamento: giugno 2025*
