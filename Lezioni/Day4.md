# 4 - Casi d'uso & Altri requisiti & Storie utente & Iterazione 1: Concetti fondamentali - 09/03/2026

> **Nota della lezione:** Esempio iniziale omesso (skip fino a 48m).

> [!WARNING]
> **Gestione dei problemi aperti:** Quando l'analista riscontra dubbi o non comprende appieno le spiegazioni degli stakeholder durante i colloqui, deve evitare di forzare una comprensione immediata o mostrare incertezza bloccante. La strategia corretta consiste nel procedere temporaneamente, annotando accuratamente i punti oscuri per poi approfondirli e chiarirli in un secondo momento.

> [!CAUTION]
> **Inaffidabilità dei requisiti statici:** Qualsiasi requisito descritto per esteso sulla carta è intrinsecamente soggetto a errori a causa di molteplici fattori (incomprensioni, mutamento delle esigenze, ambiguità). Non bisogna mai fidarsi ciecamente della documentazione: l'unica vera convalida di un requisito avviene tramite la sua **implementazione pratica** seguita da un **feedback immediato** da parte dell'utente.

---

## Linee Guida per la Scrittura dei Casi d'Uso

I casi d'uso devono essere scritti in modo essenziale, prediligendo la forma attiva e focalizzando l'attenzione sull'azione diretta del sistema.
* **Corretto (Forma attiva):** *"Il sistema autentica l'Amministratore."*
* **Sconsigliato (Forma passiva):** *"L'Amministratore viene autenticato dal sistema."*

> [!NOTE]
> **Approccio a Scatola Nera (Black-Box):** I casi d'uso devono descrivere *cosa* il sistema fa dal punto di vista esterno, ignorando i dettagli implementativi interni.
> * **Sì:** *"Il sistema registra X."*
> * **No:** *"Il sistema memorizza X in una base di dati tramite un comando SQL..."*

### Livelli di granularità dei Casi d'Uso
* **Obiettivo Utente (User Goal):** Il livello standard, focalizzato sul valore concreto che l'attore principale vuole ottenere.
* **Sotto-funzione (Sub-function):** Livello di dettaglio inferiore, descrive passi operativi o sotto-attività tecniche necessarie a supportare un obiettivo utente.
* **Sommario (Summary):** Livello macroscopico ad alto livello, utile per raggruppare e dare una panoramica di più casi d'uso correlati.

---

## Altri Artefatti dei Requisiti

### Visione (Vision)
Documento sintetico che esplicita gli obiettivi strategici generali, i confini del sistema e le motivazioni di alto livello alla base del progetto.

---

## Le Storie Utente (User Stories)
Strumento alternativo o complementare ai casi d'uso tipico dei contesti agili. Ogni storia si sviluppa attraverso tre dimensi chiave:
1. **Descrizione:** Breve testo descrittivo che sintetizza il valore della funzionalità dal punto di vista dell'utente finale.
2. **Conversazione:** Lo scambio verbale continuo e il dibattito tra il team di sviluppo e gli stakeholder per definire i dettagli operativi.
3. **Test di Accettazione:** I criteri oggettivi e le condizioni di verifica che stabiliscono quando la storia può considerarsi effettivamente completata e funzionante.

> Analizzati a lezione i relativi esempi pratici per i due casi di studio del corso (POS e Monopoly).
