---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, R squared

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

# R quadrato ![tag beta](images/beta.png)
{: #quality_r_squared}

L'R quadrato è il rapporto della differenza tra la varianza obiettivo e la varianza dell'errore di previsione rispetto alla varianza obiettivo. Può indicare quanto si adattano alla regressione i dati utilizzati per creare il modello.
{: shortdesc}

## R quadrato a colpo d'occhio
{: #quality_r_squared-glance}

- **Descrizione**: il rapporto di differenza tra la varianza obiettivo e la varianza dell'errore di previsione rispetto alla varianza obiettivo
- **Soglie predefinite**: limite inferiore = 80%
- **Raccomandazione predefinita**:
   - **Andamento crescente**: un andamento crescente indica che la metrica sta migliorando. Ciò significa che il nuovo training del modello è efficace.
   - **Andamento decrescente**: un andamento decrescente indica che la metrica sta peggiorando. I dati di feedback stanno riportando differenze significative rispetto ai dati di training.
   - **Variazione anomala o irregolare**: una variazione anomala o irregolare indica che i dati di feedback non sono congruenti tra le valutazioni. Incrementare la dimensione minima del campione per il monitor Qualità.
- **Tipo di problema**: regressione
- **Valori del grafico**: ultimo valore nel periodo di tempo
- **Dettagli di metriche disponibili**: nessuno

## Interpretazione del pannello
{: #quality_r_squared-display}

![viene visualizzato il grafico dell'R quadrato.](images/xxxx.png)

## Calcolo matematico
{: #quality_r_squared-math}

La metrica dell'R quadrato è definita nella seguente formula.

```
                  variazione spiegata
R quadrato = 1 -  _____________________

                    variazione totale
```
