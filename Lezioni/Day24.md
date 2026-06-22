# 24 - GRASP: Progettazione di oggetti con responsabilità - 25/05/2026

> [!NOTE]
> ### Il Principio Generale dell'Assegnazione di Responsabilità
> Il cardine dell'assegnazione consiste nell'affidare una determinata responsabilità all'**esperto delle informazioni (Information Expert)**, ossia alla classe che detiene tutti i dati necessari per poterla soddisfare.
> 
> * **Caratteristiche:** È il pattern più frequentemente utilizzato per allocare compiti nel software e promuove fortemente l'incapsulamento delle informazioni.
> * **L'effetto "Antropomorfo":** Spesso porta a progetti in cui gli oggetti software compiono azioni che, nel mondo reale, verrebbero eseguite *sopra* di essi in quanto inanimati. Al contrario, se un oggetto rappresenta un'entità animata del mondo reale (es. una persona), nel software esso non farà le medesime cose che compie nella realtà.
> * **Controindicazioni:** Le soluzioni suggerite puramente dal pattern Expert potrebbero rivelarsi povere e andare in netta contraddizione con i principi di *Low Coupling* e *High Cohesion*.

---

## I Pilastri della Progettazione Modulare

L'accoppiamento e la coesione costituiscono le fondamenta della **progettazione modulare**, ovvero la proprietà di un sistema di essere decomposto in elementi (moduli) altamente coesi e debolmente accoppiati.

### 1. Accoppiamento (Coupling)
Rappresenta la misura di quanto fortemente un elemento sia connesso ad altri componenti, li conosca o dipenda da essi.
* **Accoppiamento Basso (Debole):** Il componente non dipende eccessivamente dagli altri elementi del sistema. È la condizione ottimale da perseguire.
* **Accoppiamento Alto (Forte):** Il componente fa profondo affidamento su troppi altri elementi, rendendo il sistema rigido.

### 2. Coesione Funzionale (Cohesion)
Rappresenta la misura di quanto siano strettamente correlate tra loro le responsabilità e le operazioni esposte da un elemento software, misurando al contempo la quantità di lavoro che esso svolge.
* **Coesione Alta:** La classe ha responsabilità fortemente correlate e non si fa carico di una mole eccessiva di lavoro.
* **Coesione Bassa:** La classe esegue troppe attività tra loro scollegate o svolge troppo lavoro centralizzato.

> [!TIP]
> **Vantaggi della Modularità (Separazione degli Interessi):**
> I moduli consentono di analizzare e progettare il software trattando i loro dettagli interni in isolamento e le loro interazioni in modo complessivo. Questo approccio favorisce direttamente la comprensione del codice, la modificabilità del sistema e il riuso dei componenti.

---

## La Modificabilità e il Calcolo dei Costi

> **Modificabilità:** La facilità con cui un sistema o un progetto può recepire e accettare i cambiamenti.

> [!IMPORTANT]
> ### Quanto costa effettuare una modifica software?
> Il costo e il tempo complessivo di implementazione (comprensivo di sviluppo, verifica e rilascio) relativo a una caratteristica o responsabilità si calcola sommando due fattori:
> 1. **Costo di modifica dell'elemento direttamente responsabile:** Questo fattore dipende strettamente dalla **coesione** del sistema. Una coesione alta garantisce una modifica localizzata e circoscritta, riducendo il costo al minimo.
> 2. **Costo di modifica degli altri elementi coinvolti indirettamente:** Questo fattore dipende strettamente dall'**accoppiamento** del sistema. Un accoppiamento basso garantisce che pochissimi elementi esterni vengano impattati di riflesso, mantenendo basso il costo.

### Linee Guida per il Codice Clean
* **Per un'Alta Coesione:** Mantieni quanto più possibile unite, nel medesimo blocco di codice, le cose che devono cambiare insieme per lo stesso motivo.
* **Per un Basso Accoppiamento:** Separa il più possibile le cose non correlate, affinché possano cambiare in modo totalmente indipendente.
* **Regola d'oro del design OO:** Ogni classe deve rappresentare uno e un solo concetto ben definito; ogni metodo deve essere responsabile di uno e un solo compito ben definito.

> Nello sviluppo è fondamentale non fermarsi alla prima idea, ma prendere in esame molteplici soluzioni candidate alternative, valutandole e confrontandole prima di effettuare la scelta definitiva.

---

## Tassonomia Qualitativa di Coesione e Accoppiamento

### Livelli di Coesione (Dalla peggiore alla migliore)
1. **Coesione per pura coincidenza (Terribile):** Elementi o metodi raggruppati all'interno di una classe in modo totalmente casuale.
2. **Coesione temporale (Mista):** Elementi accoppiati nella stessa classe solo perché vengono eseguiti o utilizzati all'incirca nel medesimo intervallo di tempo.
3. **Coesione dei dati (Solitamente buona):** Classi nate con lo scopo specifico di implementare e incapsulare un tipo di dato.
4. **Coesione funzionale (Ottima):** Tutti gli elementi della classe cooperano strettamente per svolgere un'unica funzione logica. *(Nota: Quando si parla genericamente di coesione, ci si riferisce a questa).*

### Livelli di Accoppiamento (Dal peggiore al migliore)
1. **Accoppiamento per dati interni (Terribile):** Un modulo accede direttamente ai dati privati interni di un altro oggetto.
2. **Accoppiamento mediante dati globali (Cattivo):** Più moduli dipendono e condividono la medesima variabile globale.
3. **Accoppiamento per sottoclasse (Può essere cattivo):** Il legame tra sottoclasse e superclasse (generalizzazione); introduce un vincolo strutturale forte.
4. **Accoppiamento di associazione (Comune):** Una classe gestisce variabili o dati che sono istanze di altre classi software.
5. **Accoppiamento mediante parametri (Comune):** Una classe definisce operazioni le cui segnature sono parametriche rispetto ad altre classi.
6. **Accoppiamento di uso (Comune):** Una classe richiede l'esecuzione di operazioni di altre classi avvalendosi strettamente delle loro interfacce esterne.

---

## Approfondimento: Pattern Low Coupling

Per minimizzare l'impatto dei cambiamenti, occorre ridurre l'accoppiamento non necessario. Le forme più comuni di accoppiamento da un tipo X a un tipo Y includono:
* La classe X possiede una variabile d'istanza (attributo) di tipo Y.
* Un oggetto X invia messaggi (chiede servizi) a oggetti di tipo Y.
* Un metodo della classe X fa riferimento a un'istanza di Y (come parametro, variabile locale o tipo di ritorno).
* X è una sottoclasse (diretta o indiretta) di Y.
* Y è un'interfaccia e X la implementa formalmente.

Altre forme di accoppiamento includono l'atto in cui un oggetto X crea fisicamente oggetti di tipo Y, o quando X accede alle variabili d'istanza di Y.

> [!WARNING]
> * L'accoppiamento derivante dalla generalizzazione (sottoclasse-superclasse) è per sua natura molto forte e rigido.
> * Una delle forme più subdole e dannose di accoppiamento e cattiva coesione è la presenza di **codice duplicato**, spesso frutto dell'abuso della cattiva pratica del "copia-incolla-modifica".
> * Proteggersi preventivamente da qualsiasi cambiamento futuro isolando classi stabili è un'operazione estremamente costosa: è necessario saper scegliere le proprie battaglie progettuali.

> [!CAUTION]
> Durante la progettazione del dominio, non è opportuno utilizzare strutture dati come `Map<A, B>` in cui sia la chiave A che il valore B siano classi software che rappresentano concetti complessi del dominio. Questa pratica va evitata in favore di tipi semplici, a meno che non si tratti dell'unica situazione possibile in cui non si ha il controllo diretto sull'oggetto A ma sia indispensabile gestirne l'informazione.

---

## Approfondimento: Pattern High Cohesion

Garantisce che gli oggetti rimangano focalizzati, comprensibili e facilmente gestibili, supportando di riflesso il mantenimento di un basso accoppiamento.
* Una classe ad alta coesione presenta **pochi metodi** con funzionalità strettamente correlate tra loro.
* Svolge una quantità di lavoro ridotta: se un compito risulta troppo complesso, la classe non lo accentra, ma distribuisce lo sforzo collaborando e delegando ad altri oggetti.

> **Coesione nei sistemi distribuiti:** Il principio della coesione è valido anche per applicazioni che comunicano via rete: mantenere operazioni coese ed evitare un'eccessiva frammentazione serve a scongiurare il transito di troppi messaggi in rete.

---

## Anti-Pattern e Principi di Riferimento

### 1. Code Duplication (Duplicazione del Codice)
Rappresenta un grave difetto di progettazione. La logica ripetuta va estratta, centralizzata o ricondotta a una classe differente mediante l'innalzamento del livello di astrazione del software.

### 2. Single-Responsibility Principle (SRP)
Principio secondo cui ogni elemento software deve avere una e una sola ragione per cambiare, focalizzandosi su un'unica responsabilità ben definita.

### 3. Il Blob o God Object (Oggetto Dio)
Un anti-pattern strutturale che si verifica quando un singolo oggetto accentra su di sé l'intero svolgimento di un compito complesso, manifestando una bassissima coesione e un altissimo accoppiamento. In questo scenario degradato, le altre classi del sistema tendono a essere **anemiche**, ossia ridotte a meri contenitori passivi di dati privi di comportamento. Il rischio di trasformare un *Controller* in un Blob è molto frequente se non si applica correttamente la delega.

---

## Il Pattern Controller

Il Controller è il primo oggetto posizionato oltre lo strato dell'interfaccia grafica (UI) preposto a ricevere e coordinare l'esecuzione di un'operazione di sistema. Rappresenta lo **Strato Application** del sistema.

### Strategie di Implementazione
* **Facade Controller:** Un unico oggetto che si fa carico di rappresentare l'intero sistema complesso o l'intero pacchetto software. Rappresenta la scelta ottimale per avviare il progetto, per poi procedere a un refactoring incrementale verso strutture più articolate.
* **Use Case / Session Controller:** Un controller dedicato a gestire una specifica istanza del caso d'uso in cui si verifica l'operazione (es. `SaleController`). Diventa di fondamentale importanza all'interno di sistemi complessi per memorizzare lo stato transiente del caso d'uso e lo stato delle sessioni utente.

> [!IMPORTANT]
> **L'obbligo di Delega:** Il Controller deve limitarsi esclusivamente a coordinare il flusso. Non deve svolgere il lavoro operativo internamente, ma deve **delegare** la logica di business agli oggetti del dominio, al fine di evitare la sua degenerazione nell'anti-pattern *Blob*.

### Distinzione Concettuale
È fondamentale non confondere il **Controller GRASP** (chiamato anche *controller del dominio*) con il **Controller del pattern MVC** tipico del mondo Web: sebbene possano collaborare nel medesimo ecosistema software, rispondono a responsabilità e livelli architetturali differenti.

> [!TIP]
> **Interfacce di Sistema per i Casi d'Uso:**
> * I controller di caso d'uso implementano una singola interfaccia di sistema specifica.
> * Il Facade Controller si fa carico di implementare tutte le interfacce di sistema globali.
> * Si progetta assumendo che il controller gestisca **un singolo utente alla volta**; la scalabilità concorrente viene demandata alle infrastrutture tecnologiche sottostanti. Evitare sempre la stesura di controller gonfi di logica.
