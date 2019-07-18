---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits, AWS, Sagemaker, Amazon

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

# Framework Amazon SageMaker
{: #frmwrks-aws-sage}

{{site.data.keyword.aios_full}} supporta completamente i seguenti framework Amazon SageMaker:
{: shortdesc}

Tabella 1. Dettagli supporto framework

| Framework | Tipo di problema | Tipo di dati |
|:---|:---:|:---:|
| Nativo | Classificazione | Strutturato |
{: caption="Dettagli supporto framework" caption-side="top"}


## Aggiunta di Amazon SageMaker a {{site.data.keyword.aios_short}}
{: #frmwrks-aws-sage-add}

È possibile configurare {{site.data.keyword.aios_short}} per lavorare con Amazon SageMaker utilizzando uno dei seguenti metodi:

- Se è la prima volta che si aggiunge un provider di machine learning a {{site.data.keyword.aios_short}}, è possibile utilizzare l'interfaccia di configurazione. Per ulteriori informazioni, consultare [Specifica di un'istanza Amazon SageMaker](/docs/services/ai-openscale?topic=ai-openscale-csm-connect).
- È anche possibile aggiungere il provider di machine learning utilizzando l'SDK Python. È necessario utilizzare questo metodo se si desidera avere più di un provider. Per ulteriori informazioni sull'esecuzione programmatica di questa azione, consultare [Collegare il motore di machine learning Amazon SageMaker](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind).


## Notebook di esempio
{: #frmwrks-aws-sage-smpl-ntbks}

I seguenti notebook mostrano come operare con Amazon SageMaker:

- [Creazione e distribuzione del modello di previsione del rischio di credito](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Credit%20%20model%20with%20SageMaker%20linear-learner%20.ipynb){: external}
- [Creazione data mart, monitoraggio distribuzione modello e analisi dati](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20SageMaker%20ML%20Engine.ipynb){: external}


## Scopri di più
{: #frmwrks-aws-sage-mediumblogs}

[Monitorare il machine learning Sagemaker con Watson OpenScale](https://developer.ibm.com/patterns/monitor-amazon-sagemaker-machine-learning-models-with-ai-openscale//){: external}
