# 25 - Esempi di progettazione a oggetti con i pattern GRASP & Trasformare i progetti in codice & Sviluppo guidato dai test e Refactoring - 26/05/2026

> **Nota della lezione:** Analizzato l'esempio pratico basato sul gioco del Monopoly. Il codice esaminato contiene intenzionalmente alcuni errori di progettazione, la cui risoluzione analitica sarà l'obiettivo centrale delle attività dell'Iterazione 2.

---

## Sviluppo Guidato dai Test e Refactoring

### Test-Driven Development (TDD)
Lo sviluppo guidato dai test si configura come una *best practice* d'eccellenza in cui l'implementazione del software e la stesura dei test non sono considerate attività separate o asincrone, ma un unico processo strettamente integrato.

* **Approccio Test-First:** Il codice di test viene tassativamente scritto *prima* del codice di business preposto a soddisfare la verifica. 
* **Opposizione al Test-Last:** Si contrappone nettamente alla rischiosa abitudine del *test-last development* (ironicamente definita a lezione come la filosofia del *"giusto per questa volta salto il test, lo scrivo dopo"*).
* **Focus sul Design:** Il TDD non deve essere frainteso come una mera tecnica di testing, bensì come una vera e propria metodologia di supporto alla progettazione e allo sviluppo strutturato del codice.
* **Ambito operativo:** Trova la sua applicazione d'elezione a livello di **test unitario (Unit Testing)**.

> [!NOTE]
> ### Tipologie di Test nel Ciclo del Software
> * **Test Unitari:** Verificano che una singola unità isolata di codice (una specifica classe o un singolo metodo) esibisca esattamente il comportamento logico atteso.
> * **Test di Integrazione:** Verificano la corretta collaborazione, comunicazione e interazione tra più moduli o componenti distinti del sistema.
> * **Test End-to-End (E2E):** Verificano l'interezza del flusso funzionale dell'applicazione, simulando l'esperienza utente dalla UI fino alla persistenza fisica dei dati.
> * **Test di Accettazione:** Verificano a livello macroscopico che il sistema soddisfi pienamente i requisiti formali e i criteri di business concordati con il cliente.

> [!TIP]
> ### Anatomia di un Metodo di Test (Le Quattro Fasi)
> 1. **Setup (Preparazione):** Configurazione preliminare dell'ambiente e istanziazione di tutti gli oggetti e i dati necessari all'esecuzione del test.
> 2. **Execute (Esecuzione):** Invocazione diretta dell'operazione o del metodo specifico sotto analisi.
> 3. **Verify (Verifica):** Controllo dei risultati ottenuti tramite asserzioni esplicite (*assert*) per validare la correttezza dello stato o del valore di ritorno.
> 4. **Teardown (Rilascio):** Pulizia finale dell'ambiente e rilascio sistematico delle risorse allocate (es. chiusura di file o connessioni a database).

---

### Il Ciclo del TDD (Red-Green-Refactor)

Il processo di sviluppo guidato dai test si sviluppa seguendo un ciclo iterativo continuo e rigoroso suddiviso in tre macro-fasi:

1. **RED:** Scrittura di un test unitario focalizzato su una nuova funzionalità che, inizialmente, deve inevitabilmente fallire (poiché il codice di business non esiste ancora). *Nota: in questa fase si può includere preliminarmente anche la stesura di un test di accettazione volto al fallimento.*
2. **GREEN:** Scrittura del codice di business minimo, più semplice e strettamente necessario a far passare il test precedentemente fallito con successo.
3. **REFACTOR:** Ristrutturazione e ottimizzazione del codice appena scritto per elevarne la qualità formale, eliminando le imperfezioni senza alterarne il comportamento esterno osservabile.



> **Nota sull'organizzazione dei test:** Argomento trattato molto brevemente a lezione ed omesso nei suoi dettagli descrittivi.

---

## Il Refactoring

Il refactoring rappresenta una *best practice* sistematica volta a preparare e predisporre il codice sorgente preesistente all'introduzione fluida e sicura di nuove funzionalità.

* Si configura come un metodo di intervento altamente strutturato, disciplinato e controllato.
* Viene impiegato per riscalare, riscrivere o ristrutturare porzioni di codice esistente.
* **Vincolo Assoluto:** L'operazione deve essere eseguita modificando esclusivamente l'architettura interna del codice, **senza alterare in alcun modo il comportamento esterno** osservabile del sistema.

> [!WARNING]
> La finalità principale del refactoring risiede nella sistematica rimozione dei difetti strutturali e delle "brutture" stilistiche del codice (*code smells*), concentrandosi in particolare sulla cancellazione del codice duplicato e sull'innalzamento della chiarezza e della leggibilità.

### Tecniche e Pattern di Refactoring Comuni

* **Rename (Ridenominazione):** Modificare il nome di variabili, metodi o classi per riflettere in modo accurato e trasparente il loro reale intento all'interno del dominio.
* **Extract Method (Estrazione di Metodo):** Scomporre un blocco di codice eccessivamente lungo o complesso all'interno di un nuovo metodo separato dotato di un nome fortemente descrittivo, semplificando la funzione d'origine.
* **Extract Class (Estrazione di Classe):** Scindere una classe troppo densa di responsabilità (prossima a diventare un *Blob*) delegando parte dei suoi compiti a una nuova entità autonoma (es. introducendo un *Ledger* o un *Controller* di sessione).
* **Introduce Explaining Variable (Variabile Esplicativa):** Assegnare il risultato di una sotto-espressione complessa o di una fitta condizione booleana a una variabile locale dal nome chiarificatore.
* **Extract Constant (Estrazione di Costante):** Sostituire i valori letterali fissi (*magic numbers* o stringhe hardcoded nel codice) con costanti nominate e centralizzate.
* **Move Method (Spostamento di Metodo):** Trasferire un metodo da una classe a un'altra quando si constata che quest'ultima utilizza o detiene la quasi totalità delle informazioni collegate a quell'operazione.
* **Replace Constructor Call with Factory Method:** Sostituire l'invocazione rigida e diretta di un costruttore mediante l'adozione di un metodo fabbrica, flessibilizzando i meccanismi di istanziazione degli oggetti.
