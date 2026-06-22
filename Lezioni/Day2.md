# 2 - Sviluppo iterativo ed evolutivo & Sviluppo agile - 03/03/2026

> [!NOTE]
> **Processo Software:** Rappresenta la cornice metodologica e strutturale adottata nell'ingegneria del software per guidare la produzione, l'evoluzione e la corretta manutenzione di un sistema informatico.

> [!TIP]
> Per comprendere l'efficacia di un qualsiasi processo software, occorre analizzare come mappa quattro vettori fondamentali:
> - **Chi:** I ruoli e le responsabilità delle figure coinvolte.
> - **Che cosa:** Le attività da svolgere e gli artefatti da produrre.
> - **Quando:** L'organizzazione e la sequenza temporale delle varie fasi.
> - **Come:** Le metodologie e le tecniche ingegneristiche applicate per raggiungere l'obiettivo.
> 
> *Esempi principali:* Modello a cascata, Unified Process (UP), Scrum, Extreme Programming (XP).

---

## Macro-Attività Ingegneristiche
Indipendentemente dallo specifico modello di ciclo di vita adottato, lo sviluppo di un sistema si articola sempre su alcune macro-attività standard:

* **Ingegneria dei Requisiti (Specifica):** Individuazione, analisi e formalizzazione delle funzionalità attese dal sistema.
* **Analisi:** Comprensione e modellazione concettuale del dominio del problema.
* **Progettazione (Design):** Definizione dell'architettura logica, tecnica e tecnologica della soluzione software.
* **Implementazione:** Codifica effettiva e scrittura del codice sorgente.
* **Validazione e Verifica:** Attività di testing e controllo qualità per garantire l'assenza di difetti e la conformità ai requisiti.
* **Rilascio e Installazione (Deployment):** Distribuzione del software e messa in produzione nell'ambiente di destinazione.
* **Gestione del Progetto (Project Management):** Monitoraggio, pianificazione e coordinamento di risorse, tempi e costi.

> [!IMPORTANT]
> **Il punto di svolta:** I diversi modelli di sviluppo non si distinguono per *quali* attività svolgono (che sono quasi sempre le stesse), ma per **quando** e in quale **ordine temporale** decidono di eseguirle.

---

## Modelli di Ciclo di Vita a Confronto

### 1. Modello a Cascata (Waterfall)
Prevede un approccio rigidamente sequenziale: ogni fase inizia solo ed esclusivamente quando la precedente è giunta a totale completamento. 

> [!WARNING]
> Il modello a cascata può risultare funzionale per team molto ridotti o in contesti con requisiti cristallini e totalmente immutabili. Tuttavia, nello scenario moderno il cambiamento è inevitabile; per questo motivo è quasi sempre preferibile migrare verso strategie di **sviluppo evolutivo**.

### 2. Sviluppo Evolutivo e Iterativo
Questo paradigma si basa sulla scomposizione del progetto in cicli ripetuti (**iterazioni**) e sul rilascio progressivo di versioni del software, basandosi su feedback regolari.

I suoi concetti cardine includono:
* **Timeboxing:** Fissare una durata temporale rigida e inderogabile per ogni iterazione (es. da 2 a 4 settimane). Se il tempo non basta, si riduce l'ambito delle funzionalità, mantenendo la scadenza immobile.
* **Iterazioni Incrementali:** Il sistema cresce per gradi; ogni singolo ciclo produce un incremento di codice funzionante, evolvendo parallelamente sia i requisiti sia l'architettura.
* **Backlog:** Un registro dinamico e costantemente aggiornato dei requisiti o dei task ancora da sviluppare, ordinati per priorità.
* **Milestone e Rilasci:** Traguardi intermedi definiti da avanzamenti interni (*internal releases*) che maturano progressivamente fino alla release di produzione finale.
* **Rigore Metodologico:** È un approccio disciplinato ed elaborato che richiede la gestione parallela di tre grandi aree:
  1. Definizione continua dei requisiti.
  2. Modellazione del business (*business model*).
  3. Progettazione tecnica strutturata.

> [!NOTE]
> **Unified Process (UP):** È l'esempio più strutturato di processo iterativo e incrementale, specificamente modellato e ottimizzato per lo sviluppo di sistemi orientati agli oggetti (OO).

---

## Il Paradigma Agile
La filosofia Agile sposa pienamente il modello evolutivo e iterativo, spingendo al massimo la reattività al cambiamento e la flessibilità operativa. In questo contesto, l'**Agile Modelling** si focalizza sulla creazione di modelli (come i diagrammi UML) agili e leggeri, usati come strumenti di discussione dinamica piuttosto che come documentazione rigida.

> [!IMPORTANT]
> ### I 4 Pilastri del Manifesto Agile
> Nello sviluppo agile viene attribuito un valore superiore a:
> 1. **Gli individui e le interazioni** *rispetto ai processi e agli strumenti.*
> 2. **Il software funzionante** *rispetto alla documentazione esaustiva.*
> 3. **La collaborazione con il cliente** *rispetto alla negoziazione contrattuale.*
> 4. **Rispondere al cambiamento** *rispetto al seguire un piano precostituito.*

### Il Framework Scrum
Scrum è una metodologia agile incentrata sul principio di "affrontare prima i requisiti a maggior valore business", organizzando il lavoro in cicli brevi chiamati **Sprint**.

| Categoria | Elemento | Descrizione Operativa |
| :--- | :--- | :--- |
| **Ruoli** | **Product Owner** | Custode della visione del prodotto. Gestisce le priorità del Product Backlog per massimizzare il valore del business. |
| | **Development Team** | Gruppo di professionisti cross-funzionale e auto-organizzato che sviluppa l'incremento pratico di software. |
| | **Scrum Master** | Facilitatore del team. Rimuove gli impedimenti e assicura che le pratiche del framework siano comprese e applicate. |
| **Artefatti** | **Product Backlog** | Elenco ordinato e centralizzato di tutte le funzionalità, modifiche e correzioni necessarie per il prodotto. |
| | **Sprint Backlog** | Selezione di task estratti dal Product Backlog da completare durante lo Sprint corrente, corredati dal piano per realizzarli. |
| **Eventi** | **Sprint Planning** | Riunione strategica iniziale per definire l'obiettivo dello Sprint e selezionare il lavoro da svolgere. |
| | **Daily Scrum** | Allineamento quotidiano di massimo 15 minuti per fare il punto sul lavoro svolto e pianificare le successive 24 ore. |
| | **Sprint Review** | Ispezione finale a fine Sprint per mostrare l'incremento software funzionante agli stakeholder e raccogliere feedback. |
