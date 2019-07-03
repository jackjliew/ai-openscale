---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds, precision

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

# Precisione ![tag beta](images/beta.png)
{: #quality_precision}

La precisione dà la proporzione di previsioni corrette nelle previsioni della classe dei positivi.
{: shortdesc}

## Precisione a colpo d'occhio
{: #quality_precision-glance}

- **Descrizione**: la proporzione delle previsioni corrette nelle previsioni della classe dei positivi
- **Soglie predefinite**: limite inferiore = 80%
- **Raccomandazione predefinita**:
   - **Andamento crescente**: un andamento crescente indica che la metrica sta migliorando. Ciò significa che il nuovo training del modello è efficace.
   - **Andamento decrescente**: un andamento decrescente indica che la metrica sta peggiorando. I dati di feedback stanno riportando differenze significative rispetto ai dati di training.
   - **Variazione anomala o irregolare**: una variazione anomala o irregolare indica che i dati di feedback non sono congruenti tra le valutazioni. Incrementare la dimensione minima del campione per il monitor Qualità.
- **Tipo di problema**: classificazione binaria
- **Valori del grafico**: ultimo valore nel periodo di tempo
- **Dettagli di metriche disponibili**: matrice di confusione

## Interpretazione del pannello
{: #quality_precision-display}

![viene visualizzato il grafico della precisione.](images/quality-precision.png)

## Calcolo matematico
{: #quality_precision-math}

La precisione (P) è definita come il numero di veri positivi (Tp) sul numero di veri positivi più il numero di falsi positivi (Fp).


```
             numero di veri positivi
Precisione =  __________________________________________________________

             (numero di veri positivi + numero di falsi positivi)
```
