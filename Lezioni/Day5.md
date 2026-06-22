# 5 - Verso l'analisi a oggetti - 10/03/2026

> **Architettura del software:** Identificazione dei componenti strutturali principali e delle relazioni che costituiscono il sistema.

> [!IMPORTANT]
> ### I Tre Strati Logici Fondamentali (Layering)
> L'architettura tipica si suddivide in livelli con responsabilità distinte:
> 1. **Presentazione (User Interface):** Gestisce l'interazione con l'utente (es. menu, pulsanti, componenti grafiche).
> 2. **Logica Applicativa (Domain/Business Logic):** Contiene le regole di business e il nucleo operativo dell'applicazione.
> 3. **Accesso ai Dati e Servizi Tecnici (Infrastructure):** Gestisce la persistenza e l'interazione con i database (es. esecuzione di comandi SQL) o altri servizi di basso livello.

> La definizione della strategia per lo strato della logica applicativa condiziona l'intero progetto. Si distinguono due approcci principali:
> * Approccio transazionale (Transaction Script)
> * **Domain Model (Modello di Dominio):** L'approccio fulcro di questo corso.

> Context di riferimento: Applicazioni di tipo sia stand-alone sia client-server.

---

## Fondamenti dell'Analisi a Oggetti
L'analisi rappresenta la fase di **investigazione** e comprensione approfondita di un problema e dei suoi requisiti.

* Si concentra esclusivamente sul **"che cosa"** il sistema deve fare.
* Non affronta il "come" (l'implementazione tecnica).
* In questa fase non si ricerca la soluzione architetturale diretta, ma la comprensione del dominio.

### Object-Oriented Analysis (OOA)
L'analisi orientata agli oggetti mappa il problema focalizzandosi su tre pilastri:
1. **Informazioni:** I dati e le entità che il sistema ha il compito di gestire.
2. **Funzioni:** Le operazioni e le attività che l'applicazione dovrà completare.
3. **Comportamento:** La dinamica e gli stati del sistema in risposta agli stimoli esterni.

---

## Progettazione Concettuale vs Modellazione di Dominio

> [!IMPORTANT]
> ### Distinzione dai concetti di Basi di Dati
> Sebbene vi siano forti analogie con la Progettazione Concettuale della Base di Dati (PCBD), la Modellazione di Dominio (MD) in UML segue regole e finalità differenti:
> * **Entità:** Diventano le classi concettuali nel dominio a oggetti.
> * **Relazione:** In UML viene definita ed espressa come **Associazione**.
> * **Cardinalità:** Prende il nome di **Molteplicità**.
> * **ER vs UML:** I diagrammi Entità-Relazione (ER) e i diagrammi delle classi UML sono concettualmente simili ma non interscambiabili; la PCBD serve a strutturare i dati su database, la MD serve a mappare i concetti logici nel software a oggetti.

> Analizzati a lezione i relativi esempi pratici di transizione tra i due modelli.
