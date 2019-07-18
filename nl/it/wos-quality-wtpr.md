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

# Tasso ponderato di veri positivi (wTPR - Weighted True Positive Rate) ![tag beta](images/beta.png)
{: #quality-wtpr}

Il tasso ponderato di veri positivi fornisce la media ponderata della classe TPR con pesi uguali alla probabilità della classe.
{: shortdesc)

## Tasso ponderato di veri positivi (wTPR - Weighted True Positive Rate) a colpo d'occhio
{: #quality-wtpr-glance}

- **Descrizione**: la media ponderata della classe TPR con pesi uguali alla probabilità della classe
- **Soglie predefinite**: limite inferiore = 80%
- **Raccomandazione predefinita**:
   - **Andamento crescente**: un andamento crescente indica che la metrica sta migliorando. Ciò significa che il nuovo training del modello è efficace.
   - **Andamento decrescente**: un andamento decrescente indica che la metrica sta peggiorando. I dati di feedback stanno riportando differenze significative rispetto ai dati di training.
   - **Variazione anomala o irregolare**: una variazione anomala o irregolare indica che i dati di feedback non sono congruenti tra le valutazioni. Incrementare la dimensione minima del campione per il monitor Qualità.
- **Tipo di problema**: classificazione multi-classe
- **Valori del grafico**: ultimo valore nel periodo di tempo
- **Dettagli di metriche disponibili**: matrice di confusione

## Interpretazione del pannello
{: #quality-wtpr-display}

![viene visualizzato il tasso ponderato di veri positivi](images/quality-tpr.png)

## Calcolo matematico
{: #quality-wtpr-math}

Il tasso di veri positivi è calcolato con la formula seguente:

```
                  numero di veri positivi
TPR =  _________________________________________________________

        (numero di veri positivi + numero di falsi negativi)
```
