---
title: "PHPStan nel tema One"
type: guide
tags: ['phpstan']
created: 2026-07-14
updated: 2026-08-24
qmd: "phpstan theme one level max modules effective scope no suppression"
related:
  - "./advanced-manage-related-records.md"
  - "./agent-confidence-discipline.md"
  - "./agent-confidence-protocol.md"
---

# PHPStan nel tema One

## Contratto effettivo

Il gate canonico del progetto usa `laravel/phpstan.neon`, che configura `level: max` e
il perimetro `Modules`. Non aggiungere `--level`, configurazioni locali, baseline,
esclusioni o `@phpstan-ignore` per ottenere un verde artificiale.

```bash
cd laravel
./vendor/bin/phpstan analyse Modules --memory-limit=-1 --no-progress
```

Il comando non certifica autonomamente tutti i file PHP del tema. Se una modifica al
tema è raggiunta da un consumer dei moduli, la diagnostica entra nel gate globale; negli
altri casi servono test e controlli mirati dichiarati nella story che possiede la modifica.

## Quando usare
- Prima di rilasci o merge importanti.
- Dopo modifiche a file PHP nel tema o nelle sue dipendenze.

## Evidenza, non memoria

Non conservare dichiarazioni permanenti come “0 errori”: registrare comando, data, exit
code e perimetro nel Dev Agent Record della story. Una corsa su `Themes/One` con una
configurazione diversa non è confrontabile con il gate `Modules`.

## Note
Se il tema contiene solo documentazione o asset statici, indicare esplicitamente che non ci sono file PHP da analizzare.

## Collegamenti correlati
- [roadmap](./roadmap.md)
- [common errors](./common-errors.md)
- [code quality tools](./code-quality-tools.md)
- [theme analysis](./theme-analysis.md)
- [README](./README.md)
