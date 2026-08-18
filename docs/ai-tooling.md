---
title: "Strumenti AI nel tema One"
type: guide
tags: [ai-tooling, graphify, headroom, caveman, tema]
created: 2026-08-03
updated: 2026-08-03
qmd: "graphify headroom caveman tema One blade indicizzazione scaffold"
related:
  - ../../../Modules/Xot/docs/ai-tooling-stack.md
  - ../../Zero/docs/no-ai-tool-scaffold-dirs.md
---

# Strumenti AI nel tema One

Canonico dello stack (versioni, installazione, configurazione):
[Xot — ai-tooling-stack](../../../Modules/Xot/docs/ai-tooling-stack.md). Qui solo ciò che cambia
per un tema.

## graphify su un tema

One contiene 20 blade e 26 file PHP fra `app/`, `resources/` e `lang/`. Indicizza i sorgenti, non
la root:

```bash
graphify update laravel/Themes/One/resources
graphify update laravel/Themes/One/app
graphify query "quali view estendono il layout base" \
  --graph laravel/Themes/One/resources/graphify-out/graph.json
```

`public/` va escluso sempre: contiene asset compilati, non sorgenti.

## La trappola: scaffold nel tema

`graphify update <path>` scrive `<path>/graphify-out/`, cioè crea una cartella di cache dentro il
tema. Il tema vive anche come repo Git indipendente, quindi quella cartella finirebbe nel suo
storico: vedi [no-ai-tool-scaffold-dirs](../../Zero/docs/no-ai-tool-scaffold-dirs.md), regola
canonica [module-theme-root-cleanup](../../../../docs/wiki/rules/module-theme-root-cleanup.md).

Mitigazione applicata: `graphify-out/` e `.headroom/` sono nel `.gitignore` del tema.

## headroom e caveman

Nessuna configurazione per tema: headroom comprime output di tool a livello di monorepo, caveman
agisce sulle risposte dell'agente. Non tenere caveman attivo mentre si scrivono label, traduzioni o
testi di pagina — quel testo lo leggono gli utenti finali.
