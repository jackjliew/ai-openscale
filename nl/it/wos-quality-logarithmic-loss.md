---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: fairness, fairness monitor, payload, perturbation, training data, debiased, Logarithmic loss

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

# Perdita logaritmica
{: #quality_log_loss}

La Perdita logaritmica dà la media delle probabilità della classe obiettivo dei logaritmi (confidenza). È nota anche come logaritmo della verosimiglianza prevista ed è una misurazione efficace delle prestazioni del modello.
{: shortdesc}

## Perdita logaritmica a colpo d'occhio
{: #quality_log_loss-glance}

- **Descrizione**: la media delle probabilità della classe obiettivo dei logaritmi (confidenza). È nota anche come logaritmo della verosimiglianza prevista.
- **Soglie predefinite**: limite inferiore = 80%
- **Raccomandazione predefinita**:
   - **Andamento crescente**: un andamento crescente indica che la metrica sta peggiorando. I dati di feedback stanno riportando differenze significative rispetto ai dati di training.
   - **Andamento decrescente**: un andamento decrescente indica che la metrica sta migliorando. Ciò significa che il nuovo training del modello è efficace.
   - **Variazione anomala o irregolare**: una variazione anomala o irregolare indica che i dati di feedback non sono congruenti tra le valutazioni. Incrementare la dimensione minima del campione per il monitor Qualità.
- **Tipi di problema**: classificazione binaria e classificazione multi-classe
- **Valori del grafico**: ultimo valore nel periodo di tempo
- **Dettagli di metriche disponibili**: nessuno

## Interpretazione del pannello
{: #quality_log_loss-display}

![viene visualizzata la perdita logaritmica](images/quality-log-loss.png)

### Punteggio di correttezza
{: #quality_log_loss-display-fairness-score}

Per la metrica di perdita logaritmica, viene visualizzato il seguente punteggio di correttezza. 

![viene visualizzata la percentuale del punteggio del richiamo.](images/wos-quality-logloss-score.png)

### Pianifica
{: #quality_log_loss-display-schedule}

Il riquadro **Pianifica** mostra i tempi per **Ultima valutazione** e **Valutazione successiva**. Le metriche di qualità vengono valutate ogni ora. È possibile forzare la valutazione facendo clic su **Controlla qualità ora**. È anche possibile aggiungere il feedback facendo clic su **Aggiungi dati di feedback**.

![viene visualizzato il riquadro Pianifica, che mostra l'ora dell'ultima valutazione e quella della successiva](images/wos-quality-schedule.png)


### Suggerimento
{: #quality_log_loss-display-recommendations}

Per facilitare l'interpretazione del grafico, viene visualizzato il riquadro **Suggerimento**, le cui tendenze indicano il miglioramento o il peggioramento dell'efficacia del modello.

![viene visualizzato il riquadro Suggerimento.](images/wos-quality-negative-recommendation.png)



## Calcolo matematico
{: #quality_log_loss-math}

Per un modello binario, la perdita logaritmica è calcolata utilizzando la seguente formula:

```
-(y log(p) + (1-y)log(1-p))
```

dove p = etichetta vero e y = probabilità prevista

Per un modello multi-classe, la perdita logaritmica è calcolata utilizzando la seguente formula:

```
  M
-SUM Yo,c log(Po,c)
 c=1 
```

dove M > 2, p = etichetta vero e y = probabilità prevista
