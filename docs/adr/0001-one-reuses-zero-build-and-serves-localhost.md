---
title: "ADR — One riusa la build di Zero e serve l'host localhost"
type: decision
status: accepted
created: 2026-11-24
updated: 2026-11-24
decision-makers: [Theme One owner]
module: One
qmd: "ADR One tema sviluppo locale localhost pub_theme build Zero vite themes/Zero"
---

# One riusa la build di Zero e serve l'host localhost

## Contesto

Per lo sviluppo locale serve un tema pubblico selezionabile per l'host `localhost` senza mantenere una seconda catena di build. Zero ha già `vite.config.js`, `tailwind.config.js`, `package.json` e `theme.json`; One no. Come si dà a One uno stile senza duplicare la toolchain?

## Driver della decisione

- Una sola catena di build front end da mantenere (quella di Zero).
- Un tema distinto selezionabile per l'ambiente locale tramite configurazione del tenant.
- Nessuna dipendenza npm propria di One.

## Alternative scartate

- **Una build propria in One** (copiando Vite, Tailwind e `package.json` di Zero): due catene identiche da tenere allineate.
- **Usare Zero anche su `localhost`**: il tenant locale non avrebbe un tema separato su cui sperimentare senza toccare quello usato dagli host reali.

## Decisione

Scelta: **One non ha build propria e carica gli asset compilati di Zero**. Le viste di One chiamano `@vite([...], 'themes/Zero')` (`laravel/Themes/One/resources/views/layouts/app.blade.php:12`, `laravel/Themes/One/resources/views/components/layouts/main.blade.php:46`) e nella cartella non esistono `vite.config.js`, `package.json`, `tailwind.config.js` né `theme.json`. Il tenant `localhost` seleziona One con `'pub_theme' => 'One'` e `'register_pub_theme' => false` (`laravel/config/localhost/xra.php:10,15`); il tenant `local/ptvx` usa Zero (`laravel/config/local/ptvx/xra.php:5-14`).

## Conseguenze

- Buono, perché una sola toolchain produce gli asset di entrambi i temi.
- Buono, perché l'aspetto di One segue Zero senza lavoro aggiuntivo.
- Cattivo, perché One funziona solo se la build di Zero è presente e il symlink `public_html/themes/Zero` esiste (vedi ADR di Zero).
- Cattivo, perché `laravel/Themes/One/public/` contiene `manifest.json` e tre asset propri (`assets/app-*`) che le viste non usano: sono artefatti orfani, non rimossi in questa passata.
- Cattivo, perché le viste di One divergono dal README: dei 20 file Blade di One, 10 differiscono da quelli di Zero (verificato con `cmp`, 2026-11-24), mentre il README dichiara che sono identici byte a byte.

## Conferma

Verifica ripetibile: `rg -n "@vite" laravel/Themes/One --glob '*.blade.php'` deve mostrare solo `'themes/Zero'`; `ls laravel/Themes/One/{vite.config.js,package.json,theme.json}` deve fallire; `laravel/config/localhost/xra.php` deve avere `'pub_theme' => 'One'`. Nessun test Pest copre queste condizioni (il tema non ha cartella `tests/`).
