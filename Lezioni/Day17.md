# 17 - GRASP: Progettazione di oggetti con responsabilità & Esempi di progettazione a oggetti con i pattern GRASP - 27/04/2026

> La progettazione orientata agli oggetti (OOD) non deve basarsi sull'intuito, ma deve essere guidata da un percorso logico metodico, razionale e rigorosamente giustificabile.

> **Domande guida del progettista:**
> - *Qual è l'input corrente e cosa è stato definito nelle fasi precedenti?*
> - *Quali sono le attività concrete da svolgere adesso?*
> - *Qual è l'output atteso e come si collegano tra loro i vari manufatti prodotti?*

---

## Il Flusso di Lavoro: Input e Finalità

Il passaggio alla progettazione poggia su precisi elementi derivanti dalle fasi precedenti:

### 1. Elementi di Input
* **Dai Requisiti:** Casi d'uso, specifiche supplementari e glossario dei termini.
* **Dall'Analisi:** Modello di dominio statico, specifiche delle operazioni di sistema con i relativi diagrammi SSD e contratti operativi.

### 2. Approcci alla OOD
Il design del software può essere affrontato direttamente durante la stesura del codice, tramite sessioni di disegno leggero (sketching) o applicando altre tecniche di modellazione visuale.

> La modellazione non deve mirare alla mera documentazione formale del sistema, bensì alla comprensione profonda dei problemi e alla comunicazione efficace all'interno del team.

---

## Progettazione Guidata dalle Responsabilità (RDD)

La **Responsibility-Driven Design (RDD)** interpreta il software come una comunità di oggetti cooperanti. Una responsabilità rappresenta un'astrazione logica di ciò che un componente deve eseguire o gestire (in UML costituisce un vero e proprio obbligo o contratto per un classificatore).

### Classificazione delle Responsabilità
* **Responsabilità di FARE (Doing):** Riguardano l'azione pura. Si ricavano direttamente dai requisiti testuali, dai casi d'uso, dalle operazioni e dai vincoli dei contratti.
* **Responsabilità di CONOSCERE (Knowing):** Riguardano la conoscenza dei dati. Si desumono principalmente dalle entità e dalle relazioni presenti nel modello di dominio.

> **Granularità delle Responsabilità:**
> * **A grana fine:** Coinvolgono pochi oggetti circoscritti e guidano la progettazione di dettaglio (OOD).
> * **A grana grossa:** Riguardano la gestione di interi package o sottosistemi complessi, e ricadono nell'ambito della Progettazione Orientata all'Architettura.

### Il Concetto di Collaborazione
Per adempiere a una determinata responsabilità, un oggetto software può agire in autonomia oppure scegliere di **collaborare** attivamente con altre entità del sistema.

### Metodologie di Applicazione della RDD

> **Approccio 1 (Da evitare):** Identificare prima tutti gli oggetti, mappare successivamente le responsabilità globali e infine tentare di assegnarle definendo le collaborazioni. Questo metodo risulta spesso empirico e poco lineare ("un po' magico").

> [!NOTE]
> **Approccio 2 (Metodo adottato nel corso):** > 1. Isolare le singole responsabilità considerandole una alla volta.
> 2. Individuare la classe più idonea (tra quelle esistenti o introducendone una nuova) a cui assegnare tale responsabilità.
> 3. Definire la strategia di adempimento: l'oggetto può completare il compito da solo o necessita di collaboratori esterni? (In questo modo si delineano le collaborazioni).
> 4. Validare la scelta basandosi su criteri e principi di assegnazione standardizzati.

---

## Il Framework GRASP

I pattern **GRASP (General Responsibility Assignment Software Patterns)** formalizzano e codificano i principi cardine della progettazione a oggetti, fungendo da guida per allocare le responsabilità alle classi software.

> [!IMPORTANT]
> ### Pattern GRASP Fondamentali (Di Base)
> * **Creator:** Stabilisce quale classe sia responsabile della creazione di nuove istanze di un oggetto.
> * **Information Expert:** Assegna una determinata responsabilità alla classe che possiede tutte le informazioni necessarie per portarla a compimento.
> * **Low Coupling (Debole Accoppiamento):** Criterio di valutazione volto a mantenere le classi indipendenti, limitando l'impatto delle modifiche.
> * **High Cohesion (Alta Coesione):** Criterio volto a garantire che una classe si focalizzi su un insieme di compiti strettamente correlati, delegando il resto.
> * **Controller:** Identifica l'oggetto preposto a ricevere e coordinare gli eventi di sistema provenienti dallo strato UI.

> [!CAUTION]
> ### Pattern GRASP Avanzati
> * Polymorphism (Polimorfismo)
> * Pure Fabrication (Invenzione Pura)
> * Indirection (Indirizzamento Indiretto)
> * Protected Variations (Variazioni Protette)

### Logica di Selezione e Salto Rappresentazionale
I pattern GRASP fondamentali guidano l'analista nell'assegnare le responsabilità a oggetti software traendo ispirazione diretta dalle entità presenti nel modello di dominio reale.

> [!WARNING]
> Sebbene l'ispirazione sia concettuale, occorre evitare un salto rappresentazionale eccessivamente basso o forzato, poiché il tentativo di mappare rigidamente la realtà nel codice può indurre a gravi errori strutturali nel software.

---

## Cos'è un Pattern di Progettazione?

Un pattern è la descrizione strutturata e formalizzata di un problema progettuale ricorrente, abbinata a una soluzione consolidata ed esemplare applicabile nel contesto specifico.

> **Esempio di struttura (Information Expert):**
> * **Problema:** *Qual è il principio cardine per distribuire le responsabilità elementari agli oggetti?*
> * **Soluzione:** *Affidare il compito alla classe che detiene i dati e la conoscenza strutturale per risolverlo.*

* **Letteratura consigliata:** Il concetto di accoppiamento problema/soluzione vanta una vasta tassonomia. Il testo di riferimento storico consigliato è *"Design Patterns"* della Gang of Four (GoF, 1995), mentre il manuale di Larman si configura come un'eccellente introduzione pratica all'analisi e alla modellazione orientata agli oggetti.
