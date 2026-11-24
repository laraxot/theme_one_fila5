---
title: "INDEX contratti — Theme One"
type: index
owner: One
updated: 2026-11-24
qmd: "Theme One contract INDEX backlog presentation-contract layout"
---

# INDEX contratti — Theme One

| Operazione | Contract | Classe | Invarianti | Copertura | Comando |
|---|---|---|---|---|---|
| — | Nessun contract (vedi [README](README.md)) | — | — | — | — |

Verifica: il tema non ha cartella `tests/` e `rg -n "group\('ONE-" laravel/Themes/One` non dà risultati (2026-11-24).

## Backlog contract

Nessun candidato oggi: le viste di One sono in gran parte copie di quelle di Zero (10 su 20 file Blade identici byte a byte, 10 divergenti, verificato con `cmp` il 2026-11-24). Se le divergenze diventano intenzionali, documentare prima la superficie divergente (es. `pages/auth/login.blade.php`, `components/navigation.blade.php`).

Totale Action di dominio: 0. Viste Blade del tema: 20 file `.blade.php`.
