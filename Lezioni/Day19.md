# 19 - GRASP: Progettazione di oggetti con responsabilità & Esempi di progettazione a oggetti con i pattern GRASP - 30/04/2026

> [!TIP]
> ### Workflow Algoritmico nella Progettazione a Oggetti
> 1. Individua chiaramente qual è la singola responsabilità software da assegnare.
> 2. In base alla tipologia di responsabilità, seleziona il pattern GRASP più idoneo da applicare.
> 3. Sulla base delle linee guida del pattern scelto, individua l'oggetto specifico a cui allocare il compito.
> 4. Chiediti in che modo l'oggetto selezionato possa adempiere a tale responsabilità.
> 5. L'analisi del punto precedente guiderà naturalmente verso l'identificazione di sotto-responsabilità secondarie da assegnare a catena.

---

## Analisi Dinamica e Assegnazione: Caso di Studio POS

### 1. Operazione di Sistema: `makeNewSale`

* **Scelta del Controller:** Chi riceve questo evento di sistema oltre lo strato UI? Applicando il pattern *Controller* (scelta orientata alla Facade), viene selezionata la classe **Cassa (Register)**.
* **Scelta del Creatore:** Chi deve istanziare l'oggetto della vendita (`Sale`)? Applicando il pattern *Creator*, la responsabilità viene affidata alla **Cassa (Register)** poiché gestisce direttamente il ciclo di vita delle vendite.
* **Formazione del Collegamento:** Per registrare la relazione stabile e mantenere il riferimento, l'istanza della Cassa valorizza la propria variabile di stato interna:
  * `{currentSale = s}`
* **Inizializzazione delle Collezioni:** L'oggetto `Sale` gestirà un'associazione a molti con i singoli elementi della vendita attraverso una lista ordinata denominata `lineItems`. Pertanto, all'interno del costruttore di `Sale`, viene invocata la creazione esplicita della struttura dati:
  * `create() -> lineItems: List«SalesLineItem»`

---

### 2. Operazione di Sistema: `enterItem`

* **Scelta del Controller:** La responsabilità di ricevere l'evento ricade nuovamente sull'oggetto **Register (Cassa)**.

> **Regola di Analisi Dinamica:** Spesso gli attori fisici del dominio non possiedono una rappresentazione diretta del comportamento logico all'interno dei casi d'uso software. Il comportamento e le azioni degli attori vengono centralizzati e associati direttamente al rispettivo oggetto *Controller*.

* **Determinazione del Creatore di `SalesLineItem`:** Il controller Cassa non crea direttamente la riga, ma delega il compito all'oggetto esperto. La Cassa interroga l'istanza della vendita corrente affinché generi la nuova riga di dettaglio.
* **Flusso dei Messaggi (Execution Trace):**
  `enterItem() -> :Register -> makeLineItem() -> currentSale: Sale -> create() -> sl: SalesLineItem`

> [!NOTE]
> **Distinzione Semantica della Nomenclatura:** La parola chiave `create` è rigorosamente riservata all'istanziazione nativa e diretta di un oggetto (chiamata al costruttore), mentre il prefisso `make` viene utilizzato quando si richiede a un terzo oggetto di coordinare la creazione di un'entità per nostro conto.

* **Dettaglio delle Interazioni nel Diagramma di Comunicazione:**
  * `2.1: create() -> sl: SalesLineItem` (La vendita istanzia la riga)
  * `2.2: add() -> lineItems: List«SalesLineItem»` (La vendita inserisce la riga nella propria lista interna)

#### Risoluzione della Descrizione Prodotto (`ProductDescription`) tramite `itemID`
* **Applicazione di Information Expert:** La classe deputata a conoscere tutte le specifiche dei prodotti è il **Catalogo Prodotti (Product Catalog)**, il quale organizza internamente le informazioni tramite una mappa indicizzata.
* **Compromesso di Progettazione:** Viene introdotta una connessione diretta e cosciente tra l'oggetto `Register` e l'oggetto `Product Catalog`. Questa scelta aumenta intenzionalmente l'accoppiamento globale del sistema, ma ne ottimizza le prestazioni operative.
* **Flusso di Recupero Dati:**
  `enterItem() -> :Register -> 1: desc = getProductDesc(id) -> :Product Catalog -> 1.1: desc = get(id) -> description: Map«ProductDescription»`

> [!NOTE]
> Nel caso in cui il sistema si appoggiasse a un DBMS reale per la persistenza, l'oggetto `Product Catalog` rimarrebbe comunque il componente architetturale più idoneo a farsi carico della comunicazione con la base dati.

---

## Il Pattern Strutturale: "IDs to Objects"

Una volta recuperato il riferimento all'oggetto `ProductDescription` dal catalogo, questo viene associato direttamente alla riga di dettaglio appena creata (`SalesLineItem`):
* Vincolo di assegnamento: `{description = desc}`

> [!WARNING]
> **Verifica dei Collegamenti Progettati:** Durante la stesura del diagramma delle classi di progetto (DCD), è obbligatorio verificare accuratamente che ogni associazione navigabile introdotta risponda a una reale utilità logica e che venga effettivamente formata da un messaggio software a runtime.
