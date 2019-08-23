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

# Richiamo
{: #quality_recall}

Il richiamo dà la proporzione di previsioni corrette nella classe dei positivi.
{: shortdesc}

## Richiamo a colpo d'occhio
{: #quality_recall-glance}

- **Descrizione**: la proporzione di previsioni corrette nella classe dei positivi
- **Soglie predefinite**: limite inferiore = 80%
- **Raccomandazione predefinita**:
   - **Andamento crescente**: un andamento crescente indica che la metrica sta migliorando. Ciò significa che il nuovo training del modello è efficace.
   - **Andamento decrescente**: un andamento decrescente indica che la metrica sta peggiorando. I dati di feedback stanno riportando differenze significative rispetto ai dati di training.
   - **Variazione anomala o irregolare**: una variazione anomala o irregolare indica che i dati di feedback non sono congruenti tra le valutazioni. Incrementare la dimensione minima del campione per il monitor Qualità.
- **Tipo di problema**: classificazione binaria
- **Valori del grafico**: ultimo valore nel periodo di tempo
- **Dettagli di metriche disponibili**: matrice di confusione

## Interpretazione del pannello delle metriche di richiamo
{: #quality_recall-display}

![viene visualizzato il grafico del richiamo.](images/quality-recall.png)

### Punteggio di correttezza
{: #quality_recall-display-fairness-score}

Per la metrica di richiamo, viene visualizzato il seguente punteggio di correttezza. 

![viene visualizzata la percentuale del punteggio del richiamo.](images/wos-quality-recall-score.png)

### Pianifica
{: #quality_recall-display-schedule}

Il riquadro **Pianifica** mostra i tempi per **Ultima valutazione** e **Valutazione successiva**. Le metriche di qualità vengono valutate ogni ora. È possibile forzare la valutazione facendo clic su **Controlla qualità ora**. È anche possibile aggiungere il feedback facendo clic su **Aggiungi dati di feedback**.

![viene visualizzato il riquadro Pianifica, che mostra l'ora dell'ultima valutazione e quella della successiva](images/wos-quality-schedule.png)


### Suggerimento
{: #quality_recall-display-recommendations}

Per facilitare l'interpretazione del grafico, viene visualizzato il riquadro **Suggerimento**, le cui tendenze indicano il miglioramento o il peggioramento dell'efficacia del modello.

![viene visualizzato il riquadro Suggerimento.](images/wos-quality-positive-recommendation.png)




## Calcolo matematico
{: #quality_recall-math}

Il richiamo (R) è definito come il numero di veri positivi (Tp) sul numero di veri positivi più il numero di falsi negativi (Fn).

```
                       numero di veri positivi
Richiamo =   ______________________________________________________

           (numero di veri positivi + numero di falsi negativi)
```
