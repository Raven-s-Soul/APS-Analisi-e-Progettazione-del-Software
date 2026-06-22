# 6 - Modellazione delle informazioni di Dominio - 12/03/2026

> [!IMPORTANT]
> **Regola d'oro della Modellazione di Dominio:** In questa fase **non si parla mai di software**. L'obiettivo è analizzare esclusivamente le tipologie di informazioni presenti nel dominio reale e non i singoli dati specifici. Il processo si basa su uno sviluppo *incrementale* e sul *feedback* continuo.

> Un modello di dominio può essere formalizzato in UML attraverso un **diagramma delle classi**, con la tassativa eccezione di **omettere le operazioni** (i metodi del software).

---

## Elementi Costitutivi del Modello

* **Classe Concettuale:** Rappresenta un'astrazione che raggruppa un insieme di elementi, oggetti o concetti del mondo reale tra loro simili.
* **Associazione:** Esprime una relazione logica o strutturale che intercorre tra le diverse classi concettuali.
* **Attributo:** Rappresenta una proprietà o una caratteristica informativa intrinseca di una classe.

---

## Classificazione delle Informazioni

Nel dominio si individuano tre tipi di informazioni, ma non tutte vanno modellate:
1. **Informazioni Persistenti:** Dati strutturali che richiedono una memorizzazione stabile a lungo termine (es. all'interno di una base di dati). **Vanno modellate.**
2. **Informazioni Transienti:** Dati temporanei, necessari esclusivamente per supportare i singoli step intermedi all'interno dei casi d'uso. **Vanno modellate.**
3. **Informazioni Locali:** Dettagli minuti e circoscritti che non apportano valore strutturale. **Non vanno inserite né modellate.**

---

## Obiettivi del Modello di Dominio

L'adozione di questo modello risponde a esigenze sia di analisi che di progettazione:

* **In fase di Analisi:** Permette di comprendere a fondo il dominio e concorre alla definizione di un linguaggio comune e condiviso (Glossario).
* **In fase di Progettazione:** Funge da ispirazione diretta per la strutturazione dei futuri strati del software, garantendo l'organizzazione architetturale.

> [!NOTE]
> **Salto Rappresentazionale (Representational Gap):** Rappresenta la distanza concettuale tra il modello mentale del problema reale (come il progettista vede il dominio) e la sua effettiva implementazione nel codice sorgente. Una buona modellazione di dominio mira a ridurre questo scarto al minimo (sebbene non possa mai essere nullo).

---

## Anatomia delle Classi Concettuali

Una classe concettuale è definita da tre componenti fondamentali:
* **Simbolo:** La rappresentazione visiva o il nome della classe (espressa nel Modello di Dominio).
* **Intensione:** La definizione semantica e il significato del concetto (documentata nel Glossario).
* **Estensione:** L'insieme pratico di tutti gli esempi reali e concreti che appartengono a quella classe (fondamentale per validare i ragionamenti e risolvere i dubbi).

### Distinzioni Chiave in UML
La notazione grafica UML prevede regole precise per distinguere la struttura astratta dalle istanze concrete:
* Nei diagrammi, la presenza del carattere `:` identifica univocamente un **oggetto** (istanza), mentre l'assegnazione dei valori agli attributi avviene tramite l'operatore `=`.

> [!IMPORTANT]
> Occorre non confondere i concetti strutturali con le loro istanze:
> * Classe $\neq$ Oggetto (ma sono strettamente correlati)
> * Associazione $\neq$ Collegamento/Link (ma sono strettamente correlati)
> * Attributo $\neq$ Valore (ma sono strettamente correlati)

---

## Metodologia di Creazione del Modello

Il processo operativo si articola in tre passi sequenziali:
1. Individuare le astrazioni significative e di reale interesse nel dominio.
2. Scegliere come rappresentarle graficamente.
3. Disegnare il diagramma.

> [!WARNING]
> **Paralisi da Analisi:** Durante l'identificazione delle classi candidate, è preferibile includere inizialmente più classi piuttosto che ometterne di critiche. L'obiettivo finale deve comunque rimanere la stesura di un elenco **utile** e concreto.

> [!CAUTION]
> Prestare estrema cautela nei confronti di classi modellate come *Singleton*, classi totalmente prive di attributi o classi che espongono esclusivamente un comportamento: spesso indicano un'intrusione precoce di concetti software all'interno del dominio puro.

### Strategie per l'Individuazione delle Classi
Per estrarre le classi concettuali si utilizzano tre approcci complementari:
* **Uso dei Pattern di Analisi:** Sfruttare soluzioni standard preesistenti per problemi di modellazione ricorrenti, evitando di reinventare soluzioni da zero.
* **Analisi Linguistica (Nomi e Locuzioni Nominali):** Identificare i sostantivi presenti nelle descrizioni e nei casi d'uso. È una tecnica semplice ma intrinsecamente limitata e povera se usata da sola.
* **Uso di Elenchi di Categorie Concettuali:** Verificare il dominio confrontandolo con una lista di categorie standard.

### Categorie di Classi Concettuali di Riferimento

| Categoria di classe concettuale |
| :--- |
| Descrizione di oggetti |
| Cataloghi |
| Contenitori di informazioni |
| Oggetti in contenitori |
| Altri sistemi esterni che elaborano dati |
| Registro di questioni finanziarie, di lavoro, contrattuali e legali |
| Strumenti finanziari |
| Piani, manuali, documenti |
| Transazioni commerciali |
| Elementi / righe di dettaglio di transazioni |
| Prodotti o servizi correlati a transazioni e/o ai loro elementi |
| Luoghi in cui è registrata la transazione |
| Ruoli di persone o organizzazioni correlati alle transazioni (attori) |
| Luogo fisico della transazione o luogo del servizio |
| Eventi significativi (spesso associati a vincoli di tempo o luogo da ricordare) |
| Oggetti fisici |
