---
id: quality-gates-phpstan-swarm-2026-09-23
title: "PHPStan gate check — Themes/One (swarm 21 moduli)"
status: done
scope: laravel/Themes/One
created: 2026-09-23
updated: 2026-09-23
---

# PHPStan gate check — Themes/One

## Contesto

Task swarm: 21 agenti paralleli, uno per Modulo/Tema, per eseguire PHPStan e
sistemare le segnalazioni reali, poi git status + BMAD + second brain per
modulo. Questo agente ha lavorato SOLO su `laravel/Themes/One`.

Nota preesistente in `docs/phpstan-level10-analysis.md`: il gate canonico del
progetto gira su `laravel/phpstan.neon` con perimetro `Modules` (non
`Themes`), quindi una corsa scoped su `Themes/One` non è direttamente
equivalente al gate globale. Questa story registra evidenza/comando/esito
della corsa scoped richiesta esplicitamente dal task swarm, senza sostituirsi
al gate canonico.

## Stato git iniziale

- `git status --short --branch` → `## dev`, working tree pulito (nessun file
  modificato o non tracciato).
- `git remote -v` → `laraxot` (github.com/laraxot/theme_one_fila5) e
  `provtv` (github.com/provtv/theme_one_fila5).
- `git branch --show-current` → `dev`.
- `git log -1 --oneline` → `dd8a2d5 Merge remote-tracking branch
  'laraxot/dev' into dev`.
- `git rev-parse --show-toplevel` → termina in `Themes/One` (repo corretto).
- Nessun `.git/MERGE_HEAD`, nessun marker di conflitto.
- Lock: libero all'avvio (`FREE: laravel/Themes/One`), acquisito con motivo
  `phpstan-fix-swarm`, rilasciato a fine task.

## Comando PHPStan eseguito

```bash
cd /var/www/_bases/base_ptvx_fila5/laravel
./vendor/bin/phpstan analyse Themes/One --no-progress --memory-limit=-1
```

Esito: `[OK] No errors`.

Verifica preliminare che lo scope contenesse file reali (per escludere un
verde silenzioso da scope vuoto): 26 file `.php` in `Themes/One` (esclusi
vendor/node_modules), 20 sotto `app/`/`resources`/`src`. Il comando ha quindi
analizzato codice reale, non uno scope vuoto.

## Fix applicati

Nessuno. Nessuna segnalazione PHPStan da risolvere: il modulo è già pulito
sullo scope `Themes/One` con la configurazione condivisa `laravel/phpstan.neon`
(level max).

## Cosa è rimasto aperto e perché

- Nessuna segnalazione aperta.
- Non è stato eseguito un aggiornamento di `qmd`/`graphify` (contesa nota con
  gli altri 20 agenti in parallelo): lasciato al coordinatore di fine swarm,
  come da istruzioni.
- Non toccato `docs/phpstan-level10-analysis.md` né altri contenuti wiki
  esistenti: la nota lì presente resta valida e coerente con questo esito
  (differenza di perimetro `Modules` vs `Themes/One` già documentata).

## Verifica reale finale

Stesso comando rieseguito immediatamente prima della chiusura story, stesso
esito:

```
Note: Using configuration file /var/www/_bases/base_ptvx_fila5/laravel/phpstan.neon.
 [OK] No errors
```

## Pattern riutilizzabile

Per i Temi (a differenza dei Modules pieni di logica applicativa), è utile
verificare prima quanti file `.php` reali esistono nello scope (`find . -iname
"*.php" -not -path "./vendor/*"`) prima di fidarsi di un "No errors": uno
scope vuoto o quasi-vuoto produrrebbe lo stesso output ma senza reale
copertura. In questo caso lo scope aveva 26 file reali, quindi il verde è
attendibile.
