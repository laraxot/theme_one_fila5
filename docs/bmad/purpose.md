---
title: "One — scopo del tema e come raggiungerlo meglio"
type: concept
document_type: concept
theme: One
status: active
version: 1.0.0
language: it-IT
created: 2026-09-09
updated: 2026-09-09
tags: [tema, purpose, fork, non-attivo, blade, allineamento]
qmd: "tema One scopo fork di Zero due file di scarto non attivo pub_theme Zero epics.md story storage policy sbagliata"
issues:
  # DA CREARE — nessun numero inventato. gh issue create --repo $(git remote -v)
  - "https://github.com/provtv/theme_one_fila5/issues/"
discussions:
  - "https://github.com/provtv/base_ptv_fila5/discussions/"
related:
  - ../../Zero/docs/purpose.md
  - ../../Three/docs/purpose.md
  - ../../../../docs/epics.md
maintainer: Laraxot
license: project-internal
---

# One — perché esiste

## Lo scopo in una frase

**One è un fork di Zero che differisce per due file e non è il tema servito**: la
configurazione punta a `Zero`, mentre la documentazione di progetto continua a indicare One.

## L'evidenza

| Fatto | Misura |
|---|---|
| Non è il tema attivo | `config('xra.pub_theme') === 'Zero'` |
| Non si dichiara tema | **manca `theme.json`** — Zero ce l'ha |
| Non ha pipeline di build | nessun `vite.config.js`, `tailwind.config.js`, `package.json` |
| Ha la superficie | 20 `.blade.php`, 48 fra css e js |
| Ha le traduzioni | `lang/{it,en,de}/{navigation,ui}.php` — **le stesse sei di Zero** |

## La differenza con Zero, misurata

L'elenco dei blade coincide **tranne due file**, presenti solo in Zero:

```
resources/views/components/layouts/guest.blade.php
resources/views/components/ui/logo.blade.php
```

Tutto il resto ha lo stesso percorso. Non è «un altro tema»: è la stessa superficie meno un
layout guest e un logo, senza `theme.json` e senza build.

## Perché conta, ed è la ragione per cui questo file esiste

`docs/epics.md`, sezione *Story Storage Policy*, dice: «Il tema pubblico configurato e `One`,
quindi le story del portale staff vanno in `laravel/Themes/One/docs/stories/`».

**È falso rispetto alla configurazione.** Chi segue quella riga scrive le story del portale nel
tema che non viene servito. Le tre story oggi presenti in `Themes/One/docs/stories/` sono lì
per quella premessa.

Va deciso, non dedotto: o la config passa a One, o `epics.md` va corretto.

## Come raggiungerlo meglio

### 1. Chiudere la domanda: fork o tema?

Due esiti possibili, entrambi legittimi, nessuno dei due è lo stato attuale:

- **è un tema**: allora gli servono `theme.json`, la pipeline di build e una ragione di
  esistere diversa da Zero — cioè almeno una scelta visiva propria;
- **è un residuo**: allora va marcato tale, e le story vanno ricollocate nel tema attivo.

Oggi non è né l'una né l'altra cosa, e la documentazione lo tratta come il tema principale.

### 2. Nessuno tiene allineati i due fork

Due file di scarto oggi. Nessun test, nessuna guardia: la prossima modifica a un componente di
Zero non arriva qui, e viceversa. Se i due temi devono restare, serve una guardia sulla
divergenza; se non devono, serve la decisione del punto 1.

## Confini

Gli stessi di [Zero](../../Zero/docs/purpose.md): la logica di dominio sta nei moduli, le
classi base Filament in `Xot`, le traduzioni di dominio nei `lang/` dei moduli.

## Collegamenti

- [Zero — scopo](../../Zero/docs/purpose.md) — il tema attivo, da cui One differisce per due file
- [Three — scopo](../../Three/docs/purpose.md)
- [docs/epics.md](../../../../docs/epics.md) — la Story Storage Policy da correggere
