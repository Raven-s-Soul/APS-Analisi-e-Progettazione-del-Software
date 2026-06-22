# 26 - Iterazione 2: Altri pattern & Rapido aggiornamento dell'analisi (e del progetto) & Ulteriore modellazione di dominio - 28/05/2026

> **Recapitolo del Flusso Iterativo:**
> * **Iterazione 0:** Interamente dedicata all'avvio dell'analisi dei requisiti.
> * **Iterazione 1:** Acquisizione delle capacità fondamentali dell'OOA/D e transizione dal progetto strutturato al codice software.
> * **Iterazione 2:** Introduzione ad altre capacità fondamentali dell'OOA/D, studio sistematico dei design pattern e della loro applicazione nell'OOD, ulteriore estensione e applicazione pratica di UML.
> * *(Nota: Gli argomenti extra residui verranno trattati successivamente nell'Iterazione 3).*

### Il Sistema Esterno
Rappresenta un sistema o un sottosistema completamente autonomo che offre servizi di reale interesse per il software sotto analisi e con il quale il Sistema in Discussione (SuD) ha l'obbligo di interagire.
* *Esempio tipico:* L'integrazione o l'interazione con **API esterne** (analizzati a lezione i casi di studio concreti applicati sia al POS che al gioco del Monopoly).

---

## La Generalizzazione in UML

La **Generalizzazione** rappresenta un processo di astrazione volto a identificare, estrarre e centralizzare le caratteristiche comuni individuate tra differenti concetti del dominio reale.



* Permette di strutturare classificazioni tassonomiche ben definite (gerarchie di classi o gerarchie di generalizzazione-specializzazione).
* Stabilisce una relazione formale tra una **Superclasse** (il concetto più esteso e generale) e una o più **Sottoclassi** (i concetti maggiormente specializzati).
* *Notazione grafica:* Una linea continua contrassegnata da una punta a forma di **triangolo vuoto** rivolta verso la superclasse.

> [!NOTE]
> ### I Tre Aspetti Fondamentali della Relazione
> 1. **Definizioni Intensionali delle Classi:** L'insieme delle regole intensionali e delle proprietà logiche che descrivono le caratteristiche astratte di una categoria.
> 2. **Estensioni delle Classi:** L'insieme pratico di tutte le istanze ed esempi concreti del mondo reale che appartengono a quella specifica classe.
> 3. **Proprietà Strutturali delle Classi:** La configurazione di attributi e associazioni ereditate lungo l'albero gerarchico.

### Le Regole di Convalida della Gerarchia

> [!TIP]
> ### 1. La Regola dell' "Is-A" (È un)
> Tutti i membri appartenenti all'estensione di una determinata sottoclasse devono tassativamente configurarsi anche come membri legittimi dell'estensione della rispettiva superclasse.
> * *Test linguistico di verifica:* La sottoclasse supera il controllo se risponde alla frase **«Sottoclasse è un(a) Superclasse»** (es. *Un Cane è un Animale*).

> [!TIP]
> ### 2. La Regola del 100%
> Tutte le caratteristiche strutturali (intese come l'unione di attributi e associazioni) definite nella specifica di una superclasse sono (e devono essere) applicabili al 100% e senza alcuna eccezione a ciascuna delle sue sottoclassi derivate.

---

## Criteri di Strutturazione Tassonomica

### Quando partizionare una classe in Sottoclassi?
L'introduzione e la visualizzazione grafica di una sottoclasse specializzata all'interno del diagramma è considerata una scelta di modellazione valida esclusivamente se risponde ad almeno una delle seguenti motivazioni:
* **Presenza di Proprietà Strutturali Aggiuntive:** La sottoclasse detiene attributi o associazioni aggiuntive di reale interesse che non si applicano alla superclasse o alle altre ramificazioni.
* **Comportamento Diversificato:** Il concetto espresso dalla sottoclasse viene fatto funzionare, viene gestito, reagisce agli stimoli o viene manipolato in modo significativamente diverso rispetto alla superclasse o alle altre sottoclassi, secondo modalità d'interesse per il sistema.
* **Entità Animate Dissimili:** La sottoclasse rappresenta un'entità animata del dominio che si comporta e agisce in modo unico rispetto alla superclasse.

### Quando generalizzare in una Superclasse?
L'estrazione e la definizione di una classe genitore comune è consigliata quando si identificano tratti condivisi tra le potenziali classi candidate:
* Le potenziali sottoclassi concettuali rappresentano variazioni o specializzazioni di un medesimo concetto di base simile.
* Le classi rispettano rigorosamente sia la regola dell'*Is-A* sia la regola del *100%*.
* Tutte le classi analizzate esibiscono una medesima proprietà strutturale (un attributo o un'associazione identica) che può essere vantaggiosamente estratta, fattorizzata ed espressa in modo centralizzato all'interno della superclasse.

---

### Classe Concettuale Astratta (`{abstract}`)

Una classe concettuale $C$ viene formalmente definita **astratta** se ciascun singolo membro appartenente alla classe $C$ è (e deve essere) obbligatoriamente membro di almeno una delle sottoclassi dirette di $C$. Di conseguenza, non possono esistere istanze pure della sola classe astratta.
* *Notazione UML:* Il nome della classe viene scritto in formato *corsivo* oppure viene esplicitata chiaramente la stringa di vincolo **`{abstract}`**.
* *Nota della lezione:* Esaminati a lezione i relativi esempi accademici mediante l'ausilio dei diagrammi degli oggetti.

---

## Modelli di Classificazione degli Oggetti

La classificazione analizza la natura del legame logico e temporale che intercorre tra un'istanza (oggetto) e il suo tipo di riferimento (classe). Lo standard UML prevede diverse opzioni per strutturare la classificazione:

* **Classificazione Singola:** Un oggetto appartiene a una e una sola classe specifica (la foglia più dettagliata dell'albero gerarchico).
* **Classificazione Multipla:** Un oggetto ha la facoltà di appartenere simultaneamente a più classi distinte tra loro.
* **Classificazione Statica:** La classificazione di un oggetto è permanente: il legame con la sua classe di appartenenza non può mai mutare o evolvere nel tempo lungo il suo ciclo di vita.
* **Classificazione Dinamica:** La classificazione dell'oggetto è fluida: l'istanza ha la possibilità di cambiare la propria classe di riferimento nel corso del tempo in risposta agli eventi del sistema.

> [!IMPORTANT]
> **Linea Guida Tassativa del Corso:** All'interno della modellazione di dominio trattata in questo insegnamento, è richiesto di adottare ed applicare rigorosamente ed esclusivamente la combinazione di classificazione **Singola** e **Statica**.
