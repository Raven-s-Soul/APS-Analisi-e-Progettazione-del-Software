# 20 - Progettare per la visibilità & Esempi di progettazione a oggetti con i pattern GRASP - 11/05/2026

> **Il principio cardine della Visibilità:** Un oggetto Mittente può inviare un messaggio a un oggetto Destinatario solo ed esclusivamente se il mittente possiede una **visibilità** (un riferimento valido in memoria) verso il destinatario. Il progetto software ha l'obbligo di garantire e strutturare tutte le visibilità necessarie a consentire le interazioni a runtime.

### I Quattro Tipi di Visibilità



1. **Visibilità per Attributo (Duratura):** L'oggetto B è un attributo (variabile d'istanza) dell'oggetto A. Finché esiste A, il riferimento a B persiste.
2. **Visibilità per Parametro (Temporanea):** L'oggetto B viene passato come argomento all'interno di un metodo dell'oggetto A. La visibilità scade al termine dell'esecuzione del metodo.
3. **Visibilità Locale (Temporanea):** L'oggetto B viene istanziato o recuperato come variabile locale interna a un metodo dell'oggetto A. Non sopravvive al di fuori del blocco d'esecuzione.
4. **Visibilità Globale (Permanente):** L'oggetto B è accessibile globalmente da qualsiasi punto dell'applicazione. È una strategia generalmente sconsigliata, ma implementata in casi specifici tramite il pattern **Singleton [GoF]**.

---

## Ciclo di Vita delle Informazioni

La persistenza dei dati determina la scelta dei meccanismi di visibilità:
* **Informazioni Persistenti:** Destinate a sopravvivere stabilmente nel tempo (gestite tramite un DBMS).
* **Informazioni Transienti:** Dati che devono sopravvivere lungo i diversi passi di un caso d'uso (memorizzati in variabili d'istanza degli oggetti di dominio).
* **Variabili Locali:** Informazioni ultra-transienti che non sopravvivono nemmeno al passaggio tra i singoli step sequenziali di un'operazione di sistema.

---

## Esempi di Progettazione a Oggetti (Caso di Studio POS)

### 1. Operazione di Sistema: `endItemEntry`
* **Problema:** Chi ha la responsabilità di calcolare il totale complessivo della vendita?
* **Applicazione di Information Expert:** Per calcolare il totale sono necessarie le informazioni sul prezzo (contenute in `ProductDescription`) e le quantità di ogni riga (contenute in `SalesLineItem`). Poiché queste informazioni sono frammentate, la responsabilità viene assegnata all'oggetto **Sale (Vendita)**, che agisce come radice (capo del grafo ad albero) dell'intera struttura.

#### Traccia dei Messaggi (Execution Trace):
1. L'operazione interroga la vendita: `tot = getTotal() -> :Sale`
2. La vendita itera sulla propria collezione interna per calcolare i parziali: `1 * [i = 1...n]: st = getSubtotal() -> lineItems[i]: SalesLineItem` *(Nota: a lezione è stato specificato che è accettabile anche la forma contratta `1 * st = getSubtotal`)*.
3. Ciascuna riga interroga il catalogo per conoscere il prezzo del prodotto: `1.1: pr = getPrice() -> :ProductDescription`

> L'operazione `getTotal` rappresenta un'interrogazione (risposta di sistema). Questo tipo di funzioni è fondamentale perché guida e motiva le scelte del progettista sulla configurazione delle visibilità e dei riferimenti tra le classi.

> [!NOTE]
> ### Strategie di Gestione di un Dato Derivato
> Quando un'informazione è calcolata (derivata), si aprono due opzioni:
> 1. **Virtualizzazione del dato:** Il valore non viene salvato; si descrive l'algoritmo per calcolarlo dinamicamente ogni volta che viene richiesto.
> 2. **Materializzazione del dato:** Il valore viene calcolato una volta e memorizzato come proprietà strutturale (attributo) di un oggetto. Semplifica la lettura successiva, ma rende più complessa e onerosa la fase di aggiornamento.

---

### 2. Operazione di Sistema: `makeCashPayment`
* **Problema:** Chi deve farsi carico della creazione del nuovo oggetto `CashPayment`?
* **Analisi delle Alternative (Pattern Creator):** L'input iniziale (`amount`) viene inserito dal cassiere ed è ricevuto direttamente dal controller **Register (Cassa)**. 

Per identificare la soluzione migliore, confrontiamo le due opzioni in termini di accoppiamento e coesione:

| Criterio di Valutazione | Soluzione A: Creazione in `Register` | Soluzione B: Creazione delegata a `Sale` |
| :--- | :--- | :--- |
| **Accoppiamento (Coupling)** | **Rapporto: 3.** `Register` deve conoscere `Sale`, `CashPayment` (per crearlo) e infine associare il pagamento a `Sale`. | **Rapporto: 2 (Migliore).** `Register` conosce solo `Sale`. Sarà poi `Sale` ad accoppiarsi a `CashPayment` creandolo e salvandone il riferimento. |
| **Coesione (Cohesion)** | **Bassa.** `Register` si fa carico sia di ricevere l'input, sia di creare l'oggetto pagamento, sia di coordinare l'aggiunta. | **Alta (Migliore).** `Register` espone solo il metodo `makeCashPayment()`, delegando la logica strutturale alla vendita. |

* **Conclusione:** Si sceglie la **Soluzione B**. delegando la creazione a `Sale` per mantenere l'accoppiamento più basso e una coesione più elevata.

#### Gestione della Vendita Completata
Una volta terminato il pagamento, l'oggetto **Store (Negozio)** ha la responsabilità di registrare e conoscere la vendita conclusa.
* *Nota di progettazione:* Si potrebbe teoricamente introdurre un libro mastro (`Ledger`), ma nel caso d'uso d'esempio si è preferito utilizzare direttamente lo `Store`.
* **Scelta strutturale:** Si sconsiglia tassativamente di salvare le vendite completate all'interno del controller `Register`; se la cassa fisica dovesse rompersi o resettarsi, i dati andrebbero persi. Il posizionamento corretto per la visibilità a lungo termine è l'oggetto `Store`.

---

### 3. Operazione di Sistema: `getBalance`
* **Problema:** Chi è responsabile di calcolare il resto dovuto al cliente?
* **Soluzione:** Viene scelto l'esperto dominante del blocco informativo, ovvero la radice **Sale (Vendita)**, evitando di demandare l'operazione direttamente all'oggetto isolato `CashPayment`.
* **Vincolo logico:** L'operazione `bal = getBalance()` risponde al vincolo formale:
  `{bal = p.amount - s.total}`

> [!WARNING]
> **Verifica di Chiusura della Progettazione:** Al termine della modellazione, è fondamentale verificare che ogni singolo collegamento navigabile introdotto nel diagramma statico sia realmente utile e che esista un messaggio dinamico nei diagrammi di interazione preposto a formare e valorizzare quel riferimento a runtime.
