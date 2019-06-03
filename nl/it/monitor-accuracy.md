---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: accuracy, 

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

# Accuratezza
{: #acc-monitor}

L'accuratezza permette di sapere con quale precisione il modello prevede i risultati.
{: shortdesc}

## Informazioni sull'accuratezza
{: #acc-understand}

Accuratezza può significare cose diverse a seconda del tipo di algoritmo:

- *Classificazione multi-classe*: l'accuratezza misura il numero di volte in cui una qualsiasi classe è stata prevista correttamente, normalizzata per il numero di punti di dati. Per ulteriori dettagli, consultare [Multi-class classification![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#multiclass-classification){: new_window} nella documentazione di Apache Spark.

- *Classificazione binaria*: per un algoritmo di classificazione binaria, l'accuratezza è misurata come l'area sotto una curva di ROC. Consultare [Binary classification ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#binary-classification){: new_window} nella documentazione di Apache Spark per ulteriori dettagli.

- *Regressione*: gli algoritmi di regressione sono misurati utilizzando il coefficiente di determinazione o R2. Per ulteriori dettagli, consultare [Regression model evaluation![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#regression-model-evaluation){: new_window} nella documentazione di Apache Spark.

### Funzionamento
{: #acc-works}

È necessario aggiungere i dati di feedback etichettati manualmente attraverso l'interfaccia utente {{site.data.keyword.aios_short}} come mostrato di seguito, utilizzando un [client Python ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://ai-openscale-python-client.mybluemix.net/#feedbacklogging){: new_window} o [API Rest ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/apidocs/ai-openscale#post-feedback-payload){: new_window}.

Esaminare [Framework supportati](/docs/services/ai-openscale?topic=ai-openscale-in-ov#in-fram) per conoscere le limitazioni del monitoraggio dell'accuratezza.

### Accuratezza senza distorsione
{: #acc-debias-view}

Quando ci sono dati a supporto, l'accuratezza del modello include sia il modello originale che quello senza distorsione. {{site.data.keyword.aios_full_notm}} calcola l'accuratezza dell'output senza distorsione e la memorizza nella tabella di registrazione del payload come una colonna aggiuntiva.

![appare una visualizzazione modello con accuratezza calcolata per entrambi i modelli, originale e senza distorsione](images/debiased-accuracy.png)

## Configurazione del monitor Accuratezza
{: #acc-config}

1.  Dalla pagina *Cos'è il monitor Accuratezza?*, fare clic su **Avanti** per avviare il processo di configurazione.

    ![Pagina Cos'è il monitor Accuratezza?](images/accuracy-what-is.png)

1.  Nella pagina *Imposta la soglia di avviso dell'accuratezza*, selezionare un valore che rappresenti un livello di precisione accettabile.

    L'accuratezza è un valore sintetizzato da pertinenti metriche di data science associate a ciascun tipo di modello particolare. Il punteggio è una misura normalizzata per consentire di confrontare facilmente l'accuratezza tra i diversi tipi di modelli. In situazioni tipiche, è sufficiente un punteggio di accuratezza di 80.
    {: note}

    ![Impostare limite di accuratezza](images/accuracy-set-limit.png)

    Fare clic su **Avanti** per continuare.

1.  Ora, impostare le dimensioni minima e massima del campione. La dimensione minima impedisce di misurare l'accuratezza fino a che non è disponibile un numero minimo di record nel dataset di valutazione; questo assicura che la dimensione del campione non sia troppo piccola per l'asimmetria dei risultati. La dimensione massima del campione facilita la gestione del tempo e dello sforzo richiesti per valutare il dataset; se viene superata questa  dimensione verranno valutati solo i record più recenti.

     ![Configurare dimensione del campione](images/accuracy-config-sample.png)

1.  Fare clic sul pulsante **Avanti**.

    Viene visualizzato un riepilogo delle selezioni per la revisione. Se si desidera modificare qualsiasi cosa, fare clic sul link **Modifica** per quella sezione.

1.  Fare clic su **Salva** per completare la configurazione.

Ora è possibile fornire direttamente i dati di feedback al modello, per valutare l'accuratezza.

  ![Inviare dati di feedback](images/accuracy-send-feedback0.png)

Selezionare il pulsante *Aggiungi dati di feedback* per caricare un file di dati in formato CSV; impostare il delimitatore in modo da corrispondere ai dati.

È previsto che il file CSV di feedback abbia tutti i valori funzione e il valore destinazione/etichetta assegnato manualmente. Ad esempio, i dati di training del modello Drug contengono i valori funzione `"AGE"`, `"SEX"`, `"BP"`, `"CHOLESTEROL"`,`"NA"`,`"K"` e il valore destinazione/etichetta `"DRUG"`. Il file CSV di feedback deve includere i valori per quei campi; un esempio potrebbe assomigli a `[43, M, HIGH, NORMAL, 0.6345, 1.4587, DrugX]`. Se viene fornita un'intestazione per il file CSV di feedback, i nomi di campo vengono associati utilizzando l'intestazione. Altrimenti l'ordine dei campi **DEVE** essere esattamente uguale a quello dello schema di training. Per ulteriori informazioni sui dati di training, consultare [Perché {{site.data.keyword.aios_short}} ha bisogno di accedere ai miei dati di training?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)
{: important}

Si noti che i tipi di previsione restituiti dal modello, e la colonna etichetta/destinazione nei dati di feedback, devono corrispondere.
{: note}

  ![Delimitatore accuratezza](images/accuracy-delimit.png)

La dimensione dei file è attualmente limitate a 8MB.
{: note}

In alternativa, è possibile pubblicare i dati di feedback utilizzando i frammenti di codice `cURL` o `Python` forniti.

I campi e i valori nei frammenti di codice devono essere sostituiti con i propri valori reali, in quanto quelli forniti sono solo esempi.
{: important}

È anche possibile scegliere **Esci** per saltare questo passo facoltativo; sarà comunque possibile caricare un file CSV per la valutazione in un secondo momento.

### Passi successivi
{: #acc-next}

Dalla pagina *Configura monitor*, è possibile selezionare un'altra categoria di monitoraggio.
