# 3 - Studi di caso & Iterazione 0: analisi dei requisiti & Requisiti evolutivi & Casi d'uso - 05/03/2026

> [!NOTE]
> **Casi di studio di riferimento:** Le esercitazioni e gli esempi pratici del corso si baseranno su due sistemi: un **POS (Point of Sale)** e il gioco del **Monopoly**.

---

## Iterazione 0
Rappresenta la fase iniziale del progetto, dedicata all'avvio dell'analisi dei requisiti. Non è un'attività isolata: l'analisi inizia qui ma evolve e prosegue lungo tutte le iterazioni successive.
* **Unified Process (UP):** Corrisponde alla fase di *Ideazione (Inception)*.
* **Scrum:** Corrisponde alla fase di *Envisioning*.

---

## Requisiti Evolutivi
I requisiti rappresentano l'insieme delle necessità, degli obiettivi e degli interessi reali che il sistema software deve soddisfare. L'**analisi dei requisiti** serve precisamente a comprendere a fondo il problema specifico da risolvere.

Si dividono principalmente in due categorie:

### 1. Requisiti Funzionali
* Definiscono i servizi e le funzionalità concrete che il sistema deve offrire ai suoi utilizzatori.
* Specificano le informazioni e i dati che l'applicazione deve memorizzare e gestire.

### 2. Requisiti Non Funzionali (Attributi di Qualità)
* Rappresentano i vincoli e le proprietà qualitative del sistema.
* *Esempi:* Sicurezza, prestazioni, scalabilità, manutenibilità e modificabilità.

---

## Strategie di Elicitazione (Trovare i Requisiti)
L'individuazione e la gestione dei requisiti non avvengono in un'unica soluzione, ma seguono un approccio **iterativo e incrementale** attraverso tecniche quali:
* Workshop dedicati ai requisiti.
* Coinvolgimento diretto e continuo degli utenti finali.
* Scrittura di casi d'uso o storie utente (*user stories*).
* Sessioni di demo pratiche al termine di ogni iterazione rilasciata.

> [!TIP]
> **Domande guida per l'analisi:**
> * *Qual è il fulcro o la parte più interessante del dominio?*
> * *Quali sono le macro-categorie di bisogni e interessi da coprire?*

> [!IMPORTANT]
> ### Il Glossario e il Linguaggio Comune
> Stabilire un canale di comunicazione chiaro tra cliente, analista e team di sviluppo è fondamentale ma complesso. Per superare le ambiguità del linguaggio naturale, è indispensabile redigere un **Glossario** condiviso che definisca univocamente i termini del dominio.

---

## Gestione dei Requisiti nei Framework

### Unified Process (UP)
I requisiti vengono formalizzati attraverso una serie di artefatti specifici:
1. **Modello dei casi d'uso:** Per gli aspetti funzionali.
2. **Specifiche supplementari:** Per i requisiti non funzionali e vincoli.
3. **Glossario:** Termini e definizioni.
4. **Regole di business (Business Rules):** Vincoli normativi o logici del dominio.
5. **Visione (Vision):** Obiettivi di alto livello e motivazioni del progetto.

### Scrum
I requisiti risiedono in modo fluido nel **Product Backlog** (l'elenco delle cose ancora da sviluppare) e vengono tipicamente espressi ad alto livello sotto forma di **Storie Utente (User Stories)**.

---

## Casi d'Uso (Use Cases)
I casi d'uso descrivono il comportamento e il funzionamento del sistema dal punto di vista dell'utente. 
*(Nota: Il corso si focalizzerà sulla parte di **Lettura** dei casi d'uso, mentre la Scrittura non verrà trattata).*

### Elementi Costitutivi: Attori, Scenari e Casi d'Uso
* **Attore:** Qualsiasi entità (persona, organizzazione, software o sistema esterno) dotata di comportamento che interagisce con il sistema. Anche il sistema stesso sotto analisi viene definito **SuD (System under Discussion)**.
* **Scenario:** Una specifica sequenza di interazioni ed azioni tra gli attori e il sistema. Si dividono in scenari di *successo* (l'obiettivo viene raggiunto) e scenari di *fallimento*.
* **Caso d'Uso:** Una collezione di scenari correlati (sia di successo che di fallimento) che descrivono un attore che usa il sistema per raggiungere uno specifico obiettivo.

> [!WARNING]
> I casi d'uso offrono enormi vantaggi in termini di chiarezza, ma presentano il limite di non essere applicabili efficacemente a qualsiasi tipologia di requisito o sistema.

### Classificazione degli Attori

| Tipo di Attore | Descrizione |
| :--- | :--- |
| **Attore Primario** | L'entità che attiva direttamente il SuD per raggiungere un proprio obiettivo logico. |
| **Attore Finale** | Il beneficiario ultimo del raggiungimento dell'obiettivo (a volte coincide con il primario). |
| **Attore di Supporto** | Un sistema o entità esterna che fornisce un servizio o un supporto al SuD per completare il caso d'uso. |
| **Attore Fuori Scena** | Un soggetto che non interagisce direttamente, ma ha un interesse economico o logico nel comportamento del SuD. |

---

## Struttura e Anatomia di un Caso d'Uso

> [!TIP]
> ### Componenti Chiave di un Documento di Caso d'Uso
> 
> * **Preambolo (Metadati iniziali):**
>   * Nome del caso d'uso
>   * Portata (*Scope*) e Livello
>   * Attore primario
>   * Parti interessate e relativi interessi (*Stakeholders*)
>   * Pre-condizioni (ciò che deve essere sempre vero prima dell'avvio)
>   * Garanzia di successo (*Post-condizioni*)
> * **Scenario Principale di Successo (Flusso Base):** La sequenza lineare di passi in cui tutto va a buon fine.
> * **Estensioni (Flussi Alternativi):** La gestione delle varianti, delle eccezioni e dei fallimenti rispetto al flusso base.
> * **Altre Sezioni:** Requisiti speciali (es. vincoli non funzionali dedicati), varianti tecnologiche/formati dei dati e frequenza di ripetizione dell'evento.
