# navigationIcon audit + consolidation — Themes (One, Three, Zero) — 2026-10-06

## Epic
Code quality + architecture compliance (navigationIcon via translations, not static).

## Story
Come team di maintenance, vogliamo verificare che **nessun tema** viola la regola navigationIcon (static property vietato), e consolidare le traduzioni di icon dove necessario.

## Acceptance criteria
- [ ] Audit: verificare Themes/One/Three/Zero per `protected static $navigationIcon` (zero trovati atteso)
- [ ] Traduttori: Themes/<Theme>/resources/lang/{locale}/navigation.php contengono icon keys
- [ ] Documentazione: cada tema ha README.md in docs/ che specifica dove vivono i navigation icons
- [ ] Zero violations: phpstan analyse Themes/ non segnala navigation-related issues

## Lavoro tracciato

### Fase 1: Audit navigationIcon (simple scan)
- [ ] Grep: `grep -r "protected static.*\$navigationIcon" laravel/Themes/*/app/Filament/`
- Expected: zero matches (regola già implementata su Modules, assume theme compliance)
- Se trovati: documentare violazioni per fix parallelo

### Fase 2: Docs consolidamento temi
- [ ] Themes/One/docs/, Themes/Three/docs/, Themes/Zero/docs/ hanno struttura coerente?
  - Cartelle: bmad/, wiki/, stories/ (come Modules)?
  - Orphan files? (come Notify 304 orphan su Modules)
  - Tool-specific folders (cursor/, windsurf/, etc.)? → rimuovi se empty
- [ ] Crea/aggiorna Themes/<Theme>/docs/README.md con confini (cosa vive dove)
- [ ] Crea Themes/<Theme>/docs/wiki/index.md (navigation reference)

### Fase 3: PHPStan themes
- [ ] Verifica: `phpstan analyse Themes/ --no-progress` → 0 errors atteso
- Se errori: classificar per tema + assegna cluster fix parallelo (come Modules)

## References
- Rule: [[xotbaseresource-navigationicon-via-translations-not-static]]
- Modules audit: phpstan-fleet-remediation-2026-10-06 (Modules clean, 0 errors)
- Docs audit Modules: a9fbfbb202ff7709b subagent (orphan file consolidation)

## Stato
⏳ BACKLOG → ready-for-dev

## Assegnazione
Unassigned. Handoff per prossimo agente/sessione.

