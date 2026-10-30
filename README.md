# NautiMag 
<img src="Screen/logo.png" height="80"/> 

**Gestione Magazzino Multi-Piattaforma per Piccole e Medie Attività**

<sub>NautiMag v1.3 · Made with ❤️ in Italia</sub>

[![Release](https://img.shields.io/badge/Release-v1.3-blue)](https://github.com/maxsassano/nautimag/releases)
[![Platform](https://img.shields.io/badge/Platform-Windows%2010%2F11%20%7C%20Android-informational)](https://github.com/maxsassano/nautimag)
[![.NET](https://img.shields.io/badge/.NET-11-purple)](https://dotnet.microsoft.com/)
[![License](https://img.shields.io/badge/License-Proprietary-red)](LICENSE)

> **NautiMag** è un gestionale di magazzino completo per negozi di casalinghi, giocattoli, ferramenta, cartolerie e piccole attività commerciali.  
> Funziona su **Windows e Android**, in **standalone** (un solo PC) o in **modalità server** (più dispositivi in rete con carrello condiviso in tempo reale).

---

### 📸 Screenshot

| Home Windows | Home Android |
|:---:|:---:|
| <img src="Screen/home-win.png"/> | <img src="Screen/home-android.png"/> |

---

### 📖 [Leggi la Guida Utente Online](https://maxsassano.github.io/NautiMag)

---

## 📑 Indice

- [📥 Download](#-download)
- [🏗️ Architettura del Sistema](#️-architettura-del-sistema)
- [✨ Funzionalità Dettagliate](#-funzionalità-dettagliate)
  - [🏠 Home e Interfaccia](#-home-e-interfaccia)
  - [⚙️ Anagrafiche](#️-anagrafiche)
  - [📦 Magazzino e Articoli](#-magazzino-e-articoli)
  - [🛒 Vendita e Cassa](#-vendita-e-cassa)
  - [📄 Documenti Fiscali e Commerciali](#-documenti-fiscali-e-commerciali)
  - [💵 Prima Nota Cassa](#-prima-nota-cassa)
  - [🎁 Tessera Fedeltà](#-tessera-fedeltà)
  - [🖨 Stampe, Etichette e Report](#-stampe-etichette-e-report)
  - [📊 Statistiche e Analisi](#-statistiche-e-analisi)
  - [📥 Import / 📤 Export](#-import--export)
  - [🗄 Backup, Recovery e Sync](#-backup-recovery-e-sync)
  - [🔧 Sistema, Utenti e Log](#-sistema-utenti-e-log)
  - [🎨 Temi e Personalizzazione](#-temi-e-personalizzazione)
- [🛠️ Novità e Stabilità (v1.3)](#️-novità-e-stabilità-v13)
- [🧬 Stack Tecnico](#-stack-tecnico)
- [🗂️ Struttura dei Progetti](#️-struttura-dei-progetti)
- [🌐 Modalità di Rete](#-modalità-di-rete)
- [🛡️ Sicurezza e Licenza](#️-sicurezza-e-licenza)
- [🚀 Installazione](#-installazione)
- [🔄 Aggiornamento da Versioni Precedenti](#-aggiornamento-da-versioni-precedenti)
- [📄 Licenza](#-licenza)
- [🆘 Supporto](#-supporto)
- [☕ Sostieni il progetto](#-sostieni-il-progetto)

---

## 📥 Download

Scarica l'ultima versione dalla pagina [**Releases**](https://github.com/maxsassano/nautimag/releases).

| Requisito | Dettaglio |
|---|---|
| **Sistema Operativo** | Windows 10 / 11 (64-bit) o Android 7.0+ |
| **Runtime** | .NET 11 Desktop Runtime (Windows) |
| **WebView2** | Runtime Edge WebView2 (preinstallato su Windows 11) |
| **Spazio disco** | ~200 MB (inclusi DB, foto e backup) |
| **Privilegi** | Nessun admin richiesto (installazione per-utente) |
| **APK Android** | Disponibile su richiesta (contatta l'autore) |

---

## 🏗️ Architettura del Sistema

NautiMag è progettato per adattarsi a qualsiasi tipo di negozio, dal piccolo esercizio familiare al punto vendita con più casse.

- **Dual-Mode**:
  - **Standalone** — un solo PC, database locale SQLite. Zero configurazione di rete.
  - **Modalità Server** — un PC fa da "server" (con DB SQLite locale in `Documenti\NautiMag\data`), gli altri dispositivi (Windows o Android) si collegano via HTTP + SignalR.
- **Archivio Anagrafico Unico**: Clienti e Fornitori condividono i dati. Se un soggetto è entrambi, il record viene marcato `Tipo = 2` e non ci sono duplicazioni.
- **Maschere Dinamiche**: Persona Fisica → Nome/Cognome. Società → Ragione Sociale. P.A. → SDI a 6 caratteri.
- **Auto-Import Anagrafiche**: Inserendo la P.IVA/C.F. di un Cliente nella scheda Fornitore (o viceversa), il sistema propone di importare automaticamente i dati.
- **Real-Time**: Aggiornamento istantaneo dei carrelli via SignalR. Un carrello modificato su un tablet Android si vede immediatamente sul PC Cassa.
- **Auto-Discovery (UDP)**: I client trovano il server in automatico sulla rete locale. Se il PC cambia IP, il client si riconnette e si aggiorna da solo.
- **QR Code Setup**: Il PC genera un QR Code con URL + PIN + CartId. Il telefono lo inquadra e si configura in 2 secondi.
- **Offline Queue**: Se il server è offline, le scritture (articoli, movimenti) vanno in coda su file JSON locale e vengono sincronizzate al ritorno della connessione.
- **Strategy Pattern Local/Remote**: I servizi anagrafiche hanno doppia implementazione (SQLite locale o HTTP remoto), iniettata via DI all'avvio in base alla modalità.

---

## ✨ Funzionalità Dettagliate

### 🏠 Home e Interfaccia

- **Home a griglia**: 8 tile principali (Scansiona, Carrello, Documenti, Anagrafiche, Gestione, Sistema, Agenda, Guida).
- **TopBar universale**: freccia indietro, casetta Home, stato connessione server (pallino verde/giallo/rosso/grigio), ricerca globale, carrello con badge, notifiche, guida.
- **Badge DEMO**: se la licenza non è attiva, la Home mostra un chiaro badge rosso "DEMO" e i dati aziendali sono bloccati.
- **Alert sottoscorta**: in Home appare una fascia rossa con il numero di articoli sotto scorta minima.
- **Notifiche**: scontrini KO, articoli sottoscorta, licenza in scadenza, appuntamenti.
- **Assistenza Remota**: collegamento rapido a RustDesk/AnyDesk o esportazione di un file ZIP con i log di diagnostica (`app.log`, `crash.log`, config server/RT).
- **Chiusura Sicura**: cliccando la "X" su Windows, viene chiesta conferma. Se ci sono modifiche non salvate, avvisa prima di uscire.
- **Single Instance (Windows)**: un Mutex impedisce l'apertura di due istanze contemporaneamente.

### ⚙️ Anagrafiche

- **Clienti e Fornitori**: maschere intelligenti che si adattano al tipo di soggetto (Persona Fisica, Società, P.A.).
- **Controllo Duplicati On-Blur**: uscendo dal campo P.IVA/C.F., un popup mostra l'anteprima del contatto esistente (Nome, P.IVA, C.F., Tel, Email) con opzione "Apri scheda".
- **Validazione Fiscale**: P.IVA e C.F. validati con algoritmi matematici ufficiali (Luhn per P.IVA, checksum per C.F., inclusi CF omocodici).
- **Auto-Import**: se inserisci la P.IVA di un Cliente esistente nella scheda Fornitore (o viceversa), NautiMag propone di importare i dati.
- **Google Maps**: dalla scheda cliente/fornitore, click su 📍 apre Google Maps con l'indirizzo già cercato.
- **Rubrica unificata**: lista contatti unica per clienti + fornitori, con azioni rapide (chiama, mappa, WhatsApp, Facebook, Instagram, condividi contatto).
- **GDPR / Privacy**: gestione consenso con generazione del modulo PDF firmabile.
- **Azienda**: dati del titolare con Logo, Tipo Soggetto, P.IVA, Codice SDI, Regime Fiscale (18 codici ufficiali). P.IVA aziendale validata contro l'archivio unico.
- **Classificazioni**: Categorie, Unità di Misura, Ubicazioni, Aliquote IVA (con Natura per IVA 0%).

### 📦 Magazzino e Articoli

- **Scheda articolo completa**: Codice, Prodotto, Categoria, Fornitore, Prezzo vendita/acquisto, IVA, foto, scorta minima, ubicazione.
- **Specifiche prodotto**: Colore, Taglia/Formato, Materiale, Imballo, Dimensioni.
- **Azioni magazzino rapide**: menu ⋮ Altro con Carica 1, Acquisto, Carico, Scarico.
- **Merci in arrivo**: badge arancione "🚚 In Arrivo: N pz" nella scheda articolo e nella lista, calcolato dagli ordini in stato Bozza/Inviato.
- **Navigazione contestuale**: entrando in un articolo dalla ricerca, le frecce ◀ ▶ scorrono solo i risultati filtrati.
- **Tracciabilità Lotti (FIFO/FEFO)**: gestione completa dei lotti con numero, data di scadenza e scarico automatico. Pagina dedicata ai lotti attivi e monitoraggio dei lotti in scadenza (es. entro 30 giorni).
- **Distinta Base / Kit**: articoli composti da più articoli semplici (cesti regalo, set, bundle). Alla vendita del kit, il magazzino scarica automaticamente tutti i componenti. Supporto per kit multilivello (kit dentro kit).
- **Inventario Storico**: calcolo preciso della giacenza a una data passata, sottraendo i movimenti successivi.
- **Importazione Listini Metel**: parsing automatico di listini hardware (formati ANIE, delimitati, custom GEK) per aggiornare/creare articoli in blocco.
- **Ricerca con pistola barcode**: su Windows funziona in qualsiasi barra di ricerca. Su Android si attiva lo scanner con la fotocamera.

### 🛒 Vendita e Cassa

- **Carrello condiviso**: in modalità server, tutti i dispositivi con lo stesso CartId vedono lo stesso carrello in tempo reale.
- **Multi-Cart / Carrelli Nominati (Android)**: su tablet è possibile creare più carrelli contemporaneamente (uno per cliente), cambiarli, unirli alla cassa.
- **Unisci Carrello**: dal PC Cassa si può prelevare il carrello di un tablet in un click, con anteprima degli articoli prima di confermare.
- **Notifica carrelli in attesa**: banner verde "📢 Ci sono N carrelli in attesa: ..." quando ci sono clienti in fila.
- **Sconti per riga**: possibilità di applicare uno sconto percentuale (0-100%) su una singola riga del carrello.
- **Selezione cliente alla chiusura**: "Cliente generico" o uno dell'anagrafica.
- **Chiusura vendita**: controllo scorte, calcolo totale, registrazione movimento, scarico magazzino.
- **Stampa fiscale automatica**: se la RT è configurata, lo scontrino viene inviato in background alla stampante.
- **Scontrini KO**: se la stampante non risponde, lo scontrino va in una coda di errore gestibile dalla UI (Riprova, Segna come risolto, Annulla, Elimina).
- **Annullamento scontrino**: dal dettaglio vendita, reintegra il magazzino e marca la vendita come annullata (ricorda: annullare anche sul RT entro 15gg).
- **Punti fedeltà**: se abilitati, alla chiusura vendita i punti vengono sommati al cliente associato.
- **Stampa PDF post-vendita**: menu unico con "Stampa Ricevuta PDF" o "Stampa Fattura Proforma" (con numero progressivo modificabile).

### 📄 Documenti Fiscali e Commerciali

- **Fatture Emesse**: creazione con cliente, righe da magazzino o righe descrittive, multi-aliquota, prezzi ivati/netti.
  - **Emissione**: la fattura passa da Bozza a Emessa e scarica il magazzino.
  - **Esportazione XML**: genera file `Fattura_YYYY-NNNN.xml` conforme al tracciato FPR12, pronto per il caricamento manuale su SDI/commercialista.
  - **Note Credito**: si emettono dalla fattura emessa, con residui per riga (non puoi stornare più del fatturato).
- **Fatture in arrivo (Fornitori)**: caricamento merce da fattura fornitore tramite scanner barcode. Supporto lotti al carico.
- **Preventivi**: creazione, stampa PDF con watermark "NON FISCALE", conversione automatica in Fattura Emessa in stato Bozza.
- **Ordini Fornitori**: gestione stati progressivi (Bozza, Inviato, Ricevuto, Chiuso, Annullato). Alla ricezione genera movimenti di Acquisto.
- **DDT / Buoni Consegna**: documento di trasporto con stati (Bozza, Emesso, Consegnato, Annullato). Generazione Fattura Accompagnatoria da DDT.
- **Note Credito**: gestione completa con residui e stato (Bozza, Emessa, Annullata).
- **Scontrini / Scontrini KO**: registro scontrini con 3 tab (Da fare, Risolti, Annullati).

### 💵 Prima Nota Cassa

- **Entrate e uscite manuali**: bollette, prelievi, stipendi, incassi vari.
- **Categorie**: Incasso, Versamento, Altro (entrate) / Bolletta, Prelievo, Acquisto, Stipendio, Altro (uscite).
- **Saldo cassa**: differenza in tempo reale tra entrate e uscite.
- **Colori**: entrate verde, uscite rosso, saldo blu.

### 🎁 Tessera Fedeltà

- **Configurazione**: abilita la tessera e imposta Euro spesi per punto + valore in euro di 1 punto (es. 10€ = 1 punto, 1 punto = 0,10€).
- **Assegnazione automatica**: alla chiusura vendita con cliente associato, i punti vengono calcolati e sommati.
- **Riscatto punti**: dalla scheda cliente, pulsante 🎁 Riscatta con importo personalizzato.
- **Storico**: i punti attuali sono sempre visibili nella scheda cliente.

### 🖨 Stampe, Etichette e Report

- **Etichette barcode Code128**: formati A4 predefiniti (2, 10, 14, 21, 24, 40 etichette) e rotolo (40×25, 50×30, 60×40 mm). Formati custom creabili.
- **Report magazzino**: completo, solo sottoscorta, solo negativi.
- **Report movimenti**: con filtri per tipo/periodo, riepilogo IVA per aliquota.
- **Report vendite**: riepilogo vendite con totali, scontrino medio, riepilogo IVA.
- **Lista clienti / fornitori / articoli**: PDF pronti per la stampa con filtri (categoria, sottoscorta, negativi).
- **Agenda PDF**: mensile e annuale.
- **Apri file/cartella**: dopo ogni PDF, menu con "Apri file" o "Apri cartella".

### 📊 Statistiche e Analisi

- **KPI vendite**: oggi, 7 giorni, mese, anno. Numero scontrini.
- **Grafico ultimi 30 giorni**: barre verticali proporzionali al fatturato giornaliero.
- **Magazzino**: articoli totali, pezzi, valore (IVA incl.), negativi, sottoscorta.
- **Top 10 articoli** per pezzi venduti nell'anno.
- **Top 10 clienti** per totale speso nell'anno.

### 📥 Import / 📤 Export

- **Import Excel magazzino**: colonne standard (CODICE, PRODOTTO, CATEGORIA, PREZZO, QUANTITA, VENDUTO, FOTO) o guidato con mapping colonne.
- **Import Excel vendite**: storico vendite con creazione movimenti.
- **Import anagrafiche**: clienti e fornitori con mapping guidato.
- **Import listini Metel**: formati ANIE, delimitati, custom GEK.
- **Export Excel**: 5 fogli (Magazzino, Movimenti, Riepilogo IVA, Clienti, Fornitori) con calcolo IVA.
- **Auto-creazione anagrafiche**: durante l'import magazzino, categorie/unità mancanti vengono create automaticamente.
- **Backup automatico pre-import**: prima di ogni import viene creato un backup del DB.

### 🗄 Backup, Recovery e Sync

- **Auto-backup giornaliero**: il server crea un backup al primo avvio di ogni giorno.
- **Backup manuale**: dalla pagina Backup, con rotazione automatica (max 5 backup).
- **Ripristino backup**: dalla UI con doppia conferma. Viene creato un backup pre-restore.
- **NautiMag.Recovery** (utility WPF): GUI + CLI per ripristinare il DB quando il server non parte. Esegue anche `integrity_check`.
- **Sync `.wmsync`**: in modalità standalone, esporta un file con tutti i dati (articoli, movimenti, anagrafiche, aliquote, azienda, logo) e lo importa su un altro dispositivo. Regola conflitti: vince la modifica più recente (`AggiornatoIl`).

### 🔧 Sistema, Utenti e Log

- **Gestione Utenti**: creazione/modifica/eliminazione utenti con 3 livelli:
  - **SuperUser**: accesso totale, unico a vedere i Log.
  - **Admin**: può creare/modificare utenti Vendita. Può creare Admin ma non eliminarli.
  - **Vendita**: accesso limitato.
- **Auto-logout**: dopo 15 minuti di inattività.
- **Primo Avvio**: creazione utenti `superuser` e `admin` con `MustChangePassword = true`.
- **Log Audit (DB)**: chi ha fatto cosa (vendite, modifiche articoli, login, ecc.), visibile solo al SuperUser.
- **Log Sistema (File)**: `app.log` con rotazione 5 MB (max 5 file). Tab separato nella pagina Log.
- **Server Tray (WinForms)**: utility in system tray con 3 tab (Console Live, Log Sistema, Log Audit). Pulsante "Pulisci Log" unico.
- **Cambio Password**: forzato al primo login e modificabile dal proprio account.
- **Licenza**: pagina dedicata con stato (Trial, Attiva, Scaduta), attivazione via seriale, disattivazione.

### 🎨 Temi e Personalizzazione

- **3 Temi**: Standard (Blu), Pastello (Colori), Dark (Notturno).
- **Applicazione tema**: al riavvio dell'app (per evitare problemi di binding MAUI).
- **Impostazioni Server**: modalità (standalone/server), URL, Hostname, PIN, CartId.
- **Configurazione RT**: cartelle Input/Esito, nome file scontrino, timeout.

---

## 🛠️ Novità e Stabilità (v1.3)

La v1.3 introduce importanti novità per la gestione degli aggiornamenti e la stabilità della rete:

- **Auto-Update da GitHub**: l'app controlla in background la presenza di nuove release, mostra il changelog e permette il download diretto (installer `.exe` per Windows, `.apk` per Android).
- **Auto-Discovery UDP (Ping/Response)**: risolto il problema degli IP dinamici (DHCP). Ora il server risponde attivamente alle richieste dei client. Se il PC cambia IP, il client lo trova e si aggiorna a caldo senza riavvii.
- **Installer e Firewall**: l'installer ora sblocca automaticamente le porte TCP 5000 (Web) e UDP 5001 (Discovery) nel Firewall di Windows.
- **Aggiornamento dinamico del Client HTTP**: il `CartBridge` ora aggiorna i client HTTP e SignalR in tempo reale quando rileva un cambio di rete, senza richiedere il riavvio dell'app.
- **Precompilazione dati PA**: aggiunta la ricerca integrata per Codice Fiscale per recuperare automaticamente SDI e PEC (solo per la Pubblica Amministrazione).
- **Bug XamlRoot (Windows)**: risolto il crash critico dell'app che si verificava quando il server non era raggiungibile all'avvio.

---

## 🧬 Stack Tecnico

| Componente | Tecnologia |
|---|---|
| **Framework** | .NET 11 (Preview) + .NET MAUI |
| **UI** | XAML + MVVM (CommunityToolkit.Mvvm) |
| **Database** | SQLite (sqlite-net-pcl) |
| **Server** | ASP.NET Core Minimal API + SignalR |
| **PDF** | QuestPDF |
| **Excel** | ClosedXML + CsvHelper |
| **Barcode** | ZXing.Net |
| **Installer** | Inno Setup |
| **Tray Utility** | WinForms (`net11.0-windows`) |
| **Recovery Utility** | WPF (`net11.0-windows`) |

---

## 🌐 Modalità di Rete

### Scenario 1 — Standalone (un solo PC)

```
┌──────────────────────┐
│  NautiMag (Windows)  │
│   DB locale SQLite   │
│   Nessuna rete       │
└──────────────────────┘
```

- Zero configurazione.
- Tutto funziona in locale.
- Sync manuale via `.wmsync` per spostare dati su un altro dispositivo.

### Scenario 2 — Client/Server (più dispositivi)

```
┌──────────────────┐        ┌──────────────────┐
│  PC Cassa        │        │  Tablet Android  │
│  NautiMag        │◄──────►│  NautiMag        │
│  Server + DB     │ SignalR│  Client          │
└──────────────────┘        └──────────────────┘
        ▲                            ▲
        │                            │
        └────────── HTTP ────────────┘

Server Tray (WinForms) → controlla il server HTTP
```

- Il PC Server ha il DB (`Documenti\NautiMag\data\nautimag.db`).
- I client si connettono via URL (`http://192.168.1.10:5000`) + PIN + CartId.
- Il carrello è condiviso in tempo reale (SignalR).
- Auto-discovery UDP: il client invia un ping, il server risponde con il suo IP aggiornato.

### Connessione Client

1. **Ricerca automatica** (UDP): pulsante "Cerca Server in automatico".
2. **QR Code**: il PC genera un QR, il telefono lo inquadra.
3. **Manuale**: IP o Hostname + PIN.

---

## 🛡️ Sicurezza e Licenza

- **Licenza Offuscata**: AES encryption per il file `license.json`.
- **Anti-Manomissione**: file nascosto in `%LocalAppData%\NautiMag\.sys_cache` per rilevare reset del trial.
- **Blocco Orologio**: se l'orologio viene spostato indietro, il trial viene bloccato.
- **PIN Hashing**: il PIN del server non viaggia in chiaro. Viene hashato con SHA256 + salt.
- **Rate Limiting**: max 5 tentativi di login al minuto.
- **CORS locale**: solo origini della rete locale (localhost, 192.168.x.x, 10.x.x.x, 172.x.x.x).
- **Restrizioni Trial**: blocco di stampe, import/export, creazione documenti e limite di 5 inserimenti per Clienti/Fornitori.
- **Single Instance (Windows)**: Mutex per impedire doppie aperture.

---

## 🚀 Installazione

1. Scarica ed esegui `NautiMag_Setup.exe`.
2. Scegli il ruolo:
   - **Server** — installa app + server + tray + recovery + DB locale.
   - **Client** — installa solo l'app (si connette via rete al server).
3. Se Client, inserisci IP del server e PIN (oppure usa "Cerca Server in automatico").
4. Al primo avvio, configura l'azienda da **🏢 Anagrafiche → Azienda**.
5. (Opzionale) Configura la stampante fiscale RT da **Gestione → Impostazioni Server → Stampante Fiscale**.

> ⚠️ **Non usare cartelle cloud** (OneDrive, Dropbox) per il database. Il DB deve risiedere in `Documenti\NautiMag\data`.

---

## 🔄 Aggiornamento da Versioni Precedenti

Passando da **v1.2 → v1.3**:

- La migrazione del DB è **automatica**.
- Prima della migrazione viene creato un **backup automatico**.
- La migrazione è **irreversibile**: se torni alla v1.2 dopo aver aggiornato, il DB non sarà leggibile.
- In caso di problemi, usa **`NautiMag.Recovery`** per ripristinare il backup pre-migrazione.

---

## 📄 Licenza

**Software proprietario** — © 2026 Massimo Sassano. Tutti i diritti riservati.

---

## 🆘 Supporto

Per **bug** o **suggerimenti**:
👉 Apri una [**Issue su GitHub**](https://github.com/maxsassano/nautimag/issues)
📧 [massimo.sassano@gmail.com](mailto:massimo.sassano@gmail.com)

Per problemi tecnici, apri **Home → Sistema → 🆘 Assistenza Remota** ed esporta il file ZIP di diagnostica. Inviandocelo, potremo capire subito cosa non va.

---

## ☕ Sostieni il progetto
[![PayPal](https://img.shields.io/badge/PayPal-Offrimi%20un%20caffè-0070BA?logo=paypal)](https://paypal.me/veruscatanese)
