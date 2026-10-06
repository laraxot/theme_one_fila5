---
title: "public_path = public_html (tema)"
type: memory
tags: [public_path, public_html, themes, assets]
created: 2026-09-01
updated: 2026-09-01
qmd: "public_path public_html themes vite copy"
related:
  - ../../../../docs/wiki/memories/public-path-is-public-html.md
  - ./binary-assets.md
---

# Document root per i temi

Gli asset del tema dopo `npm run build` + `npm run copy` devono finire in **`public_html/themes/{Theme}/`**.

`public_path()` Laravel punta a `public_html/`, **non** a `laravel/public/`.

SSoT: [public-path-is-public-html](../../../../docs/wiki/memories/public-path-is-public-html.md) · skill [public-path-public-html](../../../../docs/wiki/skills/public-path-public-html.md).
