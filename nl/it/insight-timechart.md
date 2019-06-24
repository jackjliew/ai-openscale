---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

keywords: fairness, monitoring, charts, de-biasing, bias, accuracy

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Monitoraggio della correttezza, Richieste medie al minuto e Accuratezza
{: #it-ov}

I dati di monitoraggio per le singole distribuzioni vengono visualizzati in un grafico di serie temporali. Il grafico traccia la correttezza, le richieste medie al minuto e l'accuratezza negli ultimi sette giorni.
{: shortdesc}

## Visualizzazione dei dati per una distribuzione
{: #it-vdep}

Selezionare una distribuzione dal dashboard per visualizzare i dati di monitoraggio per tale distribuzione. La parte superiore del grafico dei dati di monitoraggio visualizza le informazioni sul modello distribuito, incluso quando il modello è stato valutato l'ultima volta per rilevare correttezza e accuratezza, e quando sarà valutato la prossima volta.

![Grafico delle serie temporali](images/insight-time-chart.png)

Poiché i controlli degli algoritmi vengono eseguiti solo ogni ora, sono presenti anche pulsanti  per consentire di controllare correttezza e accuratezza su richiesta. Se non vengono forniti  record di payload (correttezza) o record di feedback (accuratezza) sufficienti, viene visualizzato un messaggio simile al seguente:

![Pulsante Accuratezza](images/accuracy-button.png)

Successivamente, spostare il puntatore nel grafico per vedere le statistiche per una singola ora. In questo esempio, il tempo selezionato è l'1:00 PM CST il 18 settembre, che rivela le seguenti statistiche:

![Dettagli del grafico delle serie temporali](images/insight-time-detail.png)

- ***Correttezza***: due di tre funzioni di correttezza, Car Value e Area Code, hanno soddisfatto le soglie di approvazione. La terza funzione di correttezza, Age, è stata segnalata per distorsione. Si può anche vedere il numero di risultati previsti (in questo caso le percentuali di approvazioni rispetto i rifiuti) per una singola popolazione nelle funzioni monitorate per la correttezza.
- ***Accuratezza***: la metrica di accuratezza con media del 78%.
- ***Richieste medie al minuto***: in media, sono stati elaborati 300 record al minuto tra l'1:00 e le 2:00 PM CST. La velocità di trasmissione viene calcolata ogni minuto, e il suo valore medio durante il corso dell'ora è riportato nel grafico.

## Visualizzazione dei dati per un'ora specifica
{: #it-vdet}

Per visualizzare i dettagli dietro una determinata statistica di correttezza, fare clic sul link **Visualizza dettagli** per l'ora selezionata.

Si apre una visualizzazione dei punti di dati per una funzione monitorata all'ora selezionata. In seguito all'esempio precedente viene visualizzata la funzione Age, che è stata contrassegnata per la distorsione.

Notare i tre filtri in alto nella pagina (Funzione, Data e Ora) che permettono di selezionare una funzione o un tempo diversi per esaminare i dettagli.

![Grafico delle serie temporali](images/insight-data-detail.png)

### Interpretazione del grafico
{: #it-intp}

Il grafico mostra più cose:

- Si può osservare la popolazione che sperimenta la distorsione (i clienti tra i 18 e i 23 anni). Il grafico mostra anche la percentuale di risultati previsti (52%) per questa popolazione.

- Il grafico mostra anche la percentuale di risultati previsti (70%) per la popolazione di riferimento. Questa è la media dei risultati previsti in tutte le popolazioni di riferimento.

- Il grafico indica la presenza di distorsione, perché il rapporto tra la percentuale di risultati previsti per le popolazioni di età tra i 18 e i 23 anni e la percentuale di risultati previsti per la popolazione di riferimento è al di sotto della soglia. In altre parole, 0.52/0.7 = 0.74, che è inferiore alla soglia 0.8.

- Il grafico mostra anche la distribuzione dei valori di riferimento e monitorati per ogni valore distinto dell'attributo nei dati della tabella payload che è stata analizzata per identificare la distorsione. In altre parole, se l'algoritmo di rilevamento della distorsione ha analizzato gli ultimi 1790 record dalla tabella di payload, per 120 di questi record l'età del cliente era tra i 18 e i 23, e fuori da quella distribuzione i risultati `Approvato` e `Denied` sono rappresentati dal grafico a barre. La distribuzione dei dati di payload viene visualizzata per ogni valore distinto dell'attributo di correttezza (sono visualizzati anche i valori di riferimento). Queste informazioni possono essere utilizzate per correlare la distorsione con la quantità di dati ricevuti dal modello.

- Il grafico mostra inoltre che la popolazione con età compresa tra i 31 e i 35 anni ha ricevuto il 91% di risultati previsti. Ciò indica l'origine della distorsione, il che significa che tali dati in questo gruppo hanno reso asimmetrici i risultati e hanno portato ad un aumento della percentuale dei risultati previsti per la classe di riferimento. Queste informazioni possono essere utilizzate per identificare parti dei dati che possono poi essere sotto-campionate quando si riesegue il training del modello.

- Un'altra cosa importante che il grafico mostra è il nome della tabella contenente i dati che sono stati identificati per l'etichettatura manuale. Ogni volta che l'algoritmo rileva la distorsione in un modello, identifica anche i punti di dati che possono essere inviati per l'etichettatura manuale da parte di persone. Questi dati etichettati manualmente possono poi essere utilizzati con i dati di training originali per rieseguire il training del modello. Questo modello risottoposto a training è probabile che non abbia la distorsione. La tabella di etichettatura manuale è presente nel database associato con all'istanza {{site.data.keyword.aios_short}}.

## Dati di runtime e training
{: #it-rtsw}

Lo switch dati di runtime/dati di training consente di alternare le differenze tra il modello sottoposto a training e i dati raccolti in fase di runtime che fa scattare un avvertenza di distorsione. Per ulteriori informazioni sui dati di training, consultare [Perché {{site.data.keyword.aios_short}} ha bisogno di accedere ai miei dati di training?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)

![Alternanza runtime training](images/runtime_train_data.png)

## Visualizza transazioni
{: #it-tra}

Questa opzione consente di visualizzare le singole transazioni che hanno contribuito alla distorsione quando si fa clic sul pulsante **Visualizza transazioni** .

![Visualizza transazioni](images/view_transactions.png)

Viene visualizzato un elenco delle transazioni in cui la distribuzione ha contribuito alla distorsione. Fare clic sul link **Spiega** per qualsiasi ID di transazione per ottenere i dettagli su quella transazione nella scheda Esplicabilità. Per ulteriori informazioni, consultare [Monitoraggio esplicabilità](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).

Selezionare la vista **Tutte le transazioni** per visualizzare tutte le transazioni dalla funzione selezionata (in questo esempio "Età") e nel periodo selezionato (in questo esempio "15 settembre 2018 1:00 PM"):

![Elenco di tutte le transazioni](images/transaction_list1.png)

Selezionare la vista **Transazioni con distorsione** per visualizzare solo il sottoinsieme di transazioni che hanno ricevuto risultati distorti. Ogni transazione distorta è confrontata con una transazione simile ma leggermente alterata (perturbata) che mostra come la modifica del valore della funzione monitorata (Età) provocherà un esito favorevole per la transazione distorta:

![Elenco transazioni distorte](images/transaction_list2.png)

## Modello di produzione e modello con distorsione annullata
{: #it-prdb}

È possibile utilizzare queste due schede per alternare tra il modello di produzione e un modello con distorsione annullata creato da {{site.data.keyword.aios_short}}. Consultare [Come funziona l'annullamento della distorsione](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor#mf-debias) per ulteriori dettagli.

![Alternanza runtime training](images/bias-debias.png)

Selezionando la scheda **Modello con distorsione annullata** vengono mostrati i cambiamenti nel modello con distorsione annullata, rispetto al modello in produzione. In questo esempio, la Correttezza del modello è aumentata dal 74% al 93%, con un calo di solo l'1% in Accuratezza. Il grafico riflette anche lo stato migliorato del risultato per i gruppi di età compresa tra i 18 e i 23 anni.

![Alternanza runtime training](images/insight-data-detail2.png)

### Opzioni di annullamento distorsione
{: #it-dbo}

- *Annullamento distorsione passivo* - Quando {{site.data.keyword.aios_short}} esegue il controllo della distorsione effettua anche un annullamento della distorsione dei dati analizzando il comportamento del modello e identificando i dati in cui il modello contribuisce alla distorsione.

  {{site.data.keyword.aios_short}} poi creare un modello di machine learning per prevedere se è probabile che il modello contribuirà alla distorsione su un nuovo punto di dati fornito. {{site.data.keyword.aios_short}} poi analizza i dati ricevuti dal modello, su base oraria, e trova i punti di dati in cui {{site.data.keyword.aios_short}} crede che il modello stia contribuendo alla distorsione. Per questi punti di dati, l'attributo di correttezza è perturbato da minoranza a maggioranza, e i dati perturbati vengono inviati al modello originale per la previsione. Questa previsione del modello originale viene utilizzata come output con distorsione annullata.

  {{site.data.keyword.aios_short}} esegue questo annullamento della distorsione ogni ora, su tutti i dati che sono stati ricevuti dal modello nell'ultima ora. Calcola anche la correttezza per l'output con distorsione annullata e lo visualizza nella scheda **Modello con distorsione annullata**.

- *Annullamento distorsione attivo* - In modalità di annullamento distorsione attiva è possibile utilizzare un endpoint API REST di annullamento distorsione dall'applicazione. Questo endpoint API REST richiamerà internamente il modello e ne verificherà il comportamento.

  Se {{site.data.keyword.aios_short}} ritiene che il modello sta contribuendo alla distorsione, eseguirà la perturbazione dei dati come indicato in precedenza e li invierà di nuovo al modello originale. L'output del modello originale sui dati perturbati sarà restituito come previsione senza distorsione. Se {{site.data.keyword.aios_short}} determina che il modello originale non sta agendo in modo distorto, {{site.data.keyword.aios_short}} restituirà la previsione del modello originale come previsione senza distorsione. Pertanto, utilizzando questo endpoint API REST, è possibile assicurarsi che l'applicazione non prenda decisione in base all'output distorto dei modelli.

Selezionare il link **Endpoint di calcolo del punteggio di distorsioni annullate** per trovare l'endpoint API REST di annullamento distorsione

![Endpoint API annullamento distorsione](images/insight-debias-api.png)
