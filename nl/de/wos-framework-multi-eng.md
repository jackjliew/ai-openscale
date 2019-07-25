---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: multiple engines, non-Watson, machine learning, frameworks, provision

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

# Unterstützung für mehrere Machine Learning-Engines
{: #fmrk-workaround-multmleng}

{{site.data.keyword.aios_short}} unterstützt mehrere Machine Learning-Engines in einer einzigen Instanz. Sie können die Komponenten über die {{site.data.keyword.aios_short}}-Dashboardkonfiguration oder das [Python-SDK](http://ai-openscale-python-client.mybluemix.net/?cm_mc_uid=70732728440115575086192&cm_mc_sid_50200000=62539451560175957820) bereitstellen.
{: shortdesc}

Bei der erstmaligen Einrichtung von {{site.data.keyword.aios_short}} haben Sie möglicherweise die Benutzerschnittstelle oder die Option für die automatisierte Konfiguration verwendet, um Ihre erste Machine Learning-Engine bereitzustellen. Zum Hinzufügen von Machine Learning-Engines müssen Sie die Registerkarte 'Konfiguration' des {{site.data.keyword.aios_short}}-Dashboards oder das Python-SDK verwenden. 

## Anbieter über das Dashboard hinzufügen
{: #fmrk-workaround-multmleng-dashboard}

1. Klicken Sie nach dem Aufrufen von {{site.data.keyword.aios_short}} auf der Registerkarte **Konfigurieren** auf die Schaltfläche **Machine Learning-Anbieter hinzufügen**.

   ![Schaltfläche 'Anbieter hinzufügen' im Fenster für Machine Learning-Anbieter](images/wos-configure-multi-providers.png)

2. Klicken Sie auf die Kachel des gewünschten Anbieters und klicken Sie auf **Weiter**.

   ![Abbildung mit der Auswahlanzeige für Machine Learning-Anbieter](images/wos-machine-learning-providers-selection.png)

3. Geben Sie die erforderlichen Informationen, z. B. die Berechtigungsnachweise, ein und klicken Sie auf **Speichern**.

Nach dem Speichern der Konfiguration haben Sie die Möglichkeit, auf das Dashboard zurückzugreifen, Bereitstellungen auszuwählen oder die Überwachung zu konfigurieren.


## Machine Learning-Anbieter mit Python-SDK-Bindungsmethode hinzufügen
{: #fmrk-workaround-multmleng-binding}

Mit der Python-API-Methode `client.data_mart.bindings.add` können Sie mehr als eine Machine Learning-Engine an {{site.data.keyword.aios_short}} binden. 

### {{site.data.keyword.pm_full}}
{: #fmrk-workaround-multmleng-binding-wml}

- Führen Sie zum Binden der Machine Learning-Engine von {{site.data.keyword.pm_full}} den folgenden Befehl aus:

   `binding_uid = client.data_mart.bindings.add('WML instance', WatsonMachineLearningInstance(WML_CREDENTIALS))`

### Microsoft Azure ML Studio
{: #fmrk-workaround-multmleng-binding-azurestudio}

- Führen Sie zum Binden der Machine Learning-Engine von Azure ML Studio den folgenden Befehl aus:

  `binding_uid_2 = client.data_mart.bindings.add('My Azure ML Studio engine', AzureMachineLearningInstance(AZURE_ENGINE_CREDENTIALS))`

### Amazon Sagemaker
{: #fmrk-workaround-multmleng-binding-aws}

- Führen Sie zum Binden der Machine Learning-Engine von AWS Sagemaker den folgenden Befehl aus:

  `binding_uid_3 = client.data_mart.bindings.add('My AWS SageMaker engine', SageMakerMachineLearningInstance(SAGEMAKER_ENGINE_CREDENTIALS)) `

### Microsoft Azure ML Service
{: #fmrk-workaround-multmleng-binding-azureservice}

- Führen Sie zum Binden der Machine Learning-Engine von Azure ML Service den folgenden Befehl aus:

  `binding_uid_4 = client.data_mart.bindings.add('My Azure ML Service engine', AzureServiceMachineLearningInstance(AZURE_SRVR_ENGINE_CREDENTIALS))`

### Liste mit Machine Learning-Anbietern erzeugen
{: #fmrk-workaround-multmleng-binding-list}

Wenn Sie eine Liste aller Bindungen anzeigen möchten, führen Sie die Methode `list` aus:

`    client.data_mart.bindings.list()
    `


| UID | Name | Servicetyp | Erstellungszeitpunkt |
|:---|:---:|:---:|:---:
| e88ms###-####-####-############ | My Azure ML Service engine | azure_machine_learning | 2019-04-04T09:50:33.189Z |
| e88sl###-####-####-############ | My Azure ML Studio engine | azure_machine_learning | 2019-04-04T09:50:33.186Z |
| e00sjl###-####-####-############ | WML instance | watson_machine_learning | 2019-03-04T09:50:33.338Z |
| e43kl###-####-####-############ | My AWS SageMaker engine | sagemaker_machine_learning | 2019-04-04T09:50:33.186Z |
{: caption="Tabelle 1. Servicebindungen" caption-side="top"}


Informationen zu bestimmten Machine Learning-Engines enthalten die folgenden Abschnitte:

- [Bindung für angepasste Machine Learning-Engine erstellen](/docs/services/ai-openscale?topic=ai-openscale-cml-cusbind#cml-cusbind).
- [Bindung für Microsoft Azure Machine Learning Studio-Engine erstellen](/docs/services/ai-openscale?topic=ai-openscale-cml-azbind#cml-azbind)
- [Bindung für Microsoft Azure Machine Learning Service-Engine erstellen](/docs/services/ai-openscale?topic=ai-openscale-cml-azsrvconfig#cml-azsrvbind)
- [Bindung für Amazon SageMaker Machine Learning-Engine erstellen](/docs/services/ai-openscale?topic=ai-openscale-cml-smbind#cml-smbind)


Ein Arbeitsbeispiel eines tatsächlichen Notebooks enthalten die [{{site.data.keyword.aios_short}}-Beispielnotebooks](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks).

