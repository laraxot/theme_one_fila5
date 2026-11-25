---
title: "public_path = public_html (tema)"
type: memory
tags: [public_path, public_html, themes, assets]
created: 2026-09-01
updated: 2026-09-01
qmd: "public_path public_html themes vite copy"
related:
  - ../../../../../bashscripts/ai/wiki/memories/frontend-themes-css.md#public-path-is-public-html
  - ./binary-assets.md
---

# Document root per i temi

Gli asset del tema dopo `npm run build` + `symlink public_html/themes (npm run copy obsoleto)` devono finire in **`public_html/themes/{Theme}/`**.

`public_path()` Laravel punta a `public_html/`, **non** a `laravel/public/`.

SSoT: [public-path-is-public-html](../../../../../bashscripts/ai/wiki/memories/frontend-themes-css.md#public-path-is-public-html) · skill [public-path-public-html](./public-path-public-html.md).
