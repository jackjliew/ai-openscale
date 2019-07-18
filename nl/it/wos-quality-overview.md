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

# Panoramica sulle metriche di qualità ![tag beta](images/beta.png)
{: #anlz_metrics}

Utilizzare il monitoraggio della qualità per determinare la precisione con cui il modello predice i risultati. Quando il monitoraggio della qualità è abilitato, genera una serie di metriche ogni ora per impostazione predefinita. È possibile generare queste metriche on-demand facendo clic sul pulsante **Controlla qualità ora** o utilizzando il client Python.

Le metriche di qualità sono calcolate in base alle seguenti informazioni:

- dati di feedback etichettati manualmente,
- risposte della distribuzione monitorata per questi dati.

Per un corretto monitoraggio, i dati di feedback devono essere registrati in {{site.data.keyword.aios_short}} su base regolare. I dati di feedback possono essere forniti utilizzando l'opzione "Aggiungi dati di feedback" o utilizzando il client Python o l'API REST.

Per i motori di machine learning diversi da {{site.data.keyword.aios_short}} come Microsoft Azure ML Studio, Microsoft Azure ML Service o Amazon Sagemaker ML, il monitoraggio della qualità crea ulteriori richieste di calcolo del punteggio sulla distribuzione monitorata.
{: note}

È possibile esaminare tutti i valori di metrica nel tempo sul dashboard {{site.data.keyword.aios_short}}:

![grafico delle metriche di qualità che mostra la deviazione dell'area sotto la curva di ROC](images/quality_metrics_001.png)


Per esaminare i dettagli correlati, ad esempio la matrice di confusione per la classificazione binaria e multi-classe, disponibile per alcune metriche, fare clic sul grafico.

![tabella dei dettagli delle metriche di qualità](images/quality_metrics_002.png)

## Metriche di qualità supportate
{: #anlz_metrics_supqualdets}

Le seguenti metriche di qualità sono supportate da {{site.data.keyword.aios_short}}:

- [Area sotto la curva ROC](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_roc)
- [Area sotto la curva PR](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality-area-pr)
- [Accuratezza](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-accuracy-opener)
- [Tasso di veri positivi (TPR - True positive rate)](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_tpr)
- [Tasso di falsi positivi (FPR - False positive rate)](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_fpr_false)
- [Richiamo](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_recall)
- [Precisione](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_precision)
- [Misura F1](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_f1-measr)
- [Perdita logaritmica](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_log_loss)

## Dettagli di qualità supportati
{: #anlz_metrics_supqualdets_suppr_dets}

I seguenti dettagli delle metriche di qualità sono supportati da {{site.data.keyword.aios_short}}:

### Matrice di confusione
{: #anlz_metrics_supqualdets_confusion-quickovr}

La matrice di confusione consente di comprendere per quale dei dati di feedback la risposta della distribuzione monitorata è corretta e per la quale non lo è.

Per ulteriori informazioni, consultare [Matrice di confusione](/docs/services/ai-openscale?topic=ai-openscale-it-conf-mtx).
