# NautiMag 
<img src="Screen/logo.png" height="80"/> 

**Gestione Magazzino Multi-Piattaforma per Piccole e Medie Attività**

<sub>NautiMag v1.1 · Made with ❤️ in Italia</sub>

[![Release](https://img.shields.io/badge/Release-v1.1-blue)](https://github.com/maxsassano/nautimag/releases)
[![Platform](https://img.shields.io/badge/Platform-Windows%2010%2F11%20%7C%20Android-informational)](https://github.com/maxsassano/nautimag)
[![.NET](https://img.shields.io/badge/.NET-10-purple)](https://dotnet.microsoft.com/)
[![License](https://img.shields.io/badge/License-Proprietary-red)](LICENSE)

---

### 📸 Screenshot

| Home Windows | Home Android|
|:---:|:---:|
| <img src="Screen/home-win.png"/> | <img src="Screen/home-android.png"/> |

---

### 📖 [Leggi la Guida Utente Online](https://maxsassano.github.io/NautiMag)

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
- **Archivio Anagrafico Unico**: I dati di Clienti e Fornitori sono condivisi in un'unica entità. Se un'azienda è sia cliente che fornitore, non ci sono duplicazioni.
- **Real-Time**: Grazie a **SignalR**, ogni modifica al carrello o alle anagrafiche viene istantaneamente propagata a tutti i dispositivi connessi.
- **Auto-Discovery (UDP)**: I client (tablet/PC) trovano il server automaticamente sulla rete locale, senza dover inserire IP statici.
- **Configurazione QR Code**: Il PC Server genera un QR Code; il telefono lo inquadra e si configura da solo in 2 secondi (Zero-Touch Setup).
- **Sicurezza PIN**: Il PIN viaggia in modo sicuro sulla rete locale (hash SHA256) e non è mai leggibile in chiaro dai file di configurazione del server.
- **Performance**: I servizi anagrafici usano il pattern Strategy per astrarre il DB locale dal server remoto. Le liste usano la paginazione (a blocchi di 50) e i Lookup (categorie, fornitori) sono mantenuti in cache per 5 minuti.

---

## 📱 Configurazione Multi-Cassa

NautiMag eccelle nella gestione di più operatori contemporanei. Ogni dispositivo ha il suo carrello "base" configurato tramite **CartId** (es. `cassa`, `android1`). Sul tablet, il commesso può creare **Carrelli Nominati** (es. "Pippo", "Mario Rossi") e parcheggiarli. Il cassiere sul PC li vedrà in attesa e potrà unirli al carrello principale con il tasto **"🔗 Unisci"** (con anteprima articoli).

---

## ✨ Funzionalità Dettagliate (Le Card dell'App)

### 🏠 Home (Griglia Principale)
Tutte le funzioni a portata di tap, con card colorate e responsive:
- **📷 Scansiona**: Fotocamera per barcode (Android) o pistola USB (Windows).
- **🛒 Carrello**: Carrello vendita con gestione multi-cassa e carrelli nominati.
- **📄 Documenti**: Fatture, DDT, Ordini, Note Credito, Scontrini.
- **🏢 Anagrafiche**: Rubrica, Articoli, Azienda, Categorie, IVA.
- **📊 Gestione**: Statistiche, Etichette, Report, Import/Export, Backup.
- **🔧 Sistema**: Impostazioni, Server, Licenza, Utenti, Log.
- **📅 Agenda**: Appuntamenti e scadenze.
- **📖 Guida**: Manuale integrato.
- *Cliccando sulla card in alto (Logo/Nome Azienda) si apre direttamente l'anagrafica aziendale.*

### ⚙️ Gestione (Anagrafiche e Sistema)

**🏢 Anagrafiche e Archivio Unico**
- **Rubrica Unificata**: Una pagina che raccoglie tutti i contatti (Clienti, Fornitori o Entrambi).
- **Validazioni Fiscali**: Controllo matematico di P.IVA e Codice Fiscale. Controllo duplicati intelligente (on-blur) con anteprima dei dati.
- **Tipo Soggetto**: Selezione tra Società di capitali, Persona Fisica, P.A.
- **Privacy (GDPR)**: Gestione del consenso con generazione del modulo cartaceo.
- **Articoli**: Scheda anagrafica pura. Il Codice è bloccato dopo la creazione.

**📄 Documenti**
- **Fatture Emesse**: Creazione di fatture ed esportazione XML SDI.
- **Fatture in arrivo**: Carico merce da fattura fornitore tramite scansione barcode.
- **Note Credito**: Emissione esclusivamente da Fatture Emesse con calcolo del residuo.
- **Ordini Fornitori / DDT**: Gestione documenti di trasporto e ordini.
- **Scontrini KO**: Coda di gestione e ristampa per scontrini non stampati dalla RT.

**📦 Magazzino**
- **Statistiche**: KPI di vendita, grafici, top 10 articoli e clienti.
- **Sottoscorta / Negativi**: Controllo degli articoli in esaurimento o venduti in eccesso.
- **Etichette Barcode**: Generazione PDF di etichette Code128.

**🔧 Sistema**
- **Guida Utente / Impostazioni Server / Gestione Utenti**.
- **Log**: Due tab separati per Audit e Sistema, con pulsante integrato per svuotare i registri.
- **Temi Grafici**: Cambio istantaneo tra **Standard**, **Pastello** e **Dark**.

### 💾 Dati e Report
- **Import Excel**: 4 modalità (Magazzino, Vendite, Clienti, Fornitori).
- **Export Excel / Report PDF**: Esportazione completa e report pronti per la stampa.
- **Backup e Sincronizzazione**: Backup automatici e file `.wmsync` per allineare i dati offline.

---

## 🛡️ Sicurezza e Licenza

NautiMag è progettato per proteggere il lavoro dell'imprenditore:
- **Licenza Offuscata**: Il file `license.json` è crittografato con **AES**.
- **Anti-Manomissione e Anti-Spostamento Orologio**: Blocco del trial se si tenta di resettare la data.
- **Restrizioni Trial**: Se il periodo di prova è scaduto, l'app blocca stampe, import/export, la creazione di nuovi documenti e limita a 5 inserimenti totali per Clienti e Fornitori.
- **Single Instance**: Un `Mutex` impedisce l'apertura di più finestre di NautiMag.
- **Tracciamento Completo**: Tutte le azioni loggate nel DB e su file.

---

## 🚀 Installazione

*(Vedi la sezione Download per i requisiti)*
1. Scarica ed esegui `NautiMag_Setup.exe`.
2. Scegli il ruolo: **Server** o **Client**.
3. Al primo avvio, configura l'azienda da **🏢 Anagrafiche → Azienda**.

---

## 📄 Licenza

**Software proprietario** — © 2026 Massimo Sassano. Tutti i diritti riservati.

> ⚠️ **Il codice sorgente non è pubblico.** Su GitHub vengono pubblicate solo le release pronte all'uso.

---

## 🆘 Supporto

Per **bug**, **suggerimenti** o **richieste di funzionalità**:
👉 Apri una nuova [**Issue su GitHub**](https://github.com/maxsassano/nautimag/issues)

Per **assistenza commerciale** o **richiesta APK Android**:
📧 [massimo.sassano@gmail.com](mailto:massimo.sassano@gmail.com)

---

## ☕ Sostieni il progetto
[![PayPal](https://img.shields.io/badge/PayPal-Offrimi%20un%20caffè-0070BA?logo=paypal)](https://paypal.me/veruscatanese)
