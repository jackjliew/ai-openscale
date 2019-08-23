---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: accuracy, 

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

# Configurazione del monitor Qualità (Accuratezza)
{: #acc-monitor}

Il monitor Qualità (precedentemente noto come monitor Accuratezza) consente di sapere come il modello prevede i risultati.
{: shortdesc}

## Procedura di configurazione
{: #acc-config}

Dalla scheda **Qualità**, sulla pagina **Cos'è il monitor Qualità?** fare clic su **Inizia** per avviare il processo di configurazione.

![viene visualizzata la pagina Cos'è il monitor Qualità? che spiega che il monitor qualità valuta in che modo il modello prevede risultati accurati](images/wos-quality-what-is.png)

Configurare le seguenti impostazioni sulle pagine successive della scheda di configurazione dell'accuratezza:

-  Impostare la soglia di avviso dell'accuratezza. Selezionare un valore che rappresenti un livello di accuratezza accettabile. Ad esempio, se si sta utilizzando il **modello German Credit Risk** per il supporto didattico interattivo, impostare l'avviso su **90%**.

    L'accuratezza è un valore sintetizzato da pertinenti metriche di data science associate a ciascun tipo di modello particolare. Il punteggio è una misura normalizzata per consentire di confrontare facilmente l'accuratezza tra i diversi tipi di modelli. In situazioni tipiche, è sufficiente un punteggio di accuratezza di 80. Per il supporto didattico, per generare più dati, consigliamo 90.
    {: note}

-  Impostare la dimensione minima e massima del campione. La dimensione minima impedisce di misurare l'accuratezza fino a che non è disponibile un numero minimo di record nel dataset di valutazione; questo assicura che la dimensione del campione non sia troppo piccola per l'asimmetria dei risultati. La dimensione massima del campione facilita la gestione del tempo e dello sforzo richiesti per valutare il dataset; se viene superata questa  dimensione verranno valutati solo i record più recenti. Ad esempio, se si utilizza il **modello German Credit Risk** per il supporto didattico interattivo, impostare la dimensione minima del campione su **100** e la dimensione massima del campione su **10000**.


Viene visualizzato un riepilogo delle selezioni per la revisione. Se si desidera modificare qualsiasi cosa, fare clic sul link **Modifica** per quella sezione. Altrimenti, fare clic su **Salva** per completare la configurazione.

### Passi successivi
{: #acc-next}

Per continuare la configurazione dei monitor, fare clic sulla scheda **Correttezza** e fare clic su **Inizia**. Per ulteriori informazioni, consultare [Configurazione del monitor Correttezza](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor).
