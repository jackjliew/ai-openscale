---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Weighted F1-Measure

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

# Misura F1 ponderata
{: #quality_wght_f1-measure}

La misura F1 ponderata dà la media ponderata della misura F1 con pesi uguali alla probabilità di classe.
{: shortdesc}

## Misura F1 ponderata a colpo d'occhio
{: #quality_wght_f1-measure-glance}

- **Descrizione**: la media ponderata della misura F1 con pesi uguali alla probabilità della classe
- **Soglie predefinite**: limite inferiore = 80%
- **Raccomandazione predefinita**:
   - **Andamento crescente**: un andamento crescente indica che la metrica sta migliorando. Ciò significa che il nuovo training del modello è efficace.
   - **Andamento decrescente**: un andamento decrescente indica che la metrica sta peggiorando. I dati di feedback stanno riportando differenze significative rispetto ai dati di training.
   - **Variazione anomala o irregolare**: una variazione anomala o irregolare indica che i dati di feedback non sono congruenti tra le valutazioni. Incrementare la dimensione minima del campione per il monitor Qualità.
- **Tipo di problema**: classificazione multi-classe
- **Valori del grafico**: ultimo valore nel periodo di tempo
- **Dettagli di metriche disponibili**: matrice di confusione

## Interpretazione del pannello
{: #quality_wght_f1-measure-display}

![viene visualizzato il grafico della misura F1 ponderata.](images/quality-f1-meas.png)

## Calcolo matematico
{: #quality_wght_f1-measure-math}

La misura F1 ponderata è il risultato dell'utilizzo dei dati ponderati.

```
          (precisione * richiamo)
F1 = 2 *  ____________________

          (precisione + richiamo)
```
