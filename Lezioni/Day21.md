# 21 - Esempi di progettazione a oggetti con i pattern GRASP & Trasformare i progetti in codice & Retrospettiva sull'iterazione 1 - 12/05/2026

## Collegamento tra UI e Logica di Dominio

* **Regola di Accesso:** Lo strato dell'interfaccia grafica (UI) deve poter interagire sicuramente con l'oggetto *Controller* e, se necessario, con altri oggetti notevoli del dominio.
* **Strategia di Implementazione:** Al momento dell'inizializzazione della UI, il riferimento al controller viene passato direttamente come parametro del costruttore. In questo modo, la UI mantiene l'accesso al controller per tutta la durata dell'applicazione e, tramite esso, può navigare verso gli altri elementi del dominio.

---

## Il Caso d'Uso di Avviamento (Startup)

Il caso d'uso di avviamento gestisce tutte le operazioni preliminari necessarie alla corretta configurazione e allocazione in memoria del sistema software. È rappresentato a livello dinamico dall'operazione di sistema globale **`startUp()`**.

### Logica di Progettazione
Si adotta un idioma progettuale consolidato: l'introduzione di un **oggetto di dominio iniziale**. Questo elemento va selezionato tra le classi posizionate al vertice (la radice) della gerarchia di contenimento, composizione o aggregazione degli oggetti del dominio reale.

> [!CAUTION]
> **Struttura di Avvio dell'Applicazione (Main Class)**
> 
```java
public class Main {
    public static void main(String[] args) {

        /* L'oggetto di dominio iniziale esegue l'operazione di startUp,
         * che si occupa di istanziare gli altri oggetti di dominio. */
        Store store = new Store();

        /* Avvia l'interfaccia grafica passando il controller 
         * come parametro del costruttore. */
        Register register = store.getRegister();
        ProcessSaleJFrame frame = new ProcessSaleJFrame(register);
        
        /* L'interfaccia grafica può così mantenere un riferimento
         * al controller per tutta la durata dell'applicazione. */
        frame.setVisible(true);
    }
}
```

> **Mappa delle Inizializzazioni e dei Collegamenti dello StartUp:**
> 
> * **Quali oggetti devono essere creati?**
>   * L'oggetto di dominio iniziale (es. `Store`).
>   * Un oggetto `Register` (Cassa).
>   * Un oggetto `ProductCatalog` e tutte le relative istanze di `ProductDescription`.
> 
> * **Quali collegamenti navigabili devono essere formati a runtime?**
>   * Da `Register` verso `ProductCatalog` (necessario per l'operazione *enterItem*).
>   * Da `ProductCatalog` verso tutte le istanze di `ProductDescription` (necessario per *enterItem*).
>   * Da `Store` verso `Register` (configurato durante la fase di *startUp*).
>   * Da `Register` verso `Store` (necessario per archiviare le vendite in *makeCashPayment*).
> 
> *Nota: L'allocazione di queste responsabilità segue fedelmente le direttive del pattern **Creator**.*

---

## Trasformare i Progetti in Codice: Il Modello di Implementazione

All'interno di Unified Process (UP), il **Modello di Implementazione** organizza tutti gli artefatti fisici e i file sorgenti prodotti dal team:
* Codice sorgente (es. file `.java`).
* Script di configurazione e popolamento SQL per i database.
* Pagine e file di configurazione HTML, XML, JSON, ecc.

> Il codice sorgente rappresenta l'unico artefatto tassativamente indispensabile e obbligatorio all'interno di un progetto software. Tutti gli altri modelli (DCD e Diagrammi di Interazione) sono strumenti intermedi a supporto dello sviluppo.

### Corrispondenza tra Modelli e Codice

1. **Dal DCD (Modello Statico) alle definizioni delle Classi:** Il Diagramma delle Classi di Progetto esplicita lo scheletro strutturale (nomi, visibilità, variabili d'istanza, tipi di ritorno, costruttori), ma non fornisce alcuna indicazione sulla logica algoritmica interna.
2. **Dai Diagrammi di Interazione (Modello Dinamico) ai Metodi:** I diagrammi di comunicazione o sequenza guidano la scrittura del corpo dei metodi. La traduzione è parzialmente meccanica, sebbene richieda l'aggiunta dei dettagli sintattici del linguaggio di programmazione.

```java
// Esempi tipici di traduzione delle molteplicità e delle mappe risultanti dal DCD
private List<SalesLineItem> lineItems = new ArrayList<>(); // o LinkedList
private Map<ItemID, ProductDescription> description = new HashMap<>();

// Operazione di assegnamento (il costrutto "this." è facoltativo in assenza di shadowing)
this.description = desc;
```

### Ordine di Implementazione delle Classi
* **Approccio Semplificato:** Procedere partendo dalle classi più indipendenti (prive di accoppiamento uscente) verso quelle dipendenti.
* **Approccio Guidato dai Test (TDD - Test-Driven Development):** Procedere partendo dalle classi radice. Prevede la stesura rigorosa dei test d'accettazione prima ancora della scrittura del codice di business.

---

## Retrospettiva sull'Iterazione 1

> **Nota metodologica (Scrum):** All'interno del framework Scrum, la fase di chiusura di un ciclo (Sprint) prevede due eventi distinti:
> * **Sprint Review:** Momento di ispezione del prodotto software insieme al cliente e agli stakeholder.
> * **Sprint Retrospective:** Momento di ispezione interno al solo team di sviluppo per analizzare i processi e migliorare i flussi di lavoro.

> **Nota della lezione:** Dal minuto 57:01 (registrazione originale) / 48:30 (versione accelerata) al minuto 56:40 (versione accelerata) viene fornita un'ottima spiegazione riassuntiva che esamina i collegamenti e la coerenza tra:
> * Requisiti ed Analisi (Mappatura dei bisogni).
> * Analisi e Progettazione (Mappatura dei concetti logici).
> * Progettazione e Programmazione (Mappatura nel codice sorgente).
> 
> Segue una discussione aperta sull'effettiva sostenibilità e sul valore aggiunto del lavorare seguendo questo rigido approccio formale.

---

## Pattern GRASP: Obiettivi di Secondo Livello

I quattro pilastri fondamentali della qualità del software sono:
1. **Comprensibilità:** Facilità di interpretazione del codice in isolamento.
2. **Modificabilità:** Contenimento dell'impatto dei cambiamenti futuri.
3. **Riuso:** Capacità di reimpiegare i moduli in contesti differenti.
4. **Semplicità:** Rimozione delle sovrastrutture non necessarie.

> Questi obiettivi di alto livello sono costantemente promossi e garantiti dall'applicazione congiunta di **Low Coupling** (Basso Accoppiamento) e **High Cohesion** (Alta Coesione), i quali trovano il loro supporto metodologico nell'intero catalogo dei pattern GRASP.
