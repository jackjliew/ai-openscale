---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:download: .download}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:faq: data-hd-content-type='faq'}

# Accuratezza
{: #accuracy-opener}

L'accuratezza è una misura della proporzione di previsioni corrette contenute nel modello.
{: shortdesc}

## Accuratezza a colpo d'occhio
{: #anlz_metrics_supqualdets_acc}

- **Descrizione**: la proporzione di previsioni corrette
- **Soglie predefinite**: limite inferiore = 80%
- **Raccomandazione predefinita**:
   - **Andamento crescente**: un andamento crescente indica che la metrica sta migliorando. Ciò significa che il nuovo training del modello è efficace.
   - **Andamento decrescente**: un andamento decrescente indica che la metrica sta peggiorando. I dati di feedback stanno riportando differenze significative rispetto ai dati di training.
   - **Variazione anomala o irregolare**: una variazione anomala o irregolare indica che i dati di feedback non sono congruenti tra le valutazioni. Incrementare la dimensione minima del campione per il monitor Qualità.
- **Tipi di problema**: classificazione binaria e classificazione multi-classe
- **Valori del grafico**: ultimo valore nel periodo di tempo
- **Dettagli di metriche disponibili**: matrice di confusione


## Informazioni sull'accuratezza
{: #acc-understand}

Accuratezza può significare cose diverse a seconda del tipo di algoritmo:

- *Classificazione multi-classe*: l'accuratezza misura il numero di volte in cui una qualsiasi classe è stata prevista correttamente, normalizzata per il numero di punti di dati. Per ulteriori dettagli, consultare [Multi-class classification](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#multiclass-classification){: external} nella documentazione di Apache Spark.

- *Classificazione binaria*: per un algoritmo di classificazione binaria, l'accuratezza è misurata come l'area sotto una curva di ROC. Consultare [Binary classification](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#binary-classification){: external} nella documentazione di Apache Spark per ulteriori dettagli.

- *Regressione*: gli algoritmi di regressione sono misurati utilizzando il coefficiente di determinazione o R2. Per ulteriori dettagli, consultare [Regression model evaluation](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#regression-model-evaluation){: external} nella documentazione di Apache Spark.

### Funzionamento
{: #acc-works}

È necessario aggiungere i dati di feedback etichettati manualmente attraverso l'interfaccia utente {{site.data.keyword.aios_short}}, come mostrato nei seguenti esempi, utilizzando un [client Python](http://ai-openscale-python-client.mybluemix.net/#feedbacklogging){: external} o [l'API Rest](https://cloud.ibm.com/apidocs/ai-openscale#post-feedback-payload){: external}.

Esaminare [Framework supportati](/docs/services/ai-openscale?topic=ai-openscale-in-ov#in-fram) per conoscere le limitazioni del monitoraggio dell'accuratezza.

### Accuratezza senza distorsione
{: #acc-debias-view}

Quando ci sono dati a supporto, l'accuratezza viene calcolata sia sul modello originale che su quello senza distorsione. {{site.data.keyword.aios_full_notm}} calcola l'accuratezza dell'output senza distorsione e la memorizza nella tabella di registrazione del payload come una colonna aggiuntiva.

![appare una visualizzazione modello con accuratezza calcolata per entrambi i modelli, originale e senza distorsione](images/debiased-accuracy.png)
