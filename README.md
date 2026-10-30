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
- [🌐 Modalità di Rete](#-modalità-di-rete)
- [🛡️ Sicurezza e Licenza](#️-sicurezza-e-licenza)
- [🚀 Installazione](#-installazione)
- [🔄 Aggiornamento da Versioni Precedenti](#-aggiornamento-da-versioni-precedenti)
- [📄 Licenza](#-licenza)
- [🆘 Supporto](#-supporto)

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

---

## 🏗️ Architettura del Sistema

NautiMag è progettato per adattarsi a qualsiasi tipo di negozio, dal piccolo esercizio familiare al punto vendita con più casse.

- **Dual-Mode**: Standalone (SQLite locale) o Modalità Server (HTTP + SignalR).
- **Archivio Anagrafico Unico**: Clienti e Fornitori condividono i dati senza duplicazioni (Tipo = 2).
- **Auto-Discovery (UDP)**: I client trovano il server in automatico sulla rete locale. Se il PC cambia IP, il client si riconnette e si aggiorna da solo in tempo reale.
- **Auto-Update**: L'app controlla in background la presenza di nuove release su GitHub, mostra il changelog e permette il download diretto.
- **Offline Queue**: Se il server è offline, le scritture vanno in coda locale e si sincronizzano al ritorno della connessione.

---

## ✨ Funzionalità Dettagliate

### 🏠 Home e Interfaccia
- **Home a griglia**: 8 tile principali, layout ottimizzato senza scroll verticale.
- **TopBar universale**: stato connessione, ricerca globale, carrello, notifiche, guida.
- **Badge DEMO**: visibile se la licenza non è attiva.
- **Alert sottoscorta**: fascia rossa con il numero di articoli sotto scorta.

### ⚙️ Anagrafiche
- **Maschere intelligenti**: Persona Fisica, Società, P.A.
- **Validazione Fiscale**: P.IVA e C.F. validati con algoritmi matematici all'uscita del campo.
- **Auto-compilazione Città**: Inserendo il CAP, l'app compila in automatico Città e Provincia.
- **WhatsApp Auto-copy**: Se lasciato vuoto, copia il numero di telefono.

### 📄 Documenti Fiscali e Commerciali
- **Fatture Emesse**: Multi-aliquota, righe descrittive, Note Credito, Esportazione XML per SDI.
- **Fatture in arrivo**: Caricamento merce tramite barcode.
- **Preventivi**: Conversione automatica in Fattura Emessa, DDT o Ordine.
- **DDT**: Generazione Fattura Accompagnatoria (con creazione del documento fiscale).

### 🔧 Sistema, Utenti e Log
- **3 Ruoli**: SuperUser, Admin, Vendita.
- **Log Audit (DB)** e **Log Sistema (File)**.
- **Licenza**: Annuale (`A-`) o a Vita (`L-`).

---

## 🛠️ Novità e Stabilità (v1.3)

- **Auto-Update**: Controllo e download nuove release da GitHub.
- **Auto-Discovery UDP**: Server in ascolto, client che pinga e aggiorna l'IP a caldo.
- **Installer**: Sblocco automatico delle porte Firewall TCP 5000 e UDP 5001.
- **Validazione P.IVA e C.F.**: Controllo matematico all'uscita del campo.
- **Comuni Italiani**: Auto-compilazione Città/Provincia dal CAP.
- **Note Credito**: Flusso di emissione immediata post-creazione.
- **DDT -> Fattura**: Ora crea il documento fiscale vero e proprio.
- **Archivi Zoppi**: Blocco eliminazione Clienti/Fornitori/Articoli con movimenti.
- **UI/UX**: Home senza scroll, Sistema e Documenti con layout affiancato.

---

## 🧬 Stack Tecnico

- **.NET 11** (Preview) + **.NET MAUI**
- **ASP.NET Core Minimal API** + **SignalR**
- **SQLite** (sqlite-net-pcl) + **QuestPDF** + **ClosedXML** + **ZXing.Net**
- **Inno Setup** (Windows Installer)

---

## 🛡️ Sicurezza e Licenza

- **Licenza Offuscata**: AES encryption.
- **Anti-Manomissione**: Rilevamento reset trial e blocco orologio.
- **PIN Hashing**: SHA256 + salt.
- **Single Instance** su Windows (Mutex).

---

## 🚀 Installazione

1. Scarica ed esegui `NautiMag_Setup.exe`.
2. Scegli il ruolo: **Server** o **Client**.
3. Configura l'azienda al primo avvio.

> ⚠️ **Non usare cartelle cloud** (OneDrive, Dropbox) per il database. Il DB deve risiedere in `Documenti\NautiMag\data`.

---

## 🔄 Aggiornamento da Versioni Precedenti

Passando da **v1.2 → v1.3**:
- La migrazione del DB è **automatica**.
- Viene creato un **backup automatico** prima della migrazione.

---

## 📄 Licenza

**Software proprietario** — © 2026 Massimo Sassano. Tutti i diritti riservati.

---

## 🆘 Supporto

👉 [**Issue su GitHub**](https://github.com/maxsassano/nautimag/issues)
📧 [massimo.sassano@gmail.com](mailto:massimo.sassano@gmail.com)
