---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Weighted precision

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

# Precisione ponderata
{: #quality_wgth_prec}

La precisione ponderata dà la media ponderata della precisione con pesi uguali alla probabilità di classe.
{: shortdesc}

## Precisione ponderata a colpo d'occhio
{: #quality_wgth_prec-glance}

- **Descrizione**: la media ponderata della precisione con pesi uguali alla probabilità della classe
- **Soglie predefinite**: limite inferiore = 80%
- **Raccomandazione predefinita**:
   - **Andamento crescente**: un andamento crescente indica che la metrica sta migliorando. Ciò significa che il nuovo training del modello è efficace.
   - **Andamento decrescente**: un andamento decrescente indica che la metrica sta peggiorando. I dati di feedback stanno riportando differenze significative rispetto ai dati di training.
   - **Variazione anomala o irregolare**: una variazione anomala o irregolare indica che i dati di feedback non sono congruenti tra le valutazioni. Incrementare la dimensione minima del campione per il monitor Qualità.
- **Tipo di problema**: classificazione multi-classe
- **Valori del grafico**: ultimo valore nel periodo di tempo
- **Dettagli di metriche disponibili**: matrice di confusione

## Interpretazione del pannello
{: #quality_wgth_prec-display}

![viene visualizzato il grafico della precisione ponderata.](images/quality-precision.png)

## Calcolo matematico
{: #quality_wgth_prec-math}

La precisione (P) è definita come il numero di veri positivi (Tp) sul numero di veri positivi più il numero di falsi positivi (Fp).


```
                        numero di veri positivi
Precisione =  __________________________________________________________

             (numero di veri positivi + numero di falsi positivi)
```
