---
title: "common errors"
type: guide
tags: ['filament', 'phpstan']
created: 2026-07-14
updated: 2026-07-14
qmd: "common errors"
related:
  - "./advanced-manage-related-records.md"
  - "./agent-confidence-discipline.md"
  - "./agent-confidence-protocol.md"
---

# common errors

## filament form schema senza chiavi (novembre 2025)

- **Sintomo**: nei form Progressioni alcune section risultano vuote o l'ordinamento dei campi è incoerente; PHPStan segnala `array<int, Component>` invece di `array<string, Component>`.
- **Causa**: le risorse Filament del modulo restituivano array numerici; Filament nel tema One non riesce a mappare correttamente le colonne quando il form arriva senza chiavi.
- **Soluzione rapida**: ogni voce del form deve essere referenziata con una chiave stabile (`'general' => Section::make(...)`). Vedi [analisi Progressioni](../../Modules/Progressioni/docs/phpstan-errors-analysis.md#avanzamento--tipizzazione-getformschema-novembre-2025).
- **Impatto tema**: gli stylesheet del tema One assumono la presenza di chiavi per applicare le classi Tailwind dinamiche; senza chiavi, alcuni componenti ricevono classi errate. Dopo l'allineamento delle risorse, non è necessario modificare ulteriormente il tema, ma monitorare questo file per regressioni future.

## GroupColumn con campi relazionali

- **Sintomo**: in tabelle con `GroupColumn` alcune righe risultano vuote quando il campo è relazionale (es. `valutatore.nome_diri`).
- **Causa tecnica**: le colonne figlio nel `GroupColumn` non sono montate alla tabella Filament, quindi `getState()` non funziona. La view usa `data_get()` come fallback per risolvere la dot notation.
- **Soluzione**:
  1. Assicurarsi che la relazione sia caricata con **eager loading** nella query della tabella:
     ```php
     public static function getEloquentQuery(): Builder
     {
         return parent::getEloquentQuery()->with(['valutatore']);
     }
     ```
  2. In alternativa, usare un **accessor piatto** sul modello o una **TextColumn standard** fuori da GroupColumn.
- **Riferimento**: dettagli completi in [group-column-fix](../../../Modules/UI/docs/group-column-fix.md).

## modello Scheda su database errato (progressioni)

- **Sintomo**: liste Filament Progressioni vuote, relazioni `valutatore`/`schede` incoerenti, o query che colpiscono il DB `ptv` invece di `progressione`.
- **Causa**: `Scheda` estende `Ptv\Models\BaseScheda` e senza override eredita `protected $connection = 'ptv'`.
- **Soluzione**: `protected $connection = 'progressione';` sul modello consumer. Vedi [database-connection-progressione](../../../Modules/Progressioni/docs/database-connection-progressione.md).
- **Impatto tema**: il tema One non configura connessioni DB; il fix è solo lato modulo Progressioni/Ptv. Monitorare questo file se compaiono dati mancanti dopo refactor cross-modulo.

## Resource Filament su connessione errata per `getPages()` cross-module

- **Sintomo**: rotta di un pannello (es. `progressioni/admin/rating-morphs`) va in errore `SQLSTATE[42S02] Base table or view not found ... (Connection: rating, Database: ptv_lara)`, e il route controller punta a `Modules\Rating\...\Pages\ListRatingMorphs` invece che alle Page del modulo corrente.
- **Causa**: il base Resource astratto del modulo Rating (`BaseRatingResource`/`BaseRatingMorphResource`), esteso da Progressioni, override `getPages()` ritornando le Page del modulo Rating → il pannello risolve `Rating\RatingMorph` (conn `rating`) invece di `Progressioni\RatingMorph` (conn `progressione`).
- **Soluzione**: rimuovere `getPages()` dalle basi condivise (auto-resolve via `static::class\Pages\`); ogni modulo consumer deve avere le proprie Page con `$resource` puntato alla Resource del proprio modulo. Vedi [Xot — getPages cross-module](../../../Modules/Xot/docs/filament/getpages-redundancy-rule.md) e [database-connection-progressione](../../../Modules/Progressioni/docs/database-connection-progressione.md).
- **Nota correlata**: le Resource che estendono `XotBaseResource` non devono dichiarare `$navigationIcon` (né altri attributi gestiti dal LangServiceProvider). Vedi [forbidden-resource-attributes](../../../Modules/Xot/docs/forbidden-resource-attributes.md).
- **Impatto tema**: nessuna modifica lato tema; il fix è architetturale lato Resource/Page.

## Colonna mancante su `stabi_dirigente` per connection (import valutatori)

- **Sintomo**: da `progressioni/admin/stabi-dirigentes` l'import valutatori esplode con `SQLSTATE[42S22] Column not found: 1054 Unknown column 'email' in 'where clause' (Connection: progressione, Database: progressione_new)`.
- **Causa**: `Modules\Ptv\Filament\Actions\Header\ImportValutatoriAction` è codice di piattaforma e presuppone il contratto colonne di `stabi_dirigente` (`email`, `valutatore_id`, `nome_diri`, `ente`, `matr`). Ogni modulo ha la **propria** tabella `stabi_dirigente` su una **propria** connection e le sei tabelle sono divergenti; Progressioni non aveva neppure la migrazione del modello, quindi lo schema non era descritto da nessun file del repo.
- **Soluzione**: migrazione per modello (`*_create_stabi_dirigentes_table.php`) con `tableUpdate()` idempotente che aggiunge `email` nullable dove manca. I dati sono sacri: solo aggiunte, nessun `migrate:fresh`/`--force`, righe storiche con `email` a `NULL`. Vedi [contratto stabi_dirigente](../../../Modules/Ptv/docs/stabi-dirigente-contract.md) e [piano Progressioni](../../../Modules/Progressioni/docs/stabi-dirigente-email-column.md).
- **Impatto tema**: nessuno — il tema One non definisce colonne né connessioni. Voce qui perché il sintomo si manifesta nelle tabelle Filament renderizzate dal tema e viene spesso scambiato per un problema di vista.

## Sezioni di form ricopiate invece che composte

- **Sintomo**: modificando un blocco di campi (es. anagrafica lavoratore, periodo dal/al/anno) l'aggiornamento compare in un pannello e non negli altri; oppure due pannelli mostrano lo stesso blocco con campi leggermente diversi.
- **Causa**: il form dichiara i campi inline invece di comporre i componenti di `Modules/Ptv/app/Filament/Forms/Components/`. Nel monorepo `TextInput::make('cognome')` compare in 32 file, `stabi_txt` in 18, `dal` in 17: ogni copia diverge per conto suo.
- **Soluzione**: estrarre il blocco in un componente che estende `XotBaseSection` e comporlo (`WorkerSection::make('lavoratore')`, `PeriodoSection::make('periodo')->add([...])`). Vedi [regola vocabolario componenti](../../../../docs/wiki/rules/filament-form-components-vocabulary.md) e [caso scheda](../../../Modules/Ptv/docs/form-components-scheda.md).
- **Impatto tema**: il tema One stila `Section` tramite le classi Filament standard, quindi un componente custom che estende `XotBaseSection` eredita lo stile senza modifiche. Attenzione a un solo punto: una `Section` **senza heading** non renderizza l'header, e nel tema questo cambia visibilmente la spaziatura del box — per questo ogni componente imposta un heading di default.

## Date `dal`/`al` mostrate come `2026-01-01 00:00:00` invece di `20260101`

- **Sintomo**: in tabelle e form di un modulo le date `dal`/`al` compaiono in formato datetime, mentre negli altri pannelli sono numeri a 8 cifre; oppure `TypeError: getDalAttribute(): Argument #1 must be of type ?int, string given`, o ancora `Declaration ... getDalAttribute() must be compatible with ...` (fatale sull'intero modulo).
- **Causa**: nel progetto `dal` e `al` sono **interi AAAAMMGG**, perché le colonne data di Sigma (`qua2kd`, `rep2kd`, `asz2kd`, `st2kas`) sono intere e ogni confronto scheda ↔ anagrafica passa da lì. Un modulo che le tratta come `Carbon` (cast `datetime`, `Carbon::parse()`, `Carbon::createFromDate()`) rompe il contratto dichiarato da `Ptv\...\SchedaMutator::getDalAttribute(?int): ?int`.
- **Soluzione**: cast `'dal' => 'integer'`, gemelli `getDal()`/`getAl()` che ritornano `(int) $carbon->format('Ymd')`, assegnazioni `($anno * 10000) + 101`. Vedi [dal-al-integer-yyyymmdd](../../../Modules/IndennitaCondizioniLavoro/docs/dal-al-integer-yyyymmdd.md).
- **Impatto tema**: nessuna modifica al tema — le colonne Filament stampano lo scalare così com'è. Se serve una data leggibile a schermo, la formattazione va fatta nella colonna/entry (`->formatStateUsing()`), non cambiando il tipo sul modello.

## Campi calcolati vuoti nel form scheda (`propro`, `posfun`, `categoria_ecoval`)

- **Sintomo**: nel form scheda alcuni campi restano vuoti su tutte le righe; il pulsante di ricalcolo risponde "Metodo getX non disponibile sul record".
- **Causa**: il modello ha il calcolo (`getPropro()`) ma non l'accessor che lo invoca (`getProproAttribute()`), oppure non ha nessuno dei due (`posfun`). Il valore non viene mai calcolato, la colonna resta `NULL` e le catene che partono da lì si spengono in silenzio — `getGgCatecoInSede()`, `getGgCatecoFuoriSede()` e `getCategoriaEcoval()` iniziano tutte con `if ($this->propro == null) { return null; }`.
- **Soluzione**: coppia accessor + gemello sul modello, e getter `public` per ogni campo cablato a `FieldRefreshAction`. Diagnosi ripetibile con `php artisan xot:check-accessor-twins --orphans`. Vedi [gemelli orfani](../../../Modules/Ptv/docs/orphan-twin-methods.md) e [regola accessor+gemello](../../../../docs/wiki/rules/accessor-twin-method.md).
- **Impatto tema**: nessuno — il tema renderizza il valore che il modello espone. Un campo vuoto qui non è mai un problema di vista: si verifica sul modello prima di toccare Blade o CSS.
