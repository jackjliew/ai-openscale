---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Weighted False Positive Rate, wFPR

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

# Tasso ponderato di falsi positivi (wFPR - Weighted False Positive Rate)
{: #quality_wfpr_weighted}

Il tasso ponderato di falsi positivi (wFPR) fornisce la media ponderata della classe tasso falsi positivi (FPR) con pesi uguali alla probabilità della classe.
{: shortdesc}

## Tasso ponderato di falsi positivi (wFPR - Weighted False Positive Rate) a colpo d'occhio
{: #quality_wfpr_weighted-glance}

- **Descrizione**: la proporzione di previsioni errate nella classe dei positivi
- **Soglie predefinite**: limite inferiore = 80%
- **Raccomandazione predefinita**:
   - **Andamento crescente**: un andamento crescente indica che la metrica sta peggiorando. I dati di feedback stanno riportando differenze significative rispetto ai dati di training.
   - **Andamento decrescente**: un andamento decrescente indica che la metrica sta migliorando. Ciò significa che il nuovo training del modello è efficace.
   - **Variazione anomala o irregolare**: una variazione anomala o irregolare indica che i dati di feedback non sono congruenti tra le valutazioni. Incrementare la dimensione minima del campione per il monitor Qualità.
- **Tipo di problema**: classificazione multi-classe
- **Valori del grafico**: ultimo valore nel periodo di tempo
- **Dettagli di metriche disponibili**: matrice di confusione

## Interpretazione del pannello
{: #quality_wfpr_weighted-display}

![viene visualizzato il grafico del tasso ponderato di falsi positivi.](images/quality-fpr.png)

## Calcolo matematico
{: #quality_wfpr_weighted-math}

Il tasso ponderato di falsi positivi è l'applicazione dell'FPR con i dati ponderati.

```
                   numero di falsi positivi
FPR =  ______________________________________________________

       (numero di falsi positivi + numero di veri negativi)
```
