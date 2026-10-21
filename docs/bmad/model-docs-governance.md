---
title: "Theme One Docs Governance"
type: rule
tags: ['theme', 'model-docs-governance']
created: 2026-07-14
updated: 2026-07-14
qmd: "theme one docs governance"
related:
  - "./advanced-manage-related-records.md"
  - "./agent-confidence-discipline.md"
  - "./agent-confidence-protocol.md"
---

# Theme One Docs Governance

## Objectives

1. Keep docs discoverable with stable filenames.
2. Keep module references aligned with real PHP class names.

## Rules

1. Use `kebab-case` filenames for new docs.
2. If a module model is singular (for example `Scheda`), docs in themes must reference the singular class name.
3. Keep one canonical doc per topic; move alternates to archive folders.
4. Maintain `README.md` as the canonical entrypoint for this folder.
5. Cross-module models (es. `Progressioni\Models\Scheda` che estende Ptv): documentare sempre la connessione DB del consumer, non quella ereditata. Vedi [common-errors](./common-errors.md#modello-scheda-su-database-errato-progressioni) e [database-connection-progressione](../../../Modules/Progressioni/docs/database-connection-progressione.md).
