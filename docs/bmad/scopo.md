---
title: "One — scopo, confini e come servirlo meglio"
type: concept
theme: One
status: active
created: 2026-09-02
updated: 2026-09-02
tags: [scopo, confini, tema, duplicazione, build, folio, public-html]
qmd: "scopo tema one duplicato zero localhost pub_theme senza vite tailwind css spuri xotcov dfa"
---

# One — scopo, confini e come servirlo meglio

## Lo scopo, dedotto dal codice

Il `composer.json` di One si descrive da sé: *"minimal theme skeleton for future
frontend development and customization"*, keywords `skeleton`, `placeholder`. Il codice
conferma: `app/` contiene solo `.gitkeep`, non c'è `theme.json`, non c'è
`package.json`, non c'è `vite.config.js`, non c'è `tailwind.config.js`, non c'è
`postcss.config.js`.

Un solo file di configurazione lo nomina:

```
config/localhost/xra.php:10    'pub_theme' => 'One',
```

Su `localhost`, e solo lì. Tutti gli host reali — `tv/prov/personale2022`,
`tv/prov/personale2019`, `ptvx`, `ptvx-mono` — selezionano Zero.

Da qui la formulazione in una riga:

> **One è il tema di sviluppo locale: la stessa superficie di Zero, servita su
> `localhost`, senza la catena di build che la produrrebbe.**

## I confini, e dove oggi sono rotti

### 1. One non è una variante di Zero: ne è una copia

Confronto byte a byte, 2026-09-02, di `resources/views/` fra i due temi:

| Esito | File |
|---|---:|
| **Identici** | **20 su 20** |
| Diversi | 0 |
| Presenti solo in One | 0 |
| Presenti solo in Zero | 2 (`components/layouts/guest.blade.php`, `components/ui/logo.blade.php`) |

Non c'è una riga di markup che distingua i due temi. One è un sottoinsieme proprio di
Zero, e per giunta di due file. Lo stesso vale per gli asset compilati:

```bash
diff -r Themes/One/public Themes/Zero/public   # nessuna differenza
```

`Themes/One/public/assets/` contiene `app-BZ_zeBx9.css`, `app-BkX4OJ4C.css`,
`app-Cgiyjb0t.js` — gli **stessi hash** di Zero. One non ha `vite.config.js` né
`package.json`: quei file non possono essere stati compilati qui. Sono stati copiati.

Un tema che è la copia di un altro non è una scelta di design: è la duplicazione che il
concetto stesso di tema doveva evitare. Se il front office locale deve essere
identico a quello di produzione, la configurazione giusta è
`config/localhost/xra.php: 'pub_theme' => 'Zero'` — una riga invece di un albero.

### 2. 42 file CSS spuri in `resources/css/`

`resources/css/` contiene 43 file. Uno è `app.css`. Gli altri 42 sono:

| Prefisso | File | Contenuto |
|---|---:|---|
| `xotcov-<hex>.<hex>.css` | 20 | `a{}` |
| `dfa-<hex>.<hex>.css` | 22 | `a{}` |

Ogni file contiene tre caratteri: un selettore vuoto. Sono artefatti di esecuzioni di
test o di tool di coverage finiti nella cartella sorgente del tema e committati.
Occupano 176 KB e, se One avesse una build Tailwind, entrerebbero nel `content` glob
`./resources/**/*.css`.

Non è un problema di spazio: è che la cartella sorgente di un tema è diventata una
directory temporanea, e nessuno se n'è accorto per 42 file.

### 3. La build non esiste, ma il `tailwind.config.js` sì — in un altro modulo

One non ha `tailwind.config.js`. Ne esiste però uno che parla di lui:

```
Modules/UI/resources/views/themes/one/tailwind.config.js
```

Un file di configurazione di build, dentro `resources/views/` di un modulo, in una
cartella `themes/one/`. Non è raggiungibile da nessuna pipeline (non c'è pipeline), non
è una view Blade, e mette UI a conoscenza di un tema — esattamente la direzione di
dipendenza che il README di UI vieta.

### 4. Le pagine Folio non sono montate

`resources/views/pages/` contiene `index.blade.php`, `home.blade.php`,
`auth/login.blade.php`. L'unico `Folio::path` del progetto è
`app/Providers/FolioServiceProvider.php:23`, che monta `resource_path('views/pages')` —
cioè `laravel/resources/views/pages`, **0 file**. Le tre pagine di One non generano
rotte.

Il vincolo di progetto è rispettato: sotto `pages/` ci sono solo shell generiche e
`auth`, nessuna cartella di dominio.

### 5. Il README promette artefatti che non ci sono

`README.md` linka `./.github/workflows/semantic-release.yml` e `./changelog.md`.
`Themes/One/.github/` non esiste e il changelog è `CHANGELOG.md`, maiuscolo. Lo stesso
testo — "il tema che trasforma complessita in vantaggio operativo", "Release
automation", "Filosofia" — compare identico nei README di Three e Zero: è un modello
compilato, non una descrizione.

## Come servire meglio lo scopo

### 1. Decidere se One deve esistere

La domanda viene prima di ogni pulizia, perché ne cambia l'esito. Due risposte
legittime:

- **No**: `config/localhost/xra.php:10` diventa `'pub_theme' => 'Zero'` e
  `Themes/One/` si archivia. Costo: una riga. Beneficio: sviluppo locale su ciò che gira
  in produzione.
- **Sì**, come banco di prova per un restyling: allora deve **divergere** da Zero, avere
  la sua build, e la prima divergenza va scritta prima di qualunque altra cosa.

Lo stato attuale — copia identica senza build — non è nessuna delle due.

```bash
cd laravel
diff -rq Themes/One/resources/views Themes/Zero/resources/views   # oggi: 0 differenze sui 20 file comuni
grep -n "pub_theme" config/localhost/xra.php
```

### 2. Cancellare i 42 CSS spuri e impedirne il ritorno

```bash
cd laravel/Themes/One
ls resources/css | grep -cE '^(xotcov|dfa)-'          # 42 oggi, obiettivo: 0
grep -rl '^a{}$' resources/css | wc -l                # obiettivo: 0
grep -nE 'xotcov|dfa-' .gitignore                     # la riga che li tiene fuori
```

Una riga in `.gitignore` (`resources/css/xotcov-*.css`, `resources/css/dfa-*.css`) non
basta: va capito quale tool li scrive nella cartella sorgente e fermato lì. Un
`.gitignore` che nasconde un artefatto mal collocato risolve il sintomo.

### 3. Spostare o cancellare `Modules/UI/resources/views/themes/one/tailwind.config.js`

Se One avrà una build, quel file va in `Themes/One/tailwind.config.js`. Se non l'avrà, va
cancellato. In nessuno dei due casi resta dentro UI.

```bash
cd laravel
ls Modules/UI/resources/views/themes/ 2>/dev/null      # obiettivo: la cartella non esiste
ls Themes/One/tailwind.config.js 2>/dev/null           # se One resta e ha una build
```

### 4. Non pubblicare asset che non si compilano

`Themes/One/public/assets/` contiene tre file con gli hash di Zero. Vanno rimossi
insieme al resto se One si archivia; se One resta, vanno rigenerati dalla sua build. Un
`manifest.json` che punta a bundle prodotti da un altro tema è una bugia che il browser
non può smascherare.

```bash
cd laravel
diff -r Themes/One/public Themes/Zero/public   # obiettivo: One/public assente, o diverso
```

### 5. Correggere i due link morti del README

```bash
cd laravel/Themes/One
ls .github/workflows/semantic-release.yml changelog.md 2>&1   # o esistono, o si tolgono i link
```

## Cosa NON è compito di One

- **Non** è il tema di produzione: quello è Zero, per `config/local/tv/prov/*/xra.php`.
  Ogni funzionalità sviluppata solo qui non arriva all'utente.
- **Non** contiene PHP: `app/` ha solo `.gitkeep`, e va lasciato così.
- **Non** ospita pagine di dominio. Sotto `resources/views/pages/` vanno shell generiche
  e `auth`; una cartella `tickets/`, `news/`, `services/` significa che una feature è
  finita nel guscio invece che nel modulo che la possiede.
- **Non** è una cartella di lavoro: `resources/css/` è sorgente, non output di test.
- **Non** scrive in `laravel/public`. Il `public_path()` di questo progetto è
  `public_html/` (`laravel/app/Application.php:16-18`), come da SSoT
  [`public-path-is-public-html`](../../../../docs/wiki/memories/public-path-is-public-html.md).
- **Non** è una libreria di componenti: quelli condivisi stanno in `Modules/UI`.

## Verifica

```bash
cd laravel

# chi seleziona questo tema
grep -rn "pub_theme" config/local config/localhost --include='xra.php'

# One è ancora una copia di Zero?
diff -rq Themes/One/resources/views Themes/Zero/resources/views
diff -r  Themes/One/public          Themes/Zero/public

# CSS spuri
ls Themes/One/resources/css | grep -cE '^(xotcov|dfa)-'    # 42 oggi, obiettivo: 0
du -sh Themes/One/resources/css                            # 176K oggi

# il tema non contiene PHP
find Themes/One/app -name '*.php' | wc -l                  # deve restare 0

# pages: solo shell generiche + auth
find Themes/One/resources/views/pages -type d | sort       # atteso: pages, pages/auth
grep -rn "Folio::path" app Modules --include='*.php'       # oggi: 1 sola riga, non punta ai temi

# config di build fuori posto
ls Modules/UI/resources/views/themes/ 2>/dev/null          # obiettivo: non esiste

# nessun riferimento a laravel/public
grep -rn "laravel/public\b" Themes/One --include='*.js' --include='*.json' --include='*.php'
```

## Collegamenti

- [Themes/Zero/docs/scopo.md](../../Zero/docs/scopo.md) — il tema di cui One è la copia
- [Themes/Three/docs/scopo.md](../../Three/docs/scopo.md) — il terzo tema, un file
- [public-path-is-public-html](../../../../docs/wiki/memories/public-path-is-public-html.md) — perché non esiste `laravel/public`
- [Modules/UI/docs/scopo.md](../../../Modules/UI/docs/scopo.md) — dove vivono i componenti condivisi
