# NautiMag 
<img src="Screen/logo.png" height="80"/> 

**Gestione Magazzino Multi-Piattaforma per Piccole e Medie Attività**

<sub>NautiMag v1.0 · Made with ❤️ in Italia</sub>

[![Release](https://img.shields.io/badge/Release-v1.0-blue)](https://github.com/maxsassano/nautimag/releases)
[![Platform](https://img.shields.io/badge/Platform-Windows%2010%2F11%20%7C%20Android-informational)](https://github.com/maxsassano/nautimag)
[![.NET](https://img.shields.io/badge/.NET-10-purple)](https://dotnet.microsoft.com/)
[![License](https://img.shields.io/badge/License-Proprietary-red)](LICENSE)

---

### 📸 Screenshot

| Home Windows | Home Android|
|:---:|:---:|
| <img src="Screen/home-win.png"/> | <img src="Screen/home-android.png"/> |

---

### 📖 [Leggi la Guida Utente Online](https://maxsassano.github.io/NautiMag/docs/)

---

## 📥 Download

Scarica l'ultima versione dalla pagina [**Releases**](https://github.com/maxsassano/nautimag/releases).

| Requisito | Dettaglio |
|---|---|
| **Sistema Operativo** | Windows 10 / 11 (64-bit) o Android 7.0+ |
| **Runtime** | .NET 10 Desktop Runtime (Windows) |
| **WebView2** | Runtime Edge WebView2 (preinstallato su Windows 11) |
| **Spazio disco** | ~200 MB (inclusi DB, foto e backup) |
| **Privilegi** | Nessun admin richiesto (installazione per-utente) |
| **APK Android** | Disponibile su richiesta (contatta l'autore) |

> ℹ️ L'installer verifica automaticamente i prerequisiti e ti guida al download se mancanti.
> 📱 L'APK per Android non è pubblicato direttamente per evitare utilizzi non autorizzati. Richiedilo via [email](mailto:massimo.sassano@gmail.com).

---

## 🏗️ Architettura del Sistema

NautiMag è progettato per adattarsi a qualsiasi tipo di negozio, sia esso un piccolo punto vendita o un'azienda con più casse e magazzinieri in mobilità.

- **Dual-Mode**: Funziona in **Standalone** (database locale sul singolo dispositivo) o in **Modalità Server** (multi-dispositivo in tempo reale).
- **Real-Time**: Grazie a **SignalR**, ogni modifica al carrello o alle anagrafiche viene istantaneamente propagata a tutti i dispositivi connessi.
- **Auto-Discovery (UDP)**: I client (tablet/PC) trovano il server automaticamente sulla rete locale, senza dover inserire IP statici.
- **Configurazione QR Code**: Il PC Server genera un QR Code; il telefono lo inquadra e si configura da solo in 2 secondi (Zero-Touch Setup).

---

## 📱 Configurazione Multi-Cassa (Il flusso di lavoro)

NautiMag eccelle nella gestione di più operatori contemporanei. Ecco come funziona nel dettaglio:

### 1. La Configurazione Base
Ogni dispositivo ha il suo carrello "base" configurato tramite **CartId** nelle Impostazioni Server:
- **PC Cassa (Windows)**: `cassa`
- **Tablet 1 (Android)**: `android1`
- **Tablet 2 (Android)**: `android2`

### 2. I Carrelli Nominati (La vera potenza)
Sul tablet, il commesso **non è limitato a un solo carrello**. Può creare più carrelli temporanei, ognuno con il nome del cliente. Ecco come:

1. Il commesso clicca su **➕ Nuovo Carrello** sul tablet.
2. Scrive il nome del cliente (es. **"Pippo"**).
3. Il sistema crea un carrello dedicato a Pippo (es. `pippo`). Il commesso aggiunge gli articoli di Pippo.
4. Arriva un altro cliente (es. **"Mario Rossi"**). Il commesso clicca di nuovo **➕ Nuovo Carrello** e scrive "Mario Rossi".
5. I due carrelli (`pippo` e `mario_rossi`) restano **parcheggiati** sul tablet, separati, senza che gli articoli si mischino.

### 3. L'Unione alla Cassa (Il momento magico)
Quando un cliente è pronto per pagare, il cassiere sul PC fa così:

1. Nel carrello del PC, vede un banner verde: **"📢 Ci sono 2 carrelli in attesa: pippo, mario_rossi"**.
2. Clicca sul pulsante **"🔗 Unisci"**.
3. Seleziona dalla lista il carrello del cliente pronto (es. `pippo`).
4. **L'Anteprima:** Prima di confermare, NautiMag mostra esattamente quali articoli e quante quantità ci sono dentro il carrello di Pippo. Nessuna sorpresa.
5. Il cassiere conferma: tutti gli articoli di `pippo` passano istantaneamente al carrello `cassa` del PC.
6. **Il tablet si svuota:** Il carrello `pippo` viene eliminato dal server. Il tablet (se era su `pippo`) torna automaticamente al suo carrello base `android1`, pronto per il prossimo cliente.

### 4. Il Vantaggio
Il commesso può servire **5-6 clienti in fila** con lo stesso tablet, senza dover tornare alla cassa a "scaricare" ogni volta. I carrelli restano separati finché non vengono chiamati dal cassiere. La cassa è il punto di raccolta, il tablet è il punto di raccolta ordini.

---

## ✨ Funzionalità Dettagliate (Le Card dell'App)

### 🏠 Home (Griglia Principale)
Tutte le funzioni a portata di tap, con card colorate e responsive:
- **📷 Scansiona**: Fotocamera per barcode (Android) o pistola USB (Windows).
- **📦 Articoli**: Lista completa con ricerca, filtri per categoria e rimanenze.
- **🛒 Carrello**: Carrello vendita con gestione multi-cassa e carrelli nominati.
- **💰 Vendite**: Storico vendite chiuse, filtri per data e cliente.
- **📊 Movimenti**: Registro immutabile di carichi, scarichi, acquisti e rettifiche.
- **💾 Dati**: Hub per Import, Export, Backup e Report PDF.
- **🔄 Sincronizza**: Trasferimento dati tra dispositivi offline.
- **⚙️ Gestione**: Accesso a tutte le configurazioni avanzate.

### ⚙️ Gestione (Anagrafiche e Sistema)
**📄 Documenti**
- **Ordini Fornitori**: Creazione, invio, ricezione (genera automaticamente i movimenti di Acquisto) e chiusura.
- **DDT / Buoni Consegna**: Documenti di trasporto per vendite, resi o ricezioni (non modificano il magazzino).
- **Note Credito**: Emissione da vendite esistenti con selezione delle righe da rendere.
- **Stampa Liste**: PDF di clienti, fornitori e articoli con filtri (sottoscorta, negativi).
- **Scontrini KO**: Coda di gestione per gli scontrini non stampati dalla RT (Da fare, Risolti, Annullati). Permette la ristampa.

**📦 Magazzino**
- **Statistiche**: KPI di vendita (oggi, mese, anno), grafici a barre, top 10 articoli e clienti.
- **Articoli Negativi**: Controllo immediato degli articoli venduti in eccesso.
- **Sottoscorta**: Avvisi per gli articoli sotto la scorta minima.
- **Etichette Barcode**: Generazione PDF di etichette Code128 (formati A4 e rotolo).

**🏢 Anagrafiche**
- **Azienda / Fornitori / Clienti**: Schede complete con storico e dati SDI.
- **Privacy (GDPR)**: Gestione del consenso con generazione del modulo cartaceo per la firma e tracciamento della data.
- **Categorie / Unità di Misura / Ubicazioni**: Gestione tassonomie merceologiche.
- **Aliquote IVA**: Personalizzabili (22%, 10%, 4%, 0%, custom).

**🔧 Sistema**
- **Guida Utente**: Manuale integrato con oltre 40 sezioni.
- **Impostazioni Server**: Configurazione modalità, IP/Hostname, PIN, CartId e Stampante Fiscale (RT).
- **Gestione Utenti**: Creazione e modifica utenti con ruoli **SuperUser**, **Admin** e **Vendita**.
- **Log**: Due tab separati per **Audit** (chi ha fatto cosa) e **Sistema** (errori tecnici).
- **Temi Grafici**: Cambio istantaneo tra **Standard (Blu)**, **Pastello (Colori)** e **Dark (Notturno)**.

### 💾 Dati e Report
- **Import Excel**: Tre modalità (Magazzino fisso, Guidato con mapping, Vendite). Creazione automatica di categorie e unità mancanti.
- **Export Excel**: File `.xlsx` con 3 fogli (Magazzino, Movimenti, Riepilogo IVA).
- **Report PDF**: Magazzino completo, Articoli in negativo, Sottoscorta, Movimenti, Vendite.
- **Backup**: Automatico giornaliero e manuale (rotazione max 5 file).

### 🖨️ Registratore Telematico (RT)
- **Integrazione Spooler**: Invio automatico degli scontrini alla stampante fiscale configurando le cartelle Input/Esito.
- **Gestione Errori**: Se lo scontrino non viene stampato (timeout o .ko), viene salvato in una coda di KO per la ristampa successiva.
- **Fatturazione SDI-ready**: I campi Codice SDI, PEC e Regime Fiscale (es. RF01, RF19) sono pronti nelle schede Cliente e Azienda per future esportazioni XML.

---

## 🛡️ Sicurezza e Licenza

NautiMag è progettato per proteggere il lavoro dell'imprenditore:

- **Licenza Offuscata**: Il file `license.json` è crittografato con **AES**. Non può essere letto o modificato con un editor di testo.
- **Anti-Manomissione**: Un file di sistema nascosto memorizza la vera data di installazione. Se l'utente cancella i file per resettare il trial, l'app se ne accorge e ripristina i dati originali.
- **Anti-Spostamento Orologio**: Se l'orologio del PC viene portato indietro nel tempo per aggirare la scadenza, il sistema blocca il trial.
- **Single Instance (Windows)**: Un `Mutex` impedisce l'apertura di più finestre di NautiMag, evitando conflitti sul database.
- **Tracciamento Completo**: Tutte le azioni (login, modifiche, vendite) sono loggate nel database (Audit) e su file (System).

---

## 🚀 Installazione

### Windows (Server o Client)
1. **Scarica** il file `NautiMag_Setup.exe` dalla pagina [**Releases**](https://github.com/maxsassano/nautimag/releases).
2. **Esegui** l'installer (nessun privilegio admin richiesto).
3. **Scegli il ruolo**:
   - **Server** — installa server, database locale, tray e app (PC principale).
   - **Client** — installa solo l'app, si collegherà al server via rete.
4. **Se Client**, inserisci l'IP o il nome del PC Server.
5. **Licenza**: Inserisci i dati della licenza (Email, P.IVA, Seriale) durante l'installazione, oppure inizia il trial di 30 giorni.
6. **Al primo avvio**:
   - Se Server: il database viene creato in `Documenti\NautiMag\data`.
   - Se Client: l'app si connette al server (verifica il pallino verde nella TopBar).
7. **Login** con le credenziali fornite dall'amministratore di sistema.
8. **Configura l'azienda** in **⚙️ Gestione → 🏢 Azienda**.

### Android (Client)
1. **Richiedi l'APK** via [email](mailto:massimo.sassano@gmail.com) (disponibile su richiesta).
2. **Installa l'APK** sul dispositivo (abilita "Origini sconosciute" se necessario).
3. **Al primo avvio**, configura la connessione al server:
   - **Metodo 1 (consigliato)**: premi **📡 Cerca Server in automatico** — l'app troverà il server da sola.
   - **Metodo 2**: inquadra il QR Code generato dal PC (Impostazioni Server → Genera QR Code).
   - **Metodo 3**: inserisci manualmente IP e PIN.
4. **Login** con le credenziali create sul server.

---

## 🔧 Requisiti Multiutente (Modalità Server)

Per uso con più postazioni sulla stessa rete:

- ✅ **PC Server** sempre acceso (o avvio automatico con Windows).
- ✅ **Stessa rete locale** (LAN/Wi-Fi) tra server e client.
- ✅ **PIN condiviso** (default `1234`).
- ✅ **CartId univoco** per ogni dispositivo (per carrelli separati).
- ✅ **Massimo 3-5 utenti** contemporanei (SQLite).
- ✅ **Firewall di Windows** configurato per la porta 5000 (l'installer lo fa automaticamente).
- ❌ **NON usare** cartelle sincronizzate cloud (OneDrive, Drive, Dropbox) per il database.

---

## 📄 Licenza

**Software proprietario** — © 2026 Massimo Sassano. Tutti i diritti riservati.

L'utilizzo è consentito esclusivamente ai soggetti in possesso di regolare licenza d'uso.
La redistribuzione, la decompilazione o la modifica non autorizzata sono vietate.

> ⚠️ **Il codice sorgente non è pubblico.** Su GitHub vengono pubblicate solo le release pronte all'uso (installer Windows e, su richiesta, APK Android).

---

## 🆘 Supporto

Per **bug**, **suggerimenti** o **richieste di funzionalità**:

👉 Apri una nuova [**Issue su GitHub**](https://github.com/maxsassano/nautimag/issues)

Per **assistenza commerciale** o **richiesta APK Android**:
📧 [massimo.sassano@gmail.com](mailto:massimo.sassano@gmail.com)

---

## ☕ Sostieni il progetto

Se l'app ti è utile, puoi offrirmi un caffè:

[![PayPal](https://img.shields.io/badge/PayPal-Offrimi%20un%20caffè-0070BA?logo=paypal)](https://paypal.me/veruscatanese)

Ogni contributo aiuta a mantenere il progetto attivo e senza pubblicità. Grazie! 🙏

---

<p align="center">
  <sub>NautiMag v1.0 · Made with ❤️ in Italia</sub>
</p>
