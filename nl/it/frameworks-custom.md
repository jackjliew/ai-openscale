---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: supported frameworks, models, model types, limitations, limits, custom machine learning engine, custom

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

# Framework ML personalizzati
{: #frmwrks-custom}

{{site.data.keyword.aios_full}} supporta completamente i seguenti framework machine learning personalizzati:
{: shortdesc}

Tabella 1. Dettagli supporto framework

| Framework | Tipo di problema | Tipo di dati |
|:---|:---:|:---:|
| Equivalente a {{site.data.keyword.pm_full}} | Classificazione | Strutturato |
{: caption="Dettagli supporto framework" caption-side="top"}

## Aggiunta di un motore di machine learning personalizzato a {{site.data.keyword.aios_short}}
{: #frmwrks-custom-add}

È possibile configurare {{site.data.keyword.aios_short}} per lavorare con un provider di machine learning personalizzato utilizzando uno dei seguenti metodi:

- Se è la prima volta che si aggiunge un provider di machine learning personalizzato a {{site.data.keyword.aios_short}}, è possibile utilizzare l'interfaccia di configurazione. Per ulteriori informazioni, consultare [Specifica di un'istanza di machine learning personalizzata](/docs/services/ai-openscale?topic=ai-openscale-co-connect).
- È anche possibile aggiungere il provider di machine learning utilizzando l'SDK Python. È necessario utilizzare questo metodo se si desidera avere più di un provider. Per ulteriori informazioni sull'esecuzione programmatica di questa azione, consultare [Collegare il motore di machine learning personalizzato](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-cusbind).


## Notebook di esempio
{: #frmwrks-custom-smpl-ntbks}

- [Creazione del motore di machine learning utilizzando il cluster Kubernetes](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix){: external}
- [Creazione data mart, monitoraggio distribuzione modello e analisi dati](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}

## Scopri di più
{: #frmwrks-custom-mediumblogs}

[Monitorare il motore di machine learning personalizzato con Watson OpenScale](https://developer.ibm.com/patterns/monitor-custom-machine-learning-engine-with-ai-openscale/){: external}
