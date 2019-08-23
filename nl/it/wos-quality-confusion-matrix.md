---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, confusion matrix

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

# Matrice di confusione
{: #it-conf-mtx}

Come un dettaglio delle metriche di qualità, è possibile visualizzare i record che il modello ha analizzato in modo non corretto. Tali anomalie possono essere falsi positivi o falsi negativi per i modelli di classificazione binari o possono essere assegnazioni di classi non corrette per i modelli multi-classe. È anche possibile visualizzare un elenco di record di feedback che il modello non ha analizzato correttamente.
{: shortdesc}

Per esaminare i dettagli correlati, ad esempio la matrice di confusione per la classificazione binaria e multi-classe, disponibile per alcune metriche, fare clic sul grafico.

![tabella dei dettagli delle metriche di qualità](images/quality_metrics_002.png)

Per i problemi binari, {{site.data.keyword.aios_full}} assegna la categoria di destinazione al livello `positivo` o `negativo`. Per questo, l'output della matrice di confusione segue la convenzione per cui l'etichetta per la categoria positiva si trova nella seconda riga o colonna.


## Passi
{: #it-conf-mtx-steps}

1. Da uno qualsiasi dei grafici **Qualità**, come **Accuratezza** fare clic su un'ora/giorno nel grafico.
    
    ![Elenco transazioni distorte](images/Confusion_Matrix_040819.004.png)

1. Una matrice di confusione visualizza i falsi positivi e falsi negativi. Fare clic su una cella per visualizzare il sottoinsieme dei record di feedback.

    ![Elenco transazioni distorte](images/Confusion_Matrix_040819.005.png)

1. Esaminare i record di feedback e richiedere una spiegazione dell'analisi rispetto al record di feedback.

    ![Elenco transazioni distorte](images/Confusion_Matrix_040819.006.png)

1. Le transazioni appaiono in linea.

    ![Elenco transazioni distorte](images/Confusion_Matrix_040819.007.png)

