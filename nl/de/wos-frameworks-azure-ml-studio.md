---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits, azure, studio

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

# Microsoft Azure ML Studio-Frameworks
{: #frmwrks-azure}

{{site.data.keyword.aios_full}} unterstützt die folgenden Microsoft Azure Machine Learning Studio-Frameworks vollständig:
{: shortdesc}

Tabelle 1. Details der Frameworkunterstützung

| Framework | Problemtyp | Datentyp |
|:---|:---:|:---:|
| Nativ | Klassifizierung | Strukturiert |
{: caption="Details der Frameworkunterstützung" caption-side="top"}

## Microsoft Azure ML Studio zu {{site.data.keyword.aios_short}} hinzufügen
{: #frmwrks-azure-add}

Sie können {{site.data.keyword.aios_short}} auf eine der folgenden Weisen für die Verwendung von Microsoft Azure ML Studio konfigurieren:

- Wenn Sie zum ersten Mal einen Machine Learning-Anbieter zu {{site.data.keyword.aios_short}} hinzufügen, können Sie die Konfigurationsschnittstelle verwenden. Weitere Informationen finden Sie im Abschnitt [Microsoft Azure ML Studio-Instanz angeben](/docs/services/ai-openscale?topic=ai-openscale-connect-azure).
- Sie können Ihren Machine-Learning-Anbieter auch mithilfe des Python-SDK hinzufügen. Diese Methode müssen Sie verwenden, wenn mehrere Anbieter zur Verfügung stehen sollen. Wenn Sie diesen Schritt programmgesteuert ausführen möchten, finden Sie weitere Informationen in [Bindung für Microsoft Azure-Machine Learning-Engine erstellen](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind).


## Beispielnotebooks
{: #frmwrks-azure-smpl-ntbks}

Die folgenden Notebooks enthalten Informationen zur Verwendung von Microsoft Azure ML Studio:

- [Datamart-Erstellung, Überwachung der Modellbereitstellung und Datenanalyse](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}
- [Scoring-Beispiele für MS Azure Service-Modelle](https://dataplatform.cloud.ibm.com/analytics/notebooks/v2/0d4ebd8d-87cb-4c38-8ba8-37f5623df131/view?access_token=fcb2c411aed913bf94f86f434184db67aef1a6b304824b86b4ad63686e4890be){: external}

## Weiterführende Informationen
{: #frmwrks-azure-mediumblogs}

- [Azure Machine Learning mit Watson OpenScale überwachen](https://developer.ibm.com/patterns/monitor-azure-machine-learning-studio-models-with-ai-openscale/){: external}
- [Wie unterscheidet sich Azure Machine Learning Service von Studio?](https://docs.microsoft.com/en-us/azure/machine-learning/service/overview-what-is-azure-ml#how-does-azure-machine-learning-service-differ-from-studio){: external}
- [Als Web-Service bereitgestelltes Azure Machine Learning-Modell verarbeiten](https://docs.microsoft.com/en-us/azure/machine-learning/service/how-to-consume-web-service){: external}
