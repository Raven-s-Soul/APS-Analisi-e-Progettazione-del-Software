# 13 - Diagrammi delle classi & Diagrammi di interazione - 31/03/2026

## Modellazione Statica: I Diagrammi delle Classi di Progetto (DCD)
I diagrammi delle classi definiscono la struttura statica del software, formalizzando la relazione diretta tra la rappresentazione grafica e il codice sorgente effettivo.

> **Mondi a confronto:**
> * **UML (Mondo Reale):** Si parla di *Modello di Dominio*.
> * **Unified Process (Mondo Software):** Si parla di *Modello di Progetto*, espresso tramite il **Diagramma delle Classi di Progetto (DCD)**, che mappa direttamente i pezzi di codice.

### Il Classificatore e la Struttura dei Rettangoli
Le classi (e gli altri classificatori) descrivono le caratteristiche strutturali (variabili d'istanza) e comportamentali (metodi) degli oggetti. Vengono rappresentate tramite rettangoli suddivisi in 3 scomparti:

1. **Nome del Classificatore:**
   * **Classe Concreta:** Scrittura standard.
   * **Classe Astratta:** Nome in *corsivo* oppure accompagnato dalla stringa `{abstract}`.
   * **Interfaccia:** Nome accompagnato dalla parola chiave `«interface»` (contiene solo il nome e l'elenco delle operazioni).
2. **Attributi (Proprietà Strutturali):**
   * Sintassi: `Visibilità Nome : Tipo = ValoreIniziale [Molteplicità]`
   * Il simbolo `/` davanti al nome indica un attributo *derivato*.
   * Il nome *sottolineato* indica una variabile di classe (membro `static`).
   * **Mappatura:** Gli attributi si traducono direttamente in variabili d'istanza. Ciascuna istanza possiede una propria copia del dato, il cui valore viene preservato per tutto il ciclo di vita dell'oggetto.
3. **Operazioni:**
   * Sintassi: `Visibilità Nome(Parametro : Tipo) : TipoDiRitorno {Proprietà}`
   * Rappresentano la dichiarazione/prototipo di una trasformazione o interrogazione (mentre il **Metodo** rappresenta la sua effettiva implementazione nel codice).
   * Possono includere costruttori (esplicitati opzionalmente dalla parola chiave `«constructor»`). Quasi tutti gli elementi della firma sono opzionali.

> [!WARNING]
> ### Indicatori di Visibilità ed Errori Frequenti
> * `-` **Privato (Default):** Visibilità standard per gli attributi.
> * `#` **Protetto (Protected):** Visibilità limitata alla sottoclasse.
> * `+` **Pubblico:** **Errore critico da bocciatura all'esame** se applicato indiscriminatamente agli attributi, in quanto viola il principio di incapsulamento.

---

## Le Relazioni e la Navigabilità delle Frecce

Le connessioni tra le classi determinano il modo in cui gli oggetti comunicano e si referenziano nel codice.

* **Generalizzazione (Ereditarietà):** Linea continua con punta triangolare vuota rivolta verso la superclasse. *(Nota: Usare rigorosamente il termine "Generalizzazione" e non "ereditarietà").*
* **Implementazione di Interfaccia:** Linea tratteggiata con punta triangolare vuota rivolta verso l'interfaccia.
* **Associazione (Navigabilità):** Linea continua con punta di freccia aperta. Indica la presenza di un riferimento strutturale.
* **Dipendenza:** Linea tratteggiata con punta di freccia aperta. Indica una relazione temporanea e debole (es. un oggetto passato come parametro locale a un metodo).

> [!CAUTION]
> **Rappresentazione delle Relazioni:** Nei DCD le associazioni verso altre classi non primitive **non devono mai** essere scritte como stringhe di testo all'interno dello scomparto degli attributi. Vanno espresse **esclusivamente** tramite le linee grafiche di associazione, pena la bocciatura.

### Traduzione delle Associazioni in Codice Java

#### 1. Associazione Singola (Navigabilità 1 a 1)
La classe sorgente possiede una variabile d'istanza (il cui tipo corrisponde alla classe di destinazione) identificata dal *Nome di Ruolo* posto vicino alla freccia. La classe di destinazione non ha invece alcun riferimento alla sorgente.

```java
public class A {
    private B nomeVariabileB;
}

public class B {
    // Non ha alcun riferimento ad A
}
```

#### 2. Associazione a Molti (Navigabilità 1 a Molti)
Quando la molteplicità indica un raggruppamento (es. `1..*` o `*`), la variabile d'istanza si traduce in una collezione (Array, `List`, `Map`). Nei diagrammi si usano proprietà come `{ordered}` per specificare il comportamento della struttura.

```java
public class A {
    private List<B> listaB; 
}
```

> **Nota sui collegamenti:** A livello software, la classe fa riferimento all'oggetto collezione, il quale referenzia le singole istanze (es. `listaB.get(0)`). Nei diagrammi questa scomposizione viene lasciata implicita.

### Vincoli, Parole Chiave e Aggregazioni
* **Vincoli:** Vengono espressi tra parentesi graffe, ad esempio `{size >= 0}`. Possono essere posizionati accanto all'elemento o inseriti in una nota testuale collegata da una linea tratteggiata.
* **Costrutti equivalenti:** Per le finalità d'esame, termini di vincolo/parole chiave (`«constructor»` / `{abstract}`) o le distinzioni tra **Aggregazione** e **Composizione** non fanno differenza e vengono trattati allo stesso modo dal docente.

---

## Modellazione Dinamica: I Diagrammi di Interazione

Mentre i diagrammi delle classi analizzano la struttura statica (plurale, focalizzata su molteplici classi), i **Diagrammi di Interazione** analizzano il comportamento dinamico (singolare, focalizzato su come un gruppo specifico di oggetti collabora a runtime).

* L'interazione avviene tramite lo scambio di **Messaggi**: un oggetto mittente invoca un metodo, l'oggetto ricevente lo esegue.
* L'intero ciclo di esecuzione prende il via da un **Messaggio Trovato (Found Message)**, che rappresenta il compito iniziale da svolgere.

Esistono due tipologie principali di diagrammi di interazione, concettualmente equivalenti ma con focus grafici differenti:

### 1. Diagramma di Sequenza
Mappa le interazioni seguendo una linea temporale che si sviluppa da sinistra a destra e dall'alto verso il basso. Replica visivamente l'andamento dello Stack dei record di attivazione delle funzioni.

```java
public class A {
    public B myB;

    public void fn() { 
        myB.fn(); 
    }
}

public class B {
    public void fn() { 
        // ... 
    }
}
```

* *Vantaggio:* Estremamente facile e intuitivo da leggere.
* *Svantaggio:* Complesso da modificare o ridisegnare in caso di variazioni.

### 2. Diagramma di Comunicazione
Mostra l'interazione direttamente sulle linee di collegamento tra gli oggetti, utilizzando una numerazione sequenziale per ordinare i messaggi.
* *Vantaggio:* Molto facile e rapido da tracciare a mano o modificare.
* *Svantaggio:* Più difficile da interpretare a colpo d'occhio rispetto alla sequenza temporale.

### Messaggi Speciali e Convenzioni Grafiche
* **Messaggio `create`:** Rappresenta la nascita di un nuovo oggetto. Nei diagrammi di sequenza la freccia di ritorno è tratteggiata, mentre nei diagrammi di comunicazione il messaggio mantiene una linea continua.
* **Linee di Vita (Lifelines):** I rettangoli in cima rappresentano i partecipanti.
  * La sintassi `nomeSimbolico : TipoClasse` indica un oggetto specifico.
  * La sintassi `: TipoClasse` (senza nome prima dei due punti) indica un oggetto anonimo.
  * La presenza del solo nome della classe (senza i due punti `:`) non è ammessa per rappresentare istanze.
  * Una linea di vita che termina con una `X` indica la distruzione esplicita dell'oggetto.
* **Rappresentazione delle Collezioni:** Una collezione si indica con `nome : List<Tipo>`, mentre il singolo elemento estratto o scansionato viene indicato come `nome[i] : Tipo`.
* *Nota:* Gli oggetti di tipo *Singleton* vengono ignorati nelle interazioni standard del corso.
