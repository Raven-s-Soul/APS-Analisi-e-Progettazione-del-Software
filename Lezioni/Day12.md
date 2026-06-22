# 12 - Contratti delle operazioni di sistema & Dai requisiti alla progettazione, iterativamente & Architettura logica & Verso la progettazione a oggetti - 30/03/2026

> **Nota del corso:** Gli argomenti d'esame per la prima prova intermedia si concludono con i contratti di sistema.

> Nello sviluppo di applicazioni in architettura **Client-Server**, la strategia migliore consiste nell'analizzare il dominio adottando la prospettiva di uno specifico punto di accesso fisico o virtuale del sistema (ad esempio, focalizzandosi sulla cassa di un negozio).

> **Regola pratica:** Per il primissimo caso d'uso identificato nel sistema, la pre-condizione è tipicamente assente ("Nessuna").

> Ragionare sulla struttura dei contratti è un esercizio mentale sempre raccomandato per l'analista, anche nei casi in cui non sussista l'obbligo di formalizzarli per iscritto.

---

## Dai Requisiti alla Progettazione

Il passaggio dall'analisi dei requisiti alla progettazione (Design) avviene secondo un approccio strettamente iterativo, traducendo i concetti astratti del dominio in elementi software concreti.

> [!NOTE]
> ### I Principi Fondamentali della Progettazione Software
> 
> * **Tracciabilità:** Il progetto deve essere costantemente riconducibile al modello di analisi iniziale.
 * **Consapevolezza Architetturale:** Bisogna considerare fin da subito l'architettura complessiva del sistema da realizzare.
 * **Equilibrio:** La progettazione dei dati ha la medesima rilevanza della progettazione delle operazioni.
 * **Cura delle Interfacce:** Le interfacce (sia quelle esterne sia quelle di comunicazione tra i componenti interni) vanno modellate con estrema precisione.
 * **Centralità dell'Utente:** Il design dell'interfaccia utente (UI) deve adattarsi strettamente alle reali necessità operative dell'utente.
 * **Indipendenza Funzionale (Coesione):** I componenti sviluppati a livello di dettaglio devono essere fortemente coesi.
 * **Disaccoppiamento (Low Coupling):** I componenti devono essere debolmente accoppiati sia tra loro sia con l'ambiente circostante.
 * **Comprensibilità:** I modelli grafici del progetto devono risultare immediati e facilmente interpretabili dal team.
 * **Iterazione:** Il design non è definitivo, ma deve evolvere attraverso cicli incrementali.
 * **Semplicità (KISS):** Il progettista deve perseguire attivamente la massima semplicità logica, evitando sovrastrutture inutili.

---

## Architettura Logica

L'architettura logica organizza i macro-elementi strutturali del sistema. In questo corso viene adottata un'**architettura a strati (Layered Architecture)**, strutturata tipicamente in tre livelli:
1. **Strato dell'Interfaccia Grafica (Presentation)**
2. **Strato Logico di Business (Domain o Logica Applicativa)**
3. **Strato dei Servizi Tecnici (Infrastructure, es. persistenza su Database)**

> [!IMPORTANT]
> **Regola di Dipendenza degli Strati:** Il flusso delle dipendenze è strettamente unidirezionale. Gli strati superiori dipendono direttamente dalle funzionalità fornite dagli strati inferiori, ma gli strati inferiori non devono mai dipendere da quelli superiori.
> 
> *In UML, gli strati vengono rappresentati graficamente tramite i **Package** (simili a cartelle) e le relazioni sono espresse da frecce tratteggiate che indicano le dipendenze logiche (note anche come dipendenze di compilazione).*

### I Due Pilastri Architetturali
* **Separazione degli Interessi (Separation of Concerns):** Responsabilità concettualmente distinte ed esigenze differenti devono essere isolate in porzioni di codice separate.
* **Modularità:** Il codice sorgente deve essere organizzato in moduli indipendenti, caratterizzati da un'alta coesione interna e da un debole accoppiamento esterno.

> [!WARNING]
> La ricerca esasperata di un "basso salto rappresentazionale" tra l'analisi e il codice non è una priorità assoluta in questa fase e rischia di indurre a scelte di progettazione errate.

### Layered Architecture orientata al Domain-Driven Design (DDD)
Una segmentazione standard più dettagliata prevede quattro livelli logici:
* **User Interface:** Gestione dei componenti grafici e dell'interazione utente.
* **Application:** Coordinamento delle attività e gestione dei dati prettamente transienti *(nota: in molti sistemi è implementata attraverso una sola classe controller)*.
* **Domain:** Il cuore del sistema, deputato alla gestione dei dati persistenti e delle regole di business.
* **Infrastructure:** Servizi tecnologici di basso livello e persistenza fisica.

### Principio di Separazione Modello-Vista (Model-View Separation)
Derivato dal principio di separazione degli interessi, stabilisce che:
* Gli oggetti grafici della UI (la Vista) non devono mai essere accoppiati direttamente in modo forte agli oggetti software non-UI (il Modello). È ammesso esclusivamente un accoppiamento indiretto.
* È tassativamente vietato inserire logica applicativa o regole di business all'interno degli oggetti deputati alla UI.

> [!NOTE]
> Le operazioni di sistema formalizzate durante la fase di analisi non sono altro che le funzioni concrete che verranno invocate dall'utente interagendo con la UI. Di conseguenza, un diagramma SSD descrive l'interfaccia parziale esposta dallo strato di dominio.

---

## Verso la Progettazione a Oggetti

La progettazione orientata agli oggetti (OOD) definisce la struttura logica del software che verrà poi implementata fattivamente tramite i linguaggi di programmazione (OOP).

### Approcci Operativi alla Progettazione
Esistono tre filosofie per affrontare il design del software:
1. **Esclusivamente durante la codifica:** Il design avviene direttamente scrivendo codice, affrontando i problemi a voce durante la programmazione.
2. **Disegno visuale preliminare seguito dalla codifica:** Si tracciano prima i diagrammi software e poi si passa all'implementazione *(approccio standard seguito in questo corso)*.
3. **Solo disegno:** Il team di progettisti si limita alla stesura dei modelli, demandando interamente la codifica a terzi.

> **Pianificazione temporale:** All'interno di un'iterazione di sviluppo tipica della durata di 3 settimane, la progettazione visiva iniziale occupa solitamente una finestra temporale ridotta (circa mezza giornata), per poi essere ripresa iterativamente attraverso brevi sessioni di disegno mirate.

### Modellazione Statica e Dinamica

| Tipo di Modellazione | Elementi Caratteristici | Livello di Importanza nel Progetto |
| :--- | :--- | :--- |
| **Modellazione Statica** | Mappa la struttura del codice: Classi, Associazioni, Attributi e segnature delle Operazioni. | Strutturale (Definisce lo scheletro). |
| **Modellazione Dinamica** | Mappa il comportamento a runtime: interazioni tra le istanze degli oggetti e flusso dei messaggi. | **Cruciale e prioritario** (Rappresenta il comportamento reale del software). |
