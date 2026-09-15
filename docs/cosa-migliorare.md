---
title: "Cosa migliorare: tema One"
type: report
theme: One
updated: 2026-09-01
qmd: "cosa migliorare one phpstan phpmd phpinsights coverage debito priorita"
---

# Cosa migliorare — tema One

Ogni affermazione qui sotto viene da un comando eseguito il 1 settembre 2026, dopo il
ripristino di `vendor/` a 330 pacchetti. Le misure precedenti a quella data giravano su
un autoloader dimezzato e non valgono.

## I numeri

| | |
|---|---:|
| Errori PHPStan (modulo isolato) | 0 |
| Rilievi PHPMD su `app/` | 0 |
| PHPInsights — Code | 100 % |
| PHPInsights — Architecture | 100 % |
| PHPInsights — Style | 100 % |
| File PHP | 26 |
| Casi di test | 0 |
| Casi di test per file | 0.00 |
| Coverage di riga | **mai misurata** |
| `@phpstan-ignore` | 0 |
| `TODO`/`FIXME`/`HACK` | 0 |
| File `.md` sotto `docs/` | 108 |

## Il quadro

Il tema One ha **PHPInsights 100 % su tutte e quattro le metriche**. E **zero test**,
su 26 file PHP.

Quel 100 % non è un traguardo: è il punteggio di poche decine di righe che nessuno
esercita. Un badge verde su un tema senza test è la forma più educata di bugia che un
progetto possa raccontare a sé stesso.

Ha anche **due file `.code-workspace`**, dove il pilastro 6 ne vuole uno.

## Cosa fare, in ordine di resa

1. **Zero test su 26 file PHP.** Qualunque punteggio di qualità qui descrive la forma del codice, non il suo comportamento.

2. **Alzare la densità di test.** 26 file PHP e 0 casi: 0.00 per file. Non serve un piano di copertura totale, serve un test sui percorsi che si rompono.

## Come rifare ogni numero

```bash
cd laravel
php -d memory_limit=-1 ./vendor/bin/phpstan analyse Themes/One
./tools/phpmd.sh Themes/One/app     # non la root: aborta sulle classi anonime
./tools/phpinsights.sh Themes/One
XDEBUG_MODE=coverage ./vendor/bin/pest Themes/One/tests -c Themes/One/phpunit.xml --coverage --min=0
```

Prima di fidarsi di qualunque numero: il tree deve essere fermo e `vendor/` completo.

```bash
/usr/bin/find Modules -newermt '-70 seconds' -type f | wc -l   # deve dare 0
php -r 'echo count(require "vendor/composer/autoload_classmap.php");'   # ~25358, non 13041
```

Quadro comparativo di tutte le unità: [`docs/quality-audit.md`](../../../../docs/quality-audit.md).

