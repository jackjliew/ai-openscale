---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: fairness, fairness monitor, payload, perturbation, training data, debiased

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

# Builder di grafici ![tag beta](images/beta.png)
{: #chart_builder}

Utilizzare il builder di grafici di {{site.data.keyword.aios_short}}  per creare visualizzazioni personalizzate, in modo da comprendere meglio le previsioni del modello e gli input al runtime. Il builder di grafici fornisce la possibilità di visualizzare l'output della previsione del modello rispetto alle funzioni o agli intervalli di dati che un'azienda considera importanti. Aiuta a scoprire nuovi andamenti nei dati che potrebbero indurre l'azienda e i team di data science a prendere in considerazione la modifica del modello AI.
{: shortdesc}

Ad esempio, se si ha familiarità con il modello di rischio di credito dai supporti didattici, è possibile vedere la suddivisione in classi previste per intervalli diversi dell'attributo Credit History. 

   ![un grafico che mostra la funzione previsione per il genere in base alla funzione età](images/by_custom_chart.png)
      
   Si può anche vedere quanto sia attendibile il modello, quando si esegue la previsione per questi intervalli di Credit History. È possibile analizzare il payload del calcolo del punteggio che viene inviato alla propria distribuzione nell'intervallo di dati selezionato in base al grafico personalizzato (selezionando tra le funzioni, le classi di previsione e la confidenza. 

   ![un grafico che mostra la funzione previsione per il genere in base alla funzione età](images/by_custom_chart002.png)
   
