# 18 - GRASP: Progettazione di oggetti con responsabilità & Esempi di progettazione a oggetti con i pattern GRASP - 28/04/2026

> [!TIP]
> ### Domande Guida per l'Assegnazione delle Responsabilità
> 
> * *Qual è la responsabilità specifica da assegnare?*
> * *A quale oggetto conviene affidarla? (Valutando se scegliere tra quelli già individuati o se sia necessario introdurne uno nuovo).*
> * *In che modo l'oggetto può adempiere a questo compito? Può completarlo autonomamente o richiede il supporto di collaboratori esterni? (Identificando così le collaborazioni).*

> **Nota del corso:** Analizzati a lezione gli esempi pratici basati sul gioco del Monopoly per affrontare il problema di progettazione legato alla creazione degli oggetti di tipo *Square* (Casella).

---

## I Pattern GRASP Fondamentali

### 1. Pattern Creator
* **Problema:** Quale classe ha la responsabilità di creare una nuova istanza di un oggetto di tipo `A`?
* **Soluzione:** Assegnare alla classe `B` la responsabilità di istanziare `A` se si verifica almeno una delle seguenti condizioni (in ordine di preferenza):
  * `B` contiene direttamente o è composto da oggetti `A` *(criterio preferenziale)*.
  * `B` registra o traccia le istanze di `A`.
  * `B` utilizza in modo stretto e continuativo l'oggetto `A`.
  * `B` possiede tutti i dati di inizializzazione necessari da passare ad `A` al momento della sua nascita.

> **Rappresentazione UML:** Nei diagrammi è possibile esplicitare l'uso del pattern tramite una nota testuale ancorata, tracciando le frecce direzionali che collegano la responsabilità alla classe creatrice e al prodotto. Spesso questa relazione introduce un legame di composizione/molteplicità strutturato tramite liste o collezioni.

> [!NOTE]
> Ragionamento analogo si applica per definire le responsabilità legate alla ricerca delle informazioni all'interno del sistema.

### 2. Pattern Information Expert
* **Problema:** Qual è il principio fondamentale per distribuire le responsabilità elementari all'interno del software?
* **Soluzione:** Assegnare il compito alla classe che detiene le informazioni necessarie per poterlo portare a termine.

> [!NOTE]
> Nella traduzione pratica, le associazioni strutturate come **composizioni** si traducono quasi sempre in collezioni di dati di tipo lista o mappa.

> **Principio di Modularità:** Cardine dell'ingegneria del software che prevede la decomposizione del sistema in moduli indipendenti, autocontenuti, facilmente comprensibili e semplici da modificare.

---

## Valutazione del Design: Accoppiamento e Coesione

### L'Accoppiamento (Coupling)
Rappresenta la misura di quanto un elemento software sia strettamente connesso ad altri componenti, basandosi su quanti altri moduli esso conosca direttamente (riferimenti) o da quanti dipenda logicamente.

### 3. Pattern Low Coupling
* **Problema:** Come limitare l'impatto dei cambiamenti futuri e garantire l'indipendenza dei componenti?
* **Soluzione:** Assegnare le responsabilità in modo tale che l'accoppiamento non necessario tra le classi rimanga il più basso possibile.
  * *Uso pratico:* Questo schema funge da principio cardine per valutare e confrontare criticamente le diverse alternative di progettazione.

> Un livello di accoppiamento ridotto al minimo rappresenta l'indicatore di un software di migliore qualità.

---

### La Coesione (Cohesion)
Indica il grado di correlazione e focalizzazione delle responsabilità o delle operazioni interne affidate a un singolo elemento software. Rappresenta una misura quantitativa e qualitativa del carico di lavoro svolto da una classe.

> [!TIP]
> **Benefici dell'Alta Coesione:** Distribuire i compiti per mantenere una coesione elevata permette di comprendere i componenti in isolamento, riduce la propagazione delle modifiche e incentiva fortemente il riuso del codice.

### 4. Pattern High Cohesion
* **Problema:** Come mantenere gli oggetti focalizzati sul proprio scopo, comprensibili e gestibili nel tempo, supportando parallelamente il principio di `Low Coupling`?
* **Soluzione:** Allocare le responsabilità facendo in modo che la coesione interna di ogni classe rimanga elevata. Funge da metro di paragone per scartare soluzioni progettuali troppo frammentate o, al contrario, centralizzate.

---

### 5. Pattern Controller
* **Problema:** Qual è il primo oggetto software, posizionato immediatamente oltre lo strato dell'interfaccia grafica (UI), deputato a ricevere e coordinare un'operazione di sistema?
* **Soluzione:** Affidare la gestione a un oggetto che sposi una delle due seguenti strategie architetturali:
  * **Facade Controller:** Un unico oggetto deputato a rappresentare l'intero sistema nel suo complesso o l'intero pacchetto software *(strategia preferita e adottata all'interno del corso)*.
  * **Session Controller:** Un oggetto creato per rappresentare una specifica istanza del caso d'uso all'interno del quale si consuma l'operazione.

---

## Realizzazione dei Casi d'Uso (Use Case Realization)

La **Realizzazione di un Caso d'Uso** definisce l'esatta traduzione dinamica dei requisiti, descrivendo come un caso d'uso venga concretamente implementato a livello software mediante la collaborazione strategica tra oggetti.

La sua documentazione richiede:
* La stesura di molteplici **Diagrammi di Interazione** (per catturare il comportamento dinamico).
* La produzione di un unico **Diagramma delle Classi di Progetto (DCD)** complessivo (per la struttura statica).

> **Caso d'uso di avviamento (Startup):** Identifica lo scenario iniziale in cui l'applicazione viene eseguita e le classi di base vengono istanziate per la prima volta. In questa fase non si considera ancora la persistenza stanziale dei dati.

> **Nota metodologica:** Nei diagrammi dinamici è fondamentale mostrare sempre in modo esplicito la nascita dei nuovi oggetti software attraverso i messaggi di creazione.
