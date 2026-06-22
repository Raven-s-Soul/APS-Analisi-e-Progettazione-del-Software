# 16 - Diagrammi di interazione & Diagrammi delle classi - 23/04/2026

> **Concetto di Interazione:** Ripasso del meccanismo di comunicazione in UML. Affinché un oggetto mittente possa inviare un messaggio, deve obbligatoriamente possedere un riferimento (navigabilità) verso l'oggetto ricevente.

La sintassi generale per l'invocazione di un messaggio (in cui quasi tutti gli elementi sono opzionali) è:
```java
valore = messaggio(parametro: tipo) : tipoDiRitorno
```

> [!NOTE]
> ### Barre di Esecuzione e Record di Attivazione
> * Le barre verticali indicano la presenza del record di attivazione sullo Stack.
> * La restituzione di un valore a seguito di un messaggio può essere espressa sia in modo esplicito (freccia tratteggiata di ritorno) sia in modo implicito.
> * La **Self-call** (chiamata a un metodo dello stesso oggetto) genera un ulteriore record di attivazione sovrapposto.
> * Durante il messaggio di creazione (`create`), si possono passare argomenti al costruttore; la freccia punta direttamente al rettangolo dell'istanza `:Classe`.
> * La distruzione di un oggetto può essere esplicitata tramite la parola chiave `«destroy»` e una `X` che interrompe la linea di vita, ma non è obbligatoria: graficamente è sufficiente che la linea tratteggiata si interrompa.

---

## Gestione dei Collegamenti e delle Collezioni

La comunicazione cambia a seconda della molteplicità del legame tra le classi:

* **In presenza di molteplicità multipla (collezioni):** Ad esempio, l'oggetto mittente invoca un metodo per aggiungere un elemento a una lista, la quale riceve ed esegue l'operazione sul proprio tipo di dato.
* **In presenza di molteplicità singola (a uno):** Ad esempio, l'oggetto imposta il valore di una variabile d'istanza locale (operazione di assegnamento del tipo `this.var = var`).

### Interfacce standard delle Collezioni Java
* `Set<E>`: espone i metodi `add`, `remove`, `contains`, `size`.
* `List<E>`: espone i metodi `add`, `remove`, `get`, `size`.
* `Map<K, V>`: espone i metodi `add`, `remove`, `find` (espressi nel codice tipicamente come `put` e `get`), mantenendo la chiave lasciata implicita nei diagrammi.

> [!CAUTION]
> **Errore Grave da Bocciatura:** Le classi che rappresentano collezioni di dati non devono **mai** presentare messaggi uscenti nei diagrammi di interazione. Sono solo contenitori passivi di oggetti.

---

## Notazione nei Diagrammi di Sequenza: I Frame

Nei diagrammi di sequenza si utilizzano i blocchi di controllo (*Frame*) per gestire la logica algoritmica:
* `loop`: rappresenta le ripetizioni e i cicli (equivalente al costrutto `for` o `while`).
* `opt`: rappresenta un blocco opzionale condizionato (equivalente a un singolo `if`).
* `alt`: rappresenta percorsi mutualmente esclusivi (equivalente alla struttura `if / else`).

---

## Notazione nei Diagrammi di Comunicazione

I diagrammi di comunicazione esprimono le stesse informazioni ma con regole grafiche differenti.

> [!TIP]
> **Linee di collegamento e messaggi multipli:**
> * La linea che unisce due oggetti rappresenta il canale e **non ha punte di freccia**.
> * Se ci sono più messaggi sullo stesso canale, questi vengono elencati in fila accanto alla linea, indicando la direzione di ognuno con una piccola freccia posizionata accanto al testo del messaggio.
> * Si utilizza una **numerazione gerarchica** (es. `1`, `1.1`, `1.2`, `1.3`) per formalizzare l'ordine sequenziale delle chiamate e delle risposte.

### Sintassi dei Messaggi Condizionali e di Creazione
* Per indicare un oggetto appena creato, oltre a `create` o `«create»`, si può apporre la stringa `:Nome {new}`.
* **Nei blocchi condizionali (opt):** La condizione di guardia precede sempre il messaggio.
  * *Sintassi:* `1 [colore == rosso] : msg1()`
* **Nei blocchi alternativi (alt):** Si ramificano le condizioni escludenti.
  * *Sintassi:* * `1A [condizione X] : msgA()`
    * `1B [condizione Y] : msgB()`
    * `1C [not condizione Y] : msgC()`
* **Nei blocchi iterativi (loop):** Si inserisce il carattere asterisco `*`.
  * *Sintassi:* `1* [i = 1 ... n] : num = nextInt()` oppure genericamente `1* : a = funzione()`

> [!CAUTION]
> **Specifiche d'Esame:** In sede di esame scritto è esplicitamente richiesto e obbligatorio utilizzare i **Diagrammi di Comunicazione** per la modellazione dinamica.

> I diagrammi di interazione (dinamici) e i diagrammi delle classi (statici) non sono attività separate, ma vanno sviluppati e aggiornati sempre in parallelo.
