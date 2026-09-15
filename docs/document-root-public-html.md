---
title: "Document root: public_html, non laravel/public"
type: rule
theme: One
created: 2026-09-01
updated: 2026-09-01
qmd: "public_path public_html document root tema one asset vite publish"
related:
  - "../../../Modules/Xot/docs/wiki/rules/public-path-public-html.md"
  - "../../../../docs/wiki/rules/public-path-public-html.md"
---

# Document root: `public_html`, non `laravel/public`

**Regola canonica**: [Modules/Xot/docs/wiki/rules/public-path-public-html.md](../../../Modules/Xot/docs/wiki/rules/public-path-public-html.md)

## In una riga

`public_path()` risolve `{repo}/public_html/`. **Mai** `{repo}/laravel/public/`.

L'applicazione sta in `laravel/`, ma il web server serve `public_html/` un livello sopra.
`App\Application::publicPath()` lo garantisce, e `laravel/bootstrap/app.php` istanzia quella
classe e non quella stock di Laravel.

## Cosa significa per questo tema

Il tema pubblica gli asset con `public_path('themes/one/...')` — vedi `docs/html2pdf-integration.md`, dove il logo del PDF si risolve con `public_path('themes/one/assets/logo.png')`.

## Come si sbaglia

Usare `base_path('public')` o scrivere `laravel/public/` a mano. Entrambi puntano a una
cartella che il web server **non serve**: gli asset finiscono fuori dalla radice pubblica e
tornano 404 in produzione, senza un solo errore nei log.

Usare sempre `public_path()`. E' l'unico punto che conosce la deviazione.

## Guardia

`Modules/Xot/tests/Unit/PublicPathTest.php` — verifica sia il risultato sia il meccanismo.
Se qualcuno rimuove l'override, la suite diventa rossa prima del deploy.
