# 7 - Modellazione delle informazioni di Dominio - 16/03/2026

> **Nota della lezione:** Trattati inizialmente esempi pratici relativi agli elenchi di categorie di classi concettuali.

---

## Identificazione delle Classi Candidate

La selezione e la stesura delle classi concettuali deve sempre avviarsi partendo dai concetti cardine e più rilevanti dell'intero dominio.

> [!IMPORTANT]
> **La Classe Radice:** All'interno di un modello esiste stabilmente una classe concettuale principale preposta a rappresentare l'interezza del dominio o del sistema analizzato.
> * Nei sistemi strutturati in architettura **Client-Server**, è prassi introdurre una classe specifica atta a rappresentare il punto di accesso fisico o virtuale al sistema software (es. un *Terminale*).

> [!WARNING]
> **Modellazione dei Flussi e degli Attori:**
> * Gli *Attori* descritti nei casi d'uso possono essere inseriti nel modello di dominio, ma non si tratta di un obbligo sistematico.
> * **Errore da evitare:** Non devono mai essere create classi concettuali che tentano di rappresentare interi casi d'uso o singoli passi/step sequenziali degli scenari utente.

---

## Approcci alla Modellazione

La strutturazione del dominio può seguire differenti metodologie operative:
* **Approccio basato sui documenti:** Analisi formale e strutturata della documentazione esistente.
* **Agile Modeling:** Approccio snello e iterativo focalizzato sulla discussione e sulla comprensione immediata rispetto alla rigida documentazione.

---

## Criteri di Nomenclatura e Glossario

La scelta dei nomi attribuiti alle entità rappresenta un fattore critico per la chiarezza del progetto.

* **Estrazione testuale:** I termini devono essere mutuati direttamente dai testi dei requisiti o dal dominio reale, evitando l'introduzione di vocaboli inventati ex novo dall'analista.
* **Verifica concettuale:** Per ogni elemento introdotto, è necessario saper rispondere con precisione alla domanda: *«Che cosa rappresenta concretamente questo elemento?»*. Se non si trova una risposta chiara, l'elemento è concettualmente errato o necessita di una ridenominazione.
* **Formalizzazione:** Ogni definizione validata deve essere tempestivamente documentata all'interno del **Glossario**.

> [!TIP]
> **Convenzioni di stile:**
> * Utilizzare esclusivamente nomi espressi al **singolare**.
> * Adottare la lingua **italiana** per mantenere la coerenza espressiva con il dominio di riferimento.

---

## La Classe Descrizione (Description Class)

Una **Classe Descrizione** è un'entità che racchiude informazioni destinate a descrivere un'altra risorsa o oggetto del dominio.

Viene introdotta per perseguire due obiettivi principali:
1. Ridurre le ridondanze e le ripetizioni superflue di informazioni nel sistema.
2. Scongiurare le anomalie tipiche di gestione dei dati (fasi di inserimento, aggiornamento e cancellazione).

---

## Identificazione delle Associazioni

Un'associazione specifica una relazione logica tra classi concettuali. Deve essere introdotta esclusivamente quando emerge la necessità reale di memorizzare un collegamento tra due oggetti per un intervallo di tempo significativo.

> [!WARNING]
> **Rischio di Over-modeling:** È fondamentale evitare la proliferazione incontrollata di associazioni. La stabilità del modello risiede nella qualità delle classi concettuali; le relazioni devono limitarsi a quelle strutturali ed essenziali, tralasciando i collegamenti marginali.

### Sintassi e Convenzioni delle Associazioni
* **Pattern del nome:** `[Nome Classe] + verbo/locuzione verbale + [Nome Classe]` (es. *Cliente -> Effettua -> Ordine*).
* **Stile:** Si utilizzano verbi di forma finita, adottando la convenzione con l'iniziale Maiuscola.
* **Direzione di lettura:** Di norma si intende da sinistra a destra e dall'alto verso il basso, oppure viene esplicitata graficamente mediante una freccia di direzione.
* **Ruoli (Association Ends):** Rappresentano le estremità dell'associazione e descrivono la funzione specifica assunta da una classe all'interno di quella determinata relazione.

---

## La Molteplicità

La molteplicità esprime il numero di istanze di una classe che possono legarsi a una singola istanza della classe contrapposta.

| Notazione | Significato |
| :--- | :--- |
| `*` | Zero o più istanze (corrisponde a `0..*`) |
| `1..*` | Almeno una o più istanze |
| `1..x` | Da un minimo di 1 a un massimo di *x* istanze |
| `x` | Esattamente *x* istanze |
| `a, b, c` | Esattamente e solo i valori discreti indicati (es. 2 o 4) |

> [!IMPORTANT]
> **Algoritmo di verifica:** Per determinare correttamente i valori ai due capi della relazione, occorre porsi la domanda in modo simmetrico: *«Data una singola istanza della Classe A (nel suo specifico Ruolo), quante istanze della Classe B possono associarsi ad essa?»*.
> * I vincoli di molteplicità **minima** sono generalmente considerati trascurabili in questa fase di analisi.
> * I vincoli di molteplicità **massima** costituiscono invece l'informazione strutturale più importante.
> * Le associazioni di tipo **1 a 1** (monogame pure) risultano estremamente rare all'interno di un corretto modello di dominio.
