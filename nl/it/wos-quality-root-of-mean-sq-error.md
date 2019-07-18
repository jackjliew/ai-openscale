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

# Radice dell'errore quadratico medio ![tag beta](images/beta.png)
{: #supqualdets_squ_errors_mean}

La radice dell'errore quadratico medio (o RMSE - root-mean-squared error) mostra la differenza tra i valori previsti e osservati nel proprio modello.
{: shortdesc}

## Radice dell'errore quadratico medio a colpo d'occhio
{: #anlz_metrics_supqualdets_squ_errors_mean}

- **Descrizione**: la radice quadrata della media della differenza quadratica tra previsione del modello e valore obiettivo
- **Soglie predefinite**: limite superiore = 80%
- **Raccomandazione predefinita**:
   - **Andamento crescente**: un andamento crescente indica che la metrica sta peggiorando. I dati di feedback stanno riportando differenze significative rispetto ai dati di training.
   - **Andamento decrescente**: un andamento decrescente indica che la metrica sta migliorando. Ciò significa che il nuovo training del modello è efficace.
   - **Variazione anomala o irregolare**: una variazione anomala o irregolare indica che i dati di feedback non sono congruenti tra le valutazioni. Incrementare la dimensione minima del campione per il monitor Qualità.
- **Tipo di problema**: regressione
- **Valori del grafico**: ultimo valore nel periodo di tempo
- **Dettagli di metriche disponibili**: nessuno

## Interpretazione del pannello
{: #supqualdets_squ_errors_mean-display}

![viene visualizzato il grafico della radice dell'errore quadratico medio.](images/xxxx.png)

## Calcolo matematico
{: #supqualdets_squ_errors_mean-math}

La radice dell'errore quadratico medio equivale alla radice quadrata della media di (previsioni meno valori osservati) al quadrato.

```
          ___________________________________________________________
RMSE  =  √(previsioni - valori osservati)*(previsioni - valori osservati)
```
