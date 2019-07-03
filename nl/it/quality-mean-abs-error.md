---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds, Mean absolute error

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

# Errore assoluto medio ![tag beta](images/beta.png)
{: #quality_abserror}

L'errore assoluto medio dà la media della differenza assoluta tra la previsione del modello e il valore obiettivo.
{: shortdesc}

## Errore assoluto medio a colpo d'occhio
{: #quality_abserror-glance}

- **Descrizione**: la media della differenza assoluta tra previsione del modello e valore obiettivo
- **Soglie predefinite**: limite superiore = 80%
- **Raccomandazione predefinita**:
   - **Andamento crescente**: un andamento crescente indica che la metrica sta peggiorando. I dati di feedback stanno riportando differenze significative rispetto ai dati di training.
   - **Andamento decrescente**: un andamento decrescente indica che la metrica sta migliorando. Ciò significa che il nuovo training del modello è efficace.
   - **Variazione anomala o irregolare**: una variazione anomala o irregolare indica che i dati di feedback non sono congruenti tra le valutazioni. Incrementare la dimensione minima del campione per il monitor Qualità.
- **Tipo di problema**: regressione
- **Valori del grafico**: ultimo valore nel periodo di tempo
- **Dettagli di metriche disponibili**: nessuno

## Interpretazione del pannello
{: #quality_abserror-display}

![viene visualizzato il grafico dell'errore assoluto medio.](images/xxxx.png)

## Calcolo matematico
{: #quality_abserror-math}

L'errore assoluto medio è calcolato sommando tutti gli errori assoluti e diviendoli per il numero di errori.

```
                         SOMMA  | Yi - Xi |
Errori assoluti medi =  ____________________

                          numero di errori
```
