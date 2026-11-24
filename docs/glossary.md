---
title: "Glossario di dominio Theme One"
type: glossary
owner: One
updated: 2026-11-24
qmd: "glossario Theme One layout blocchi pagine login manifest pub_theme localhost build Zero"
---

# Glossario di dominio Theme One

Termini di presentazione verificati. Se glossario e codice divergono vale il codice. Percorsi relativi a `laravel/Themes/One/`.

| Termine | Significato | Nel codice |
|---|---|---|
| Tema pubblico (`pub_theme`) | Tema del front office; One è il valore per l'host `localhost`. | `laravel/config/localhost/xra.php:10` |
| `register_pub_theme` | Flag di registrazione del tema; vale `false` nel tenant `localhost`. | `laravel/config/localhost/xra.php:15`, `Modules/Xot/app/Datas/XotData.php:65` |
| Layout | Shell Blade delle pagine: `app` e `main`. | `resources/views/components/layouts/`, `resources/views/layouts/app.blade.php` |
| Blocco | Sezione di contenuto riusabile: hero, cta, features, stats, testimonials, links, navigation, sidebar. | `resources/views/components/blocks/` |
| Pagina | Vista di contenuto (`index`, `home`, `auth/login`). | `resources/views/pages/` |
| Widget di login | Vista Filament del widget di accesso. | `resources/views/filament/widgets/auth/login.blade.php` |
| Build di Zero | Gli asset si caricano con `@vite([...], 'themes/Zero')`: One non compila. | `resources/views/layouts/app.blade.php:12`, `resources/views/components/layouts/main.blade.php:46` |
| Sorgenti asset | `resources/css/app.css`, `resources/js/app.js`, `resources/js/bootstrap.js`. | `resources/css/`, `resources/js/` |
| Manifest orfano | `public/manifest.json` di One, non usato dalle viste che puntano a `themes/Zero`. | `public/manifest.json` |
| Layout email | Template HTML per le mail (`base`, `christmas-professional`). | `resources/mail-layouts/` |
| Lingue del tema | Cartelle di traduzione `it`, `en`, `de` (in `it`: `navigation.php`, `ui.php`). | `lang/` |
