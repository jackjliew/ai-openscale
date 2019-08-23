---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Mean squared error

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

# Errore quadratico medio
{: #quality_squerror}

L'errore quadratico medio dà la media della differenza quadratica tra la previsione del modello e il valore obiettivo. Può essere utilizzato come misura della qualità di uno stimatore.
{: shortdesc}

## Errore quadratico medio a colpo d'occhio
{: #quality_squerror-glance}

- **Descrizione**: la media della differenza quadratica tra previsione del modello e valore obiettivo
- **Soglie predefinite**: limite superiore = 80%
- **Raccomandazione predefinita**:
   - **Andamento crescente**: un andamento crescente indica che la metrica sta peggiorando. I dati di feedback stanno riportando differenze significative rispetto ai dati di training.
   - **Andamento decrescente**: un andamento decrescente indica che la metrica sta migliorando. Ciò significa che il nuovo training del modello è efficace.
   - **Variazione anomala o irregolare**: una variazione anomala o irregolare indica che i dati di feedback non sono congruenti tra le valutazioni. Incrementare la dimensione minima del campione per il monitor Qualità.
- **Tipo di problema**: regressione
- **Valori del grafico**: ultimo valore nel periodo di tempo
- **Dettagli di metriche disponibili**: nessuno

## Interpretazione del pannello
{: #quality_squerror-display}

![viene visualizzato il grafico dell'errore quadratico medio.](images/xxxx.png)

## Calcolo matematico
{: #quality_squerror-math}

L'errore quadratico medio nella sua forma più semplice è rappresentato dalla seguente formula.

```
                         SOMMA  (Yi - ^Yi) * (Yi - ^Yi)
Errori quadratici medi  =  ____________________________

                             numero di errori
```
