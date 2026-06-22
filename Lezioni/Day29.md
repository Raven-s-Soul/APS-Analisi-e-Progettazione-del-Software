# 29 - GRASP: altri oggetti con responsabilità - 08/06/2026

## Pattern GRASP Avanzati (Seconda Parte)

### 1. Pattern Polymorphism (Polimorfismo)

* **Problema:** Come gestire varianti e alternative di comportamento basate sul tipo? Come creare componenti software facilmente inseribili, intercambiabili e "pluggabili"?
* **Soluzione:** Evitare l'uso di istruzioni condizionali per ramificare la logica in base al tipo. Assegnare la responsabilità del comportamento direttamente **ai tipi per i quali il comportamento varia**, sfruttando le operazioni polimorfe.

> [!IMPORTANT]
> ### Regole e Sfumature di Applicazione del Polimorfismo
> * **Zero logica condizionale:** Non testare mai esplicitamente il tipo di un oggetto a runtime (es. niente `instanceof` o switch sui tipi).
> * **Estensibilità pulita:** Consente di introdurre nuove classi nel sistema con un impatto basso o nullo sulle classi preesistenti.
> * **Attenzione alla semantica:** Non assegnare la responsabilità di un comportamento ai tipi *di cui* varia il comportamento, ma ai tipi *per i quali* il comportamento varia!
> * **Variazione parametrica:** Se il cambiamento comportamentale può essere risolto semplicemente passando parametri diversi a un unico metodo, il polimorfismo non è necessario ed è una sovrastruttura inutile.
> 
> *Esempi visti a lezione:* Il caso del **Monopoly** con la gestione polimorfa delle Caselle (`Square`) e il caso del **POS** con l'astrazione tramite classi *Adattatore*.

> [!CAUTION]
> **Modellazione Dinamica delle Sottoclassi:** > Nel gioco del Monopoly, il Giocatore delega l'azione specifica direttamente alla casella. Quando nei diagrammi di interazione viene invocata un'operazione polimorfa, l'interazione generale su quel diagramma si interrompe: la progettazione prosegue creando un diagramma di comunicazione separato e distinto per ciascuna sottoclasse concreta della classe astratta/interfaccia.

> [!TIP]
> ### Interfaccia o Superclasse Astratta?
> * Moltissimi design pattern combinano il polimorfismo con i principi di composizione e delega.
> * Spesso il polimorfismo non si applica direttamente agli oggetti del dominio puro, bensì a oggetti polimorfi artificiali associati a essi.
> * **La scelta:** L'interfaccia è uno strumento flessibile e meno vincolante, ma se emerge la necessità reale di ereditare codice o attributi comuni, la superclasse astratta rimane l'unica strada percorribile. 
> * *Nota di pragmatismo:* Se la variazione logica è estremamente ridotta e circoscritta, le comuni istruzioni condizionali possono temporaneamente bastare.

---

### 2. Pattern Indirection (Indirizzamento Indiretto)



* **Problema:** Come disaccoppiare due elementi o servizi in modo da mantenere l'accoppiamento globale basso e salvaguardare un alto potenziale di riuso?
* **Soluzione:** Assegnare la responsabilità della comunicazione a un elemento intermediario interposto tra i due componenti.

> Moltissimi pattern famosi si configurano come declinazioni del principio di Indirezione:
> * Adattatore (Adapter)
> * Archivi di Persistenza (`PersistentStorage`)
> * Bridge, Facade, Observer, Mediator.
> 
> *Controindicazione:* L'introduzione di troppi livelli di indirezione intermedi può generare un leggero decadimento delle prestazioni computazionali a runtime.

---

### 3. Pattern Protected Variations (Variazioni Protette)

* **Problema:** Come progettare oggetti, sottosistemi e intere architetture in modo tale che le variazioni o l'instabilità latente di alcuni elementi non si propaghino con impatti indesiderati su altri moduli?
* **Soluzione:** Identificare i punti prevedibili di variazione o instabilità e strutturare un'**interfaccia stabile** attorno a essi per schermare il resto dell'applicazione.

> I meccanismi concreti per implementare le Variazioni Protette includono:
> * Uso combinato di Polimorfismo e Adattatori.
> * Incapsulamento rigoroso dei dati privati.
> * Uso sistematico di interfacce, indirezioni e standard tecnologici.
> * Broker di messaggi e macchine virtuali.
> * Progettazione guidata dai dati (*data-driven design*) o tramite interpreti.
> * Meccanismi di service look-up, progettazione riflessiva o di meta-livello.
> * Accesso uniforme alle proprietà e adozione di linguaggi standard.

> **Punti di Variazione vs Punti di Evoluzione:**
> * I *punti di variazione* rispondono a diversità riscontrabili nei requisiti correnti e attuali del sistema.
> * I *punti di evoluzione* rappresentano speculazioni su possibili necessità future.
> * **Scegli le tue battaglie:** Bisogna prestare estrema attenzione a non cadere nella trappola del *future proofing* speculativo, evitando di scrivere codice complesso per proteggersi da cambiamenti che potrebbero non avvenire mai.

> [!NOTE]
> ### Radici Storiche del Principio
> * **Information Hiding (Parnas, 1972):** Principio volto a nascondere le scelte implementative e i dettagli di gestione di un modulo agli altri componenti, al fine di preservare la stabilità globale.
> * **Open-Closed Principle (Meyer, 1988):** Un modulo deve essere contemporaneamente *Aperto* all'estensione (es. tramite l'aggiunta di nuovi adattatori polimorfi) ma *Chiuso* alla modifica del codice esistente.

---

## Pattern di Domain-Driven Design (DDD)

### 1. Pattern Repository (Deposito)



* **Problema:** Fornire allo strato di dominio l'illusione che ogni oggetto persistente sia stabilmente salvato in una comune collezione in memoria, mascherando le interazioni con il database attraverso un'interfaccia standard.
* **Soluzione:** Il repository viene modellato definendo un'interfaccia generica ("Repository") accoppiata a una o più implementazioni tecnologiche concrete.

> * **Data Access Object (DAO):** Rappresenta l'implementazione specifica del repository preposta ad accedere fisicamente alla base di dati.
> * **Evoluzione del Dominio:** In contesti avanzati, l'uso del repository consente di superare oggetti rigidi come il `ProductCatalog`, facendo interagire le entità del dominio direttamente con la persistenza.
> * **Collocazione Architetturale:** Essendo definita tramite un'interfaccia pura indipendente dalla tecnologia, la segnatura del Repository viene memorizzata direttamente all'interno dello **Strato di Dominio**.

---

### 2. Pattern Entity (Entità)

* **Problema:** Gestire in modo coerente il ciclo di vita degli oggetti dotati di un'identità persistente e differenziata.
* **Soluzione:** Le entità vengono istanziate al di fuori del repository, ma la loro persistenza stabile viene delegata a quest'ultimo tramite metodi espliciti di salvataggio (es. `save()` o `create()`).

> ### Caratteristiche dell'Entità
> * Un'Entità è un oggetto software caratterizzato da una **propria identità univoca e immutabile**, progettato per sopravvivere a lungo termine all'interno del sistema, anche se i valori dei suoi attributi interni o dei sotto-oggetti cambiano continuamente nel tempo.
> 
> Ogni entità va analizzata sotto due lenti distinte:
> 1. **Punto di vista Concettuale:** Nel mondo reale, l'entità vive molto più a lungo del software. Nasce nel momento in cui quel concetto si manifesta nella realtà. Di conseguenza, l'asserzione *"è stata creata un'istanza di x"* nei contratti d'analisi si riferisce a questa nascita concettuale (che avviene una sola volta).
> 2. **Punto di vista del Software:** L'applicazione viene periodicamente chiusa, spenta o aggiornata, determinando la cancellazione degli oggetti dalla memoria RAM. Nel codice, una singola istanza concettuale può quindi avere molteplici rappresentazioni e rinascite software differenti.
> 
> **Il ruolo del Repository:** Il compito del Repository è proprio quello di gestire la perfetta corrispondenza e consistenza tra la persistenza software e l'esistenza concettuale dell'entità.
> * Per recuperare un'entità esistente si utilizzano i metodi `find()` o `get()`. Fuori dal repository **non si deve mai usare il costruttore `new`** per recuperare oggetti già esistenti.
> * Per aggiornare lo stato di un'entità, il flusso corretto prevede: `find()` per recuperare l'oggetto $\to$ esecuzione dei metodi setter (`setVar()`) per aggiornare i dati $\to$ invocazione del metodo `update()` sul repository.

---

### 3. Pattern Aggregati (Aggregates)

* **Problema:** Definire i confini di transazione e di accesso per gruppi di oggetti strettamente correlati per garantire l'integrità dei dati.
* **Soluzione:** Un Aggregato è un insieme di oggetti associati che costituisce un'unità atomica di accesso e manipolazione dei dati.

> L'aggregato è strutturato secondo una gerarchia precisa:
> * **Entity Root (Radice dell'Aggregato):** Un'entità dotata di identità propria ed esistenza individuale autonoma. Rappresenta l'unico punto di accesso autorizzato per l'esterno.
> * **Value Objects (Oggetti Valore):** Un gruppo di oggetti privi di identità o esistenza individuale autonoma. Hanno significato logico esclusivamente se analizzati in stretta relazione alla loro entità radice.
> 
> *(Nota della lezione: Gli esempi di implementazione del pattern tramite codice JPA ed annotazioni specifiche come `@Entity` ed `@Embeddable` sono stati omessi nei dettagli).*

---

> [!NOTE]
> Il programma ufficiale del corso di Ingegneria del Software per l'anno accademico 2026 si conclude qui.
