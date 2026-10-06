---
title: "Theme Documentation"
type: index
tags: [theme, one, readme]
created: 2026-05-19
updated: 2026-07-31
qmd: "one theme theme documentation"
---
# Theme Documentation

This directory contains documentation for the theme.

## Structure

- **customization.md** - Theme customization
- **README.md** - This file

## Guidelines

Documentation should be:
- Clear and concise
- Updated with theme changes
- Use Markdown format (.md)

<!-- swarm-docs:index:start -->

## Mappa della documentazione (indice di radice, generato dalla passata swarm-docs 2026-10-06)

Sezione generata: raggruppamento euristico per nome e titolo, nessun file e' stato spostato o rinominato. Marcatori: `[orfano]` = prima di questa passata nessun file della cartella `docs/` lo linkava; `[dup]` = sospetto duplicato (vedi sezione dedicata); `[marker di merge]` = contiene `<<<<<<<` o `>>>>>>>` non risolti.

### Entry point e struttura

- Modulo o tema: [../README.md](../README.md) (vetrina), [../../../Modules/Xot/docs/README.md](../../../Modules/Xot/docs/README.md) (docs del modulo base Xot)
- [INDEX.md](./INDEX.md): indice gia' presente
- [purpose.md](./purpose.md): scopo (esiste anche l'equivalente italiano/inglese, possibile duplicato)
- [scopo.md](./scopo.md): scopo (esiste anche l'equivalente italiano/inglese, possibile duplicato)
- Architettura: [architecture.md](./architecture.md)
- Architettura: [architecture-rules.md](./architecture-rules.md)
- [wiki/index.md](./wiki/index.md)
- Story BMAD (posizione canonica): [bmad/stories/](./bmad/stories/) (2 file)

### Sottocartelle

| Cartella | File .md (ricorsivo) | Entry point | Nota |
| --- | --- | --- | --- |
| [bmad/](./bmad/) | 2 | nessuno |  |
| [charts/](./charts/) | 2 | [README.md](./charts/README.md) |  |
| [epics/](./epics/) | 1 | nessuno |  |
| [html2pdf/](./html2pdf/) | 6 | [index.md](./html2pdf/index.md) |  |
| [prompts/](./prompts/) | 1 | nessuno |  |
| [raw/](./raw/) | 0 | nessuno | materiale grezzo |
| [roadmap/](./roadmap/) | 5 | nessuno |  |
| [schema/](./schema/) | 0 | nessuno |  |
| [screenshots/](./screenshots/) | 0 | nessuno |  |
| [shared-components/](./shared-components/) | 1 | nessuno |  |
| [stories/](./stories/) | 3 | nessuno | legacy: la posizione canonica e' `bmad/stories/` |
| [wiki/](./wiki/) | 19 | [index.md](./wiki/index.md) |  |

### Sovrapposizioni rilevate (nessuna azione eseguita)

- `stories/` (3 file) e `bmad/stories/`: 0 stessi nomi, 0 byte-identici. La posizione canonica e' `bmad/stories/`.

### File di radice per argomento

#### Agenti AI e regole di lavoro (6)

- [agent-confidence-discipline.md](./agent-confidence-discipline.md): Disciplina agenti per massimizzare la confidenza
- [agent-confidence-protocol.md](./agent-confidence-protocol.md): Massima confidenza agente
- [agent-edit-discipline.md](./agent-edit-discipline.md): agent edit discipline — puntatore
- [ai-tooling.md](./ai-tooling.md): Strumenti AI nel tema One [orfano]
- [graphify-map.md](./graphify-map.md): One Theme — Mappa Graphify [orfano]
- [second-brain.md](./second-brain.md): second brain — puntatore modulo

#### PHPStan, qualita e test (11)

- [code-quality-tools.md](./code-quality-tools.md): Code Quality Tools - Tema One
- [code-redundancy-audit.md](./code-redundancy-audit.md): Code redundancy audit — One
- [dry-kiss-analysis.md](./dry-kiss-analysis.md): 🎨 DRY & KISS Analysis - Theme One
- [dry-kiss-matr-ente-relationships.md](./dry-kiss-matr-ente-relationships.md): HasMany matr/ente Pattern - DRY + KISS
- [duplicate-methods-report.md](./duplicate-methods-report.md): Report: Metodi con nome duplicato nei moduli e nei temi [dup]
- [duplicate-methods.md](./duplicate-methods.md): Metodi duplicati — One [dup]
- [duplicate_methods.md](./duplicate_methods.md): duplicate-methods (deprecated) [orfano] [dup]
- [duplicate_methods_report.md](./duplicate_methods_report.md): duplicate-methods-report (deprecated) [orfano] [dup]
- [ide-helper-phpdoc-boundary.md](./ide-helper-phpdoc-boundary.md): ide helper — confine PHPDoc tema One [orfano]
- [phpstan-level10-analysis.md](./phpstan-level10-analysis.md): PHPStan nel tema One
- [quality-audit.md](./quality-audit.md): Audit di qualita: tema One [orfano]

#### Git, sync e conflitti (4)

- [git-multi-org-sync-handoff.md](./git-multi-org-sync-handoff.md): Handoff multi-org sync (STORY-003) [orfano]
- [gitmodules-sync-session.md](./gitmodules-sync-session.md): Gitmodules sync session — note modulo/tema [orfano]
- [multi-org-sync-laraxot-provtv.md](./multi-org-sync-laraxot-provtv.md): Sincronizzazione multi-organizzazione (laraxot + provtv) [orfano]
- [no-git-lfs.md](./no-git-lfs.md): Git LFS vietato: linea guida e prototipo .gitattributes [orfano]

#### Bug fix e troubleshooting (2)

- [common-errors.md](./common-errors.md): common errors
- [troubleshooting.md](./troubleshooting.md): Troubleshooting [orfano]

#### Architettura e pattern (5)

- [ARCHITECTURE.md](./ARCHITECTURE.md): One Theme Architecture [orfano] [dup]
- [architecture-rules.md](./architecture-rules.md): architecture rules — Theme One
- [architecture.md](./architecture.md): One Theme Architecture [orfano] [dup]
- [filament-table-architecture.md](./filament-table-architecture.md): Dove si configura la tabella di una Resource Filament [orfano]
- [folio-pages-structure.md](./folio-pages-structure.md): Folio pages — struttura tema One (ptvx)

#### Prodotto, roadmap e pianificazione (14)

- [PRD.md](./PRD.md): Product Requirements Document (PRD) - One Theme [orfano] [dup]
- [cosa-migliorare.md](./cosa-migliorare.md): Cosa migliorare: tema One [orfano]
- [launch-plan.md](./launch-plan.md): Product Launch Plan: One Theme
- [prd.md](./prd.md): PRD: One Theme [dup]
- [product-launch-plan.md](./product-launch-plan.md): One - Product Launch Plan
- [product-requirements.md](./product-requirements.md): Product Requirements Document (PRD)
- [product-strategy.md](./product-strategy.md): One - Product Strategy
- [release-marketing-standard.md](./release-marketing-standard.md): Release e README marketing — One
- [roadmap.md](./roadmap.md): Product Roadmap - One Theme
- [sprint-planning-meeting.md](./sprint-planning-meeting.md): One - Sprint Planning Meeting
- [sprint-planning.md](./sprint-planning.md): Sprint Planning: One Theme
- [strategy.md](./strategy.md): Product Strategy: One Theme
- [tech-spec.md](./tech-spec.md): Technical Specification - One Theme [orfano]
- [user-research.md](./user-research.md): User Research: One Theme

#### Filament, UI e grafici (10)

- [advanced-manage-related-records.md](./advanced-manage-related-records.md): Advanced ManageRelatedRecords - One Theme
- [charts-integration.md](./charts-integration.md): Theme One - Charts Integration
- [filament-admin-sub-navigation.md](./filament-admin-sub-navigation.md): Sub navigation del pannello admin [orfano]
- [filament-resource-schemas-tables.md](./filament-resource-schemas-tables.md): Filament Resource: Schemas e Tables (tema One)
- [filament-version.md](./filament-version.md): Filament Version Declaration — One
- [html2pdf-integration.md](./html2pdf-integration.md): HTML2PDF Integration for Theme One
- [one-migration-themes-boundary.md](./one-migration-themes-boundary.md): Temi — nessuna migrazione owner [orfano]
- [pandoc-guide.md](./pandoc-guide.md): Pandoc Documentation Generation Guide [orfano]
- [readonly-field-styling.md](./readonly-field-styling.md): Readonly Field Styling - UI/UX Pattern
- [theme-analysis.md](./theme-analysis.md): Theme Analysis - Theme One

#### Dati, modelli e schema (2)

- [model-docs-governance.md](./model-docs-governance.md): Theme One Docs Governance
- [schema.md](./schema.md): Module Schema

#### Configurazione, permessi e confini (9)

- [FRAMEWORKS.md](./FRAMEWORKS.md): One — Framework Integration Notes [orfano] [dup]
- [binary-assets.md](./binary-assets.md): Asset binari [orfano]
- [document-root-public-html.md](./document-root-public-html.md): Document root: public_html, non laravel/public [orfano]
- [frameworks.md](./frameworks.md): One — Framework Integration Notes [orfano] [dup]
- [laravel-13-composer-boundary.md](./laravel-13-composer-boundary.md): Laravel 13 Composer boundary for Theme One
- [laravel-13-upgrade.md](./laravel-13-upgrade.md): Upgrade Laravel 13 - Theme One 🐄✨
- [public-path-public-html.md](./public-path-public-html.md): public_path = public_html (tema)
- [spatie-permission-team-context.md](./spatie-permission-team-context.md): Spatie Permission Team Context
- [spatie-permission-teams-boundary.md](./spatie-permission-teams-boundary.md): Spatie Permission teams boundary

#### Indici, standard e meta-documentazione (8)

- [README-en.md](./README-en.md): One: il tema che trasforma complessita in vantaggio operativo [orfano] [dup]
- [changelog.md](./changelog.md): Changelog — One Theme
- [docs-archive-policy.md](./docs-archive-policy.md): docs archive policy — puntatore
- [docs-deduplication.md](./docs-deduplication.md): docs deduplication — tema One
- [naming-conventions.md](./naming-conventions.md): Naming Conventions — One Theme
- [purpose.md](./purpose.md): One — scopo del tema e come raggiungerlo meglio [orfano]
- [readme-en.md](./readme-en.md): One Theme — README (English) [orfano] [dup]
- [scopo.md](./scopo.md): One — scopo, confini e come servirlo meglio [orfano]

### Sospetti duplicati (richiedono approvazione per il consolidamento)

Nessun file e' stato toccato. Proposte di destinazione nella story [swarm-phpstan-modular-docs-org](../../../Modules/Xot/docs/bmad/stories/swarm-phpstan-modular-docs-org.story.md).

- stesso nome normalizzato (maiuscole, `_`/`-`, `-en`, `-report`): [ARCHITECTURE.md](./ARCHITECTURE.md), [architecture.md](./architecture.md)
- stesso nome normalizzato (maiuscole, `_`/`-`, `-en`, `-report`): [FRAMEWORKS.md](./FRAMEWORKS.md), [frameworks.md](./frameworks.md)
- stesso nome normalizzato (maiuscole, `_`/`-`, `-en`, `-report`): [PRD.md](./PRD.md), [prd.md](./prd.md)
- stesso nome normalizzato (maiuscole, `_`/`-`, `-en`, `-report`): [README-en.md](./README-en.md), [readme-en.md](./readme-en.md)
- stesso nome normalizzato (maiuscole, `_`/`-`, `-en`, `-report`): [duplicate-methods-report.md](./duplicate-methods-report.md), [duplicate-methods.md](./duplicate-methods.md), [duplicate_methods.md](./duplicate_methods.md), [duplicate_methods_report.md](./duplicate_methods_report.md)

### Senza front matter (2)

[FRAMEWORKS.md](./FRAMEWORKS.md), [README-en.md](./README-en.md)

<!-- swarm-docs:index:end -->
