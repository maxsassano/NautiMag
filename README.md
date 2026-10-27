# NautiMag 
<img src="Screen/logo.png" height="80"/> 

**Gestione Magazzino Multi-Piattaforma per Piccole e Medie Attività**

<sub>NautiMag v1.1 · Made with ❤️ in Italia</sub>

[![Release](https://img.shields.io/badge/Release-v1.1-blue)](https://github.com/maxsassano/nautimag/releases)
[![Platform](https://img.shields.io/badge/Platform-Windows%2010%2F11%20%7C%20Android-informational)](https://github.com/maxsassano/nautimag)
[![.NET](https://img.shields.io/badge/.NET-11-purple)](https://dotnet.microsoft.com/)
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
| **Runtime** | .NET 11 Desktop Runtime (Windows) |
| **WebView2** | Runtime Edge WebView2 (preinstallato su Windows 11) |
| **Spazio disco** | ~200 MB (inclusi DB, foto e backup) |
| **Privilegi** | Nessun admin richiesto (installazione per-utente) |
| **APK Android** | Disponibile su richiesta (contatta l'autore) |

---

## 🏗️ Architettura del Sistema

NautiMag è progettato per adattarsi a qualsiasi tipo di negozio:
- **Dual-Mode**: Funziona in **Standalone** (DB locale) o in **Modalità Server** (multi-dispositivo real-time).
- **Archivio Anagrafico Unico**: Clienti e Fornitori condividono i dati. Se un soggetto è entrambi, non ci sono duplicazioni.
- **Persona Fisica e Società**: Maschere di input dinamiche (Nome/Cognome per privati, Ragione Sociale per aziende).
- **Auto-Import**: Inserendo la P.IVA di un Cliente nella scheda Fornitore (o viceversa), il sistema propone di importare automaticamente i dati.
- **Real-Time**: Aggiornamento istantaneo dei carrelli via SignalR.
- **Auto-Discovery (UDP)**: I client trovano il server in automatico sulla rete locale.

---

## ✨ Funzionalità Dettagliate

### 🏠 Home e Interfaccia
- **Badge DEMO**: Se la licenza non è attiva, la Home mostra un chiaro badge rosso "DEMO".
- **Assistenza Remota**: Collegamento rapido a RustDesk/AnyDesk o esportazione di un file ZIP con i log di diagnostica per l'assistenza.
- **Chiusura Sicura**: Cliccando la "X" per chiudere l'app, viene chiesta conferma per evitare chiusure accidentali.

### ⚙️ Gestione e Anagrafiche
- **Clienti e Fornitori**: Maschere intelligenti che si adattano al tipo di soggetto (Privato o Azienda). Validazione fiscale rigorosa con controllo duplicati "on-blur" e anteprima dei dati. Include l'apertura rapida di Google Maps per l'indirizzo.
- **Tessera Fedeltà**: Assegnazione punti, storico punti e riscatto premi integrato nella scheda cliente.
- **Prima Nota Cassa**: Gestione autonoma delle entrate e uscite manuali (bollette, prelievi, stipendi, ecc.) per il controllo del saldo di cassa.
- **Azienda**: I dati aziendali sono bloccati in modalità Demo e la P.IVA viene validata contro l'anagrafica unica.
- **Privacy (GDPR)**: Gestione del consenso con generazione del modulo cartaceo.

### 📄 Documenti
- **Preventivi**: Creazione, stampa PDF dedicata e conversione automatica in Fattura Emessa (in stato Bozza).
- **Fatture Emesse**: Supporto multi-aliquota e inserimento di **Righe Descrittive** per prestazioni e servizi.
- **Fatture in arrivo**: Carico merce da fattura fornitore tramite scansione barcode.
- **Note Credito / DDT / Ordini**: Gestione completa con residui e stati.

### 📦 Magazzino e Stampe
- **Importazione Listini Metel**: Parsing automatico di listini hardware (formati ANIE, delimitati e custom GEK) per aggiornare o creare articoli in blocco.
- **Inventario a data**: Calcolo della giacenza storica del magazzino ad una data specifica.
- **Merci in arrivo**: Visualizzazione degli articoli in arrivo dagli ordini fornitori in sospeso.
- **Paginazione Movimenti**: Storici enormi non bloccano più l'app (caricamento a blocchi di 50).
- **Apri File / Cartella**: Dopo aver generato un PDF, puoi aprirlo al volo o aprire la cartella di salvataggio in un click.
- **Report PDF ed Etichette**: Generazione documenti pronti per la stampa.

---

## 🛡️ Sicurezza e Licenza

- **Licenza Offuscata**: AES encryption per il file `license.json`.
- **Restrizioni Trial**: Blocco di stampe, import/export, creazione documenti e limite di 5 inserimenti per Clienti/Fornitori.

---

## 🚀 Installazione

1. Scarica ed esegui `NautiMag_Setup.exe`.
2. Scegli il ruolo: **Server** o **Client**.
3. Al primo avvio, configura l'azienda da **🏢 Anagrafiche → Azienda**.

---

## 📄 Licenza

**Software proprietario** — © 2026 Massimo Sassano. Tutti i diritti riservati.

---

## 🆘 Supporto

Per **bug** o **suggerimenti**:
👉 Apri una [**Issue su GitHub**](https://github.com/maxsassano/nautimag/issues)
📧 [massimo.sassano@gmail.com](mailto:massimo.sassano@gmail.com)

---

## ☕ Sostieni il progetto
[![PayPal](https://img.shields.io/badge/PayPal-Offrimi%20un%20caffè-0070BA?logo=paypal)](https://paypal.me/veruscatanese)
