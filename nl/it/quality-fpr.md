---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds, False positive rate, fpr

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

# Tasso di falsi positivi (FPR - False positive rate) ![tag beta](images/beta.png)
{: #quality_fpr_false}

Il tasso di falsi positivi fornisce la proporzione di previsioni errate nella classe dei positivi.
{: shortdesc}

## Tasso di falsi positivi (FPR - False positive rate)
{: #quality_fpr_false-glance}

- **Descrizione**: la proporzione di previsioni errate nella classe dei positivi
- **Soglie predefinite**: limite inferiore = 80%
- **Raccomandazione predefinita**:
   - **Andamento crescente**: un andamento crescente indica che la metrica sta migliorando. Ciò significa che il nuovo training del modello è efficace.
   - **Andamento decrescente**: un andamento decrescente indica che la metrica sta peggiorando. I dati di feedback stanno riportando differenze significative rispetto ai dati di training.
   - **Variazione anomala o irregolare**: una variazione anomala o irregolare indica che i dati di feedback non sono congruenti tra le valutazioni. Incrementare la dimensione minima del campione per il monitor Qualità.
- **Tipo di problema**: classificazione binaria
- **Valori del grafico**: ultimo valore nel periodo di tempo
- **Dettagli di metriche disponibili**: matrice di confusione

## Interpretazione del pannello
{: #quality_fpr_false-display}

![viene visualizzato il grafico del tasso di falsi positivi.](images/quality-fpr.png)

## Calcolo matematico
{: #quality_fpr_false-math}

Il tasso di falsi positivi è calcolato come il numero totale di falsi positivi diviso per il numero di falsi positivi e il numero di veri negativi.

```
                        numero di falsi positivi
Tasso falsi positivi =  ______________________________________________________

                       (numero di falsi positivi + numero di veri negativi)
```
