---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Proportion explained variance

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

# Varianza spiegata dalla proporzione ![tag beta](images/beta.png)
{: #quality_var}

La varianza spiegata dalla proporzione fornisce il rapporto tra varianza spiegata e varianza obiettivo. La varianza spiegata indica la differenza tra varianza obiettivo e varianza dell'errore di previsione.
{: shortdesc}

## Varianza spiegata dalla proporzione a colpo d'occhio
{: #quality_var-glance}

- **Descrizione**: la varianza spiegata dalla proporzione rappresenta il rapporto tra varianza spiegata e varianza obiettivo. La varianza spiegata indica la differenza tra varianza obiettivo e varianza dell'errore di previsione.
- **Soglie predefinite**: limite inferiore = 80%
- **Raccomandazione predefinita**:
   - **Andamento crescente**: un andamento crescente indica che la metrica sta migliorando. Ciò significa che il nuovo training del modello è efficace.
   - **Andamento decrescente**: un andamento decrescente indica che la metrica sta peggiorando. I dati di feedback stanno riportando differenze significative rispetto ai dati di training.
   - **Variazione anomala o irregolare**: una variazione anomala o irregolare indica che i dati di feedback non sono congruenti tra le valutazioni. Incrementare la dimensione minima del campione per il monitor Qualità.
- **Tipo di problema**: regressione
- **Valori del grafico**: ultimo valore nel periodo di tempo
- **Dettagli di metriche disponibili**: nessuno

## Interpretazione del pannello
{: #quality_var-display}

![viene visualizzato il grafico della varianza spiegata dalla proporzione.](images/xxxx.png)

## Calcolo matematico
{: #quality_var-math}

La varianza spiegata dalla proporzione si ottiene calcolando la media dei numeri e sottraendo per ogni numero la media e facendo il quadrato dei risultati. Successivamente si elaborano i quadrati

```
                                  somma dei quadrati tra i gruppi
Varianza spiegata dalla proporzione =  ________________________________

                                      somma dei quadrati totali
```
