---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds, Area under ROC

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

# Area sotto la curva ROC ![tag beta](images/beta.png)
{: #quality_roc}

L'area sotto la curva ROC (receiver operating characteristic) fornisce l'area sotto la curva della percentuale di richiami e falsi positivi. Calcola la sensibilità rispetto al tasso di ricaduta.
{: shortdesc}

## Area sotto la curva ROC a colpo d'occhio
{: #quality_roc-glance}

- **Descrizione**: l'area sotto la curva della percentuale di richiami e falsi positivi
- **Soglie predefinite**: limite inferiore = 80%
- **Raccomandazione predefinita**:
   - **Andamento crescente**: un andamento crescente indica che la metrica sta migliorando. Ciò significa che il nuovo training del modello è efficace.
   - **Andamento decrescente**: un andamento decrescente indica che la metrica sta peggiorando. I dati di feedback stanno riportando differenze significative rispetto ai dati di training.
   - **Variazione anomala o irregolare**: una variazione anomala o irregolare indica che i dati di feedback non sono congruenti tra le valutazioni. Incrementare la dimensione minima del campione per il monitor Qualità.
- **Tipo di problema**: classificazione binaria
- **Valori del grafico**: ultimo valore nel periodo di tempo
- **Dettagli di metriche disponibili**: matrice di confusione

## Interpretazione del pannello
{: #quality_roc-display}

![viene visualizzato il grafico dell'area sotto la curva ROC.](images/quality-area-under-roc.png)

## Calcolo matematico
{: #quality_roc-math}

L'area sotto la curva ROC è tracciata parametricamente come `tasso di veri positivi` rispetto al `tasso di falsi positivi` rispetto ad una soglia `T`.

