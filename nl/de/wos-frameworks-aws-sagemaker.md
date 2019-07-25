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

# Amazon SageMaker-Frameworks
{: #frmwrks-aws-sage}

{{site.data.keyword.aios_full}} unterstützt die folgenden Amazon SageMaker-Frameworks vollständig:
{: shortdesc}

Tabelle 1. Details der Frameworkunterstützung

| Framework | Problemtyp | Datentyp |
|:---|:---:|:---:|
| Nativ | Klassifizierung | Strukturiert |
{: caption="Details der Frameworkunterstützung" caption-side="top"}


## Amazon SageMaker zu {{site.data.keyword.aios_short}} hinzufügen
{: #frmwrks-aws-sage-add}

Sie können {{site.data.keyword.aios_short}} auf eine der folgenden Weisen für die Verwendung von Amazon SageMaker konfigurieren:

- Wenn Sie zum ersten Mal einen Machine Learning-Anbieter zu {{site.data.keyword.aios_short}} hinzufügen, können Sie die Konfigurationsschnittstelle verwenden. Weitere Informationen hierzu finden Sie im Abschnitt [Amazon SageMaker-Instanz angeben](/docs/services/ai-openscale?topic=ai-openscale-csm-connect).
- Sie können Ihren Machine-Learning-Anbieter auch mit dem Python-SDK hinzufügen. Diese Methode müssen Sie verwenden, wenn mehrere Anbieter zur Verfügung stehen sollen. Wenn Sie diesen Schritt programmgesteuert ausführen möchten, finden Sie weitere Informationen in [Bindung für Amazon SageMaker-Machine Learning-Engine erstellen](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind).


## Beispielnotebooks
{: #frmwrks-aws-sage-smpl-ntbks}

Die folgenden Notebooks enthalten Informationen zur Verwendung von Amazon SageMaker:

- [Erstellen und Bereitstellen von Vorhersagemodellen für Kreditrisiken](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Credit%20%20model%20with%20SageMaker%20linear-learner%20.ipynb){: external}
- [Datamart-Erstellung, Überwachung der Modellbereitstellung und Datenanalyse](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20SageMaker%20ML%20Engine.ipynb){: external}


## Weiterführende Informationen
{: #frmwrks-aws-sage-mediumblogs}

[Sagemaker-Machine Learning mit Watson OpenScale überwachen](https://developer.ibm.com/patterns/monitor-amazon-sagemaker-machine-learning-models-with-ai-openscale//){: external}
