---
title: "Folio pages — struttura tema One (ptvx)"
type: concept
tags: [folio, pages, theme-one, ptvx, auth, dry, kiss]
created: 2026-07-22
updated: 2026-07-22
qmd: "folio pages structure theme one ptvx auth home index no semantic directories"
issues:
  - https://github.com/provtv/base_ptv_fila5/issues/124
discussions:
  - https://github.com/laraxot/base_fixcity_fila5/discussions/273
related:
  - ../wiki/concepts/theme-one-operating-focus.md
  - ../../../../docs/wiki/rules/no-semantic-folio-page-directories.md
  - ../../Zero/docs/folio-pages-structure.md
  - ../../../../bashscripts/tools/verify-no-semantic-folio-pages.sh
---

# Folio pages — Theme One (ptvx)

## Scopo

Definire **cosa può vivere** in `resources/views/pages/` per questo tema, e perché.

## Contesto ptvx vs Fixcity

| Base | Tema tipico | Pattern FO |
|------|-------------|------------|
| **ptvx** (questo repo) | One, Zero, Three | `auth/` + `home`/`index` — **niente** Sixteen |
| Fixcity | Sixteen | `[container0]/[slug0]` + CMS JSON + widget modulo |

La regola «no cartelle semantiche» è **condivisa**. Il pattern `container0` è **opzionale** qui finché non si adotta CMS containerizzato.

## Layout attuale (fatto verificato)

```text
resources/views/pages/
├── auth/login.blade.php   # ammesso — shell login FO
├── home.blade.php
└── index.blade.php
```

## Vietato

Creare `pages/tickets`, `pages/news`, `pages/dashboard`, `pages/profile`, …  
Dominio editoriale → **modulo owner** (Filament widget / CMS), non cartella nel tema.

## Chi verifica

- Script: [`verify-no-semantic-folio-pages.sh`](../../../../bashscripts/tools/verify-no-semantic-folio-pages.sh)
- Pest: `laravel/tests/Unit/NoSemanticFolioPageDirectoriesTest.php` (PHPStan/PHPMD/Insights OK)
- Canon root: [no-semantic-folio-page-directories](../../../../docs/wiki/rules/no-semantic-folio-page-directories.md)
- Post-edit: [validation-post-edit-rule](../../../../docs/wiki/rules/validation-post-edit-rule.md)

## Provenienza (studio, non restore)

Contratto originale studiato da **base_fixcity** Theme Sixteen (`page-directory-structure.md`: solo `[container0]`, `auth`, `tests`) e dallo script sibling Fixcity.  
Su ptvx si **avanza**: stesso divieto semantic dirs; senza obbligo Sixteen. Git: solo `log`/`show` — mai restore/checkout/reset ([git-forward-only](../../../../docs/wiki/rules/git-forward-only.md)).

## Prima di editare `pages/`

1. Leggere questo file + operating focus del tema.
2. `rg` chiamanti / rotte Folio (`folio:list` se serve URL).
3. Se serve contenuto di dominio → modulo, non `mkdir pages/<dominio>`.
