# 8 - Modellazione delle informazioni di Dominio - 17/03/2026

> **Nota della lezione:** Trattati a lezione il modello di dominio iniziale, esempi pratici su oggetti di dominio e relativi collegamenti (link), cenni storici ed esempi conclusivi.

---

## Tipologie Avanzate di Associazione

Durante la modellazione possono emergere relazioni strutturali più complesse rispetto alle associazioni standard:

* **Associazioni Multiple:** Presenza di due o più associazioni distinte che collegano le medesime classi concettuali, ciascuna con un significato logico differente.
* **Nomi di Ruolo (Role Names):** Etichette esplicite poste alle estremità di un'associazione per specificare la funzione precisa assunta da un oggetto nei confronti dell'altro.
* **Associazione Riflessiva (o Ricorsiva):** Una relazione logica che lega una classe concettuale a se stessa.
* **Associazioni Derivate:** Relazioni non primitive che possono essere dedotte o calcolate mediante la composizione di altre associazioni già esistenti nel diagramma. Vengono graficamente contrassegnate anteponendo il simbolo `/` al nome della relazione.

> [!TIP]
> **Criterio di inserimento:** Non occorre mostrare tutte le possibili associazioni derivate geometricamente combinabili. Vanno inserite esclusivamente quelle che favoriscono in modo tangibile la comprensione del dominio da parte dei lettori.

> **Regola della memoria:** A volte è utile rappresentare elementi o relazioni che non richiedono di essere permanentemente registrati dal sistema, al solo scopo di migliorare la comprensione del contesto reale. La domanda guida dell'analista deve essere sempre: *«È strutturalmente necessario ricordare questa informazione?»*.

---

## La Composizione (Aggregazione)

> [!NOTE]
> Nel contesto e nelle finalità di questo corso, i concetti di **Aggregazione** e **Composizione** tendono a sovrapporsi e a essere considerati equivalenti.

La composizione descrive una forma di associazione estremamente forte ed evidente (relazione "tutto-parte"), in cui un oggetto composto è strutturalmente costituito da uno o più oggetti parte (un esempio tipico è il legame con le *Classi Descrizione*).

Le sue proprietà fondamentali sono:
1. La relazione di inclusione e dipendenza è ovvia e manifesta nel mondo reale.
2. **Vincolo del Ciclo di Vita:** La durata della vita della parte è strettamente subordinata e vincolata alla vita del composto (se si distrugge il composto, cessano di esistere anche le parti).
3. **Propagazione logica:** Le proprietà intrinseche del composto si riflettono e si propagano sulle singole parti.
4. Di conseguenza, alcune operazioni macroscopiche applicate all'oggetto composto si estendono automaticamente a tutte le parti che lo costituiscono.

---

## Gli Attributi nel Modello di Dominio

Un attributo rappresenta una proprietà informativa o un valore logico caratteristico degli oggetti appartenenti a una determinata classe. Di norma, in questa fase di modellazione del dominio, i tipi di dato specifici **non vengono mostrati**.

### Sintassi e Visibilità
* `-` indica un attributo con visibilità *Privata*.
* `+` indica un attributo con visibilità *Pubblica*.
* Gli attributi possono prevedere un valore predefinito o essere contrassegnati come opzionali.
* **Molteplicità multipla:** Non è ammessa per gli attributi all'interno di un corretto modello di dominio.

> [!IMPORTANT]
> **I Tipi Ammessi:** Gli attributi devono limitarsi esclusivamente a tipi di dato semplici o primitivi (es. stringhe, numeri, booleani). 

> [!CAUTION]
> **Divieto di Chiavi Esterne (No Foreign Keys):** È un grave errore di modellazione utilizzare un attributo per rappresentare o simulare la relazione tra due classi (es. inserire un ID all'interno di una classe per puntare a un'altra). I collegamenti tra le classi concettuali devono essere espressi **unicamente e rigorosamente** attraverso le linee grafiche delle associazioni.

### Strutture Speciali degli Attributi

* **Classe Tipo di Dato (Data Type Class):** Classi di supporto ("serie B") che vengono introdotte per modellare proprietà non elementari o tipi di dato complessi che non possono essere ridotti a semplici primitivi.
* **Attributi Derivati:** Proprietà il cui valore non è nativo ma può essere calcolato a partire da altri dati già presenti nel modello. Vengono identificati anteponendo il simbolo `/` prima del nome dell'attributo.
