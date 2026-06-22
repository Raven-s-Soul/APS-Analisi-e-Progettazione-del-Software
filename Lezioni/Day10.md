# 10 - Operazioni di sistema e diagrammi di sequenza di sistema & Contratti delle operazioni di sistema - 24/03/2026

## Operazioni di Sistema e Diagrammi di Sequenza di Sistema (SSD)

L'analisi delle funzioni di sistema si traduce nella modellazione delle operazioni attraverso i **Diagrammi di Sequenza di Sistema (SSD)**. Un SSD è un artefatto basato sulla notazione dei diagrammi di sequenza UML che illustra una specifica sequenza di interazioni per un singolo scenario di un caso d'uso.

### Caratteristiche del Modello
* **Sistema come Scatola Nera (`:System`):** Il sistema viene considerato un'entità unica priva di dettagli implementativi interni.
* **Operazioni di Sistema:** Gli input diretti verso il sistema inviati dagli attori.
* **Risposte del Sistema:** I messaggi di ritorno graficamente rappresentati con linee tratteggiate.
* **Evento:** Interazione che si consuma istantaneamente nel tempo.
* **Operazione:** L'esecuzione di una trasformazione di stato o di un'interrogazione interna attivata dall'evento.

> [!TIP]
> ### Regole Pratiche e Linee Guida per gli SSD
> * **Elementi base:** Posizionare l'istanza dell'attore primario (`:Attore`) e il sistema (`:System`), tracciando le rispettive linee di vita verticali tratteggiate.
> * **Cosa inserire:** Mappare passo-passo la lettura del caso d'uso inserendo esclusivamente le interazioni esterne. Non devono essere mostrate dichiarazioni di variabili o azioni interne compiute autonomamente dal sistema.
> * **Cicli (Loop):** Raggruppare i blocchi ripetitivi all'interno di un rettangolo di frame (esplicitando l'eventuale condizione o evento di terminazione).
> * **Nomenclatura orientata all'intento:** Scegliere nomi descrittivi espliciti che denotino l'azione del dominio (es. *inizia...*, *inserisci...*, *aggiungi...*, *seleziona...*, *termina...*). 
>   * *No:* `inserisciArticolo()` 
>   * *Sì:* `aggiungiArticoloAllaVendita()`
> * **Formato dei Parametri:** Gli argomenti passati nelle operazioni devono essere rigorosamente **valori semplici o primitivi**, mai riferimenti a oggetti software.
> * **Formato delle Risposte:** I messaggi di ritorno non espongono parametri formali, ma mostrano direttamente i dati risultanti (es. *"descrizione, totale"* oppure *"totale con tasse"*).

---

## Contratti delle Operazioni di Sistema

I contratti operativi costituiscono l'anello di congiunzione dell'analisi del comportamento, unendo formalmente il mondo statico del **Modello di Dominio** con quello dinamico espresso dai **Diagrammi di Sequenza di Sistema (SSD)**.

### Struttura Standard di un Contratto
* **Nome:** `Contratto [Identificativo]: [Nome Funzione]`
* **Operazione:** `funzione(parametri con relativo tipo)`
* **Riferimenti:** Identificazione del Caso d'Uso di origine.
* **Pre-condizioni:** Stato del sistema richiesto prima dell'esecuzione.
* **Post-condizioni:** Cambiamenti avvenuti a seguito dell'operazione.

> [!IMPORTANT]
> ### Le Pre-condizioni
> Esplicitano lo stato o le assunzioni sul sistema che devono essere tassativamente vere prima dell'esecuzione dell'operazione. Devono citare esclusivamente oggetti concettuali e relazioni che sono già noti al sistema all'interno di quello specifico scenario del caso d'uso.

> [!IMPORTANT]
> ### Le Post-condizioni (La sezione più critica)
> Descrivono i cambiamenti di stato avvenuti nel sistema a seguito dell'operazione. Poiché rappresentano effetti consolidati, vanno **sempre scritte al tempo passato**. 
> 
> Si limitano rigorosamente a tre tipologie di variazioni di stato:
> 1. **Creazione o eliminazione di un oggetto:** *"È stata creata un'istanza x di X."*
> 2. **Formazione o rottura di un collegamento (Link):** *"È stato formato un collegamento tra x e y."*
> 3. **Modifica del valore di un attributo:** *"L'attributo x dell'oggetto Y è diventato uguale a z."*

> [!NOTE]
> Nel caso di operazioni destinate alla sola consultazione o ricerca, si formula una proto-scelta logica basata sulle restrizioni del tipo *"in base al parametro X"*.

> [!TIP]
> **Il concetto di Conoscenza:** Ragionare su un contratto significa ragionare in termini di *conoscenza di sistema*. Chiedersi sempre: *«Che cosa sa il sistema di ciò che esiste nel dominio?»*. Ad esempio, asserire che *"è stata creata un'istanza X"* significa formalmente che il sistema ha appreso ed esteso la propria conoscenza logica nei confronti di quell'entità.
