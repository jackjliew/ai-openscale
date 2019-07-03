---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: supported frameworks, models, model types, limitations, limits, azure

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

# Framework per Microsoft Azure ML Service
{: #frmwrks-azure-service}

{{site.data.keyword.aios_full}} supporta completamente i seguenti framework Microsoft Azure Machine Learning Service:
{: shortdesc}

Tabella 1. Dettagli supporto framework

| Framework | Tipo di problema | Tipo di dati |
|:---|:---:|:---:|
| Nativo | Classificazione | Strutturato |
{: caption="Dettagli supporto framework" caption-side="top"}

## Aggiunta di Microsoft Azure ML Service a {{site.data.keyword.aios_short}}
{: #frmwrks-azure-add}

È possibile configurare {{site.data.keyword.aios_short}} per lavorare con Microsoft Azure ML Service utilizzando uno dei seguenti metodi:

- Se è la prima volta che si aggiunge un provider di machine learning a {{site.data.keyword.aios_short}}, è possibile utilizzare l'interfaccia di configurazione. Per ulteriori informazioni, consultare [Specifica di un'istanza Microsoft Azure ML Studio](/docs/services/ai-openscale?topic=ai-openscale-connect-azure).
- È anche possibile aggiungere il provider di machine learning utilizzando l'SDK Python. È necessario utilizzare questo metodo se si desidera avere più di un provider. Per ulteriori informazioni sull'esecuzione programmatica di questa azione, consultare [Collegare il motore di machine learning Microsoft Azure](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind).


Caricare il payload utente necessario per i metadati.
Create the model
onboarding UI to configure monitoring for
upload training data / notebook openscale needs info
run payload logging,
UI - refresh

Onus on implementer 

MJS: Follow up with Lukasz & Clifford Chu

A

## Notebook di esempio
{: #frmwrks-azure-smpl-ntbks}

I seguenti notebook mostrano come operare con Microsoft Azure ML Service:

- [Creazione data mart, monitoraggio distribuzione modello e analisi dati](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}
- [Esempi di calcolo del punteggio del modello MS Azure Service](https://dataplatform.cloud.ibm.com/analytics/notebooks/v2/0d4ebd8d-87cb-4c38-8ba8-37f5623df131/view?access_token=fcb2c411aed913bf94f86f434184db67aef1a6b304824b86b4ad63686e4890be){: external}

## Scopri di più
{: #frmwrks-azure-mediumblogs}

[Monitorare il machine learning Azure con Watson OpenScale](https://developer.ibm.com/patterns/monitor-azure-machine-learning-studio-models-with-ai-openscale/){: external}
