# 28 - Ulteriore modellazione di dominio & Altri SSD e contratti & GRASP: altri oggetti con responsabilità - 04/06/2026

> **Recapitolo sulla Gerarchia di Classi e Classificazione:**
> * **Superclasse:** Rappresenta il concetto più generale. Ogni sottoclasse eredita tutte le proprietà strutturali (attributi e associazioni), che si applicano quindi a cascata a tutte le specializzazioni.
> * **Tipi di Classificazione:**
>   * *Singola vs Multipla*
>   * *Statica vs Dinamica*
>   * *Esempio Singola Statica:* Una persona viene modellata o come Studente o come Lavoratore, senza possibilità di mutare nel tempo.
>   * *Esempio Multipla Dinamica:* Una persona può essere contemporaneamente sia Studente sia Lavoratore, e cambiare il proprio ruolo nel corso del tempo.

---

## Modellare gli Stati che Cambiano nel Tempo

> **Caso di studio di riferimento:** L'evoluzione dello stato di un ordine all'interno di un ristorante (es. *Inviato*, *In Preparazione*, *Pronto*, *Servito*).

> [!TIP]
> **Linee Guida di Modellazione dello Stato:**
> * I possibili stati assunti da un concetto `X` **non devono mai** essere modellati come sottoclassi di `X`.
> * Si applica la logica del **Pattern State**: si associa l'oggetto principale a un oggetto di stato separato, evitando di modificare strutturalmente l'oggetto in sé.
> * Invece di implementare lo stato tramite un semplice dizionario o un tipo enumerativo (`Enum`), lo si modella come un riferimento a una classe specifica, ereditata da una classe astratta preposta a definire il ruolo o lo stato logico. Le molteplicità di questo legame possono variare a seconda dei vincoli di business.

> **Vincolo Metodologico:** Si ricorda che nella sintassi dei diagrammi UML esistono esclusivamente tre elementi primitivi utilizzabili: **Classi**, **Associazioni** e **Attributi**.

### L'Ereditarietà nel Software
Rappresenta la relazione formale tra classi nello strato di codice: la sottoclasse eredita nativamente la definizione di tutti gli attributi e delle operazioni della superclasse, conservando la facoltà di effettuare l'override (ridefinizione) dei metodi ereditati.

### Gestione dei Ruoli e degli Oggetti Mutabili
Per rappresentare ruoli o variazioni temporali degli oggetti, le opzioni d'analisi includono:
1. Modellare i ruoli come concetti indipendenti (classi separate).
2. Modellare i ruoli come associazioni dedicate.
3. Modellare i ruoli come attributi di stato interni.

> **Esempio del prezzo variabile:** Se il prezzo di un articolo cambia nel tempo, la soluzione consiste nell'aggiungere un attributo specifico di prezzo direttamente all'interno dell'oggetto che mappa la singola riga di vendita (fissando il valore a quell'istante temporale), mentre la classe descrizione del prodotto continuerà a variare il proprio prezzo base indipendentemente.

> [!CAUTION]
> **Costrutti UML Vietati all'Esame:**
> Le **Classi di Associazione** e le **Associazioni Qualificate** messe a disposizione dallo standard UML non devono essere utilizzate in sede d'esame (sebbene rimangano strumenti validi nella pratica professionale).

---

## Iterazione 3: Operazioni di Sistema e Contratti con Sistemi Esterni

L'introduzione di sistemi o attori esterni (come il servizio esterno per il calcolo delle imposte e delle tasse nell'operazione *Elabora Vendita* del POS) influisce sulla stesura dei contratti.

> **La specializzazione nei contratti:** Quando un'entità generale (es. `Payment`) si specializza tramite generalizzazione in più classi concrete (`CashPayment`, `CreditPayment`, `CheckPayment`), la sezione delle post-condizioni del contratto deve riflettere con precisione l'istanza specifica creata.
> * *Sintassi corretta:* *"È stata creata un'istanza p di CashPayment"* (oppure di `CreditPayment` / `CheckPayment` a seconda del tipo di operazione di sistema invocata).

---

## Pattern GRASP Avanzati

I quattro pattern avanzati preposti alla distribuzione delle responsabilità software sono:

### 1. Pattern Pure Fabrication (Invenzione Pura)
* **Problema:** Come preservare i principi di *High Cohesion* e *Low Coupling* quando l'applicazione dei pattern *Information Expert* e *Creator* costringerebbe ad assegnare responsabilità inappropriate a oggetti del dominio?
* **Soluzione:** Introdurre una classe artificiale (non ispirata ad alcun concetto del modello di dominio reale) a cui affidare la responsabilità, agendo come "ultima spiaggia" progettuale.

> **Il Pattern Repository (Deposito):** È un esempio tipico di Pure Fabrication. Si tratta di un oggetto progettato per incapsulare l'accesso fisico a una base di dati, offrendo al resto dell'applicazione l'illusione di interagire con una comune collezione in memoria di oggetti (esponendo le classiche operazioni CRUD).

> **La classe `PersistenceStorage`:** Altro esempio macroscopico di Pure Fabrication a grana grossa, utile per garantire il riuso architetturale o per fungere da canale di comunicazione standardizzato verso un intero sottosistema.

* **Oggetti di Dominio:** Orientati alle informazioni (valore rappresentazionale).
* **Oggetti Pure Fabrication:** Orientati esclusivamente al comportamento (servizi e logica).

> [!WARNING]
> **Rischio di Abuso:** Evitare la proliferazione incontrollata di classi artificiali. 
> * Alle Pure Fabrication vengono solitamente demandate responsabilità che l'Information Expert non riesce a gestire in modo pulito.
> * I *Controller di caso d'uso* sono, a tutti gli effetti, delle Pure Fabrication.
> * Virtualmente tutti i design pattern del catalogo della *Gang of Four (GoF)* si configurano strutturalmente come delle Pure Fabrication.

---

### 2. Pattern Polymorphism (Polimorfismo)
* **Problema:** Come gestire varianti e alternative di comportamento basate sul tipo di un oggetto senza irrigidire il codice? Come creare componenti software facilmente inseribili e intercambiabili?
* **Soluzione:** Evitare tassativamente l'uso di istruzioni condizionali (es. lunghi blocchi `if/else` o `switch`) e non testare mai esplicitamente il tipo di un oggetto a runtime. Assegnare la responsabilità del comportamento direttamente ai tipi per i quali il comportamento varia, definendo un'**operazione polimorfa** astratta sulla superclasse o sull'interfaccia.
