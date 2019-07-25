---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

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

# Angepasste ML-Frameworks
{: #frmwrks-custom}

{{site.data.keyword.aios_full}} unterstützt die folgenden angepassten ML-Frameworks vollständig:
{: shortdesc}

Tabelle 1. Details der Frameworkunterstützung

| Framework | Problemtyp | Datentyp |
|:---|:---:|:---:|
| Äquivalent zu {{site.data.keyword.pm_full}} | Klassifizierung | Strukturiert |
{: caption="Details der Frameworkunterstützung" caption-side="top"}

## Angepasste Machine Learning-Engine zu {{site.data.keyword.aios_short}} hinzufügen
{: #frmwrks-custom-add}

Sie können {{site.data.keyword.aios_short}} auf eine der folgenden Weisen für die Verwendung eines Anbieters für angepasstes Machine Learning konfigurieren:

- Wenn Sie zum ersten Mal einen Anbieter für angepasstes Machine Learning zu {{site.data.keyword.aios_short}} hinzufügen, können Sie die Konfigurationsschnittstelle verwenden. Weitere Informationen finden Sie im Abschnitt [Angepasste Machine Learning-Instanz angeben](/docs/services/ai-openscale?topic=ai-openscale-co-connect).
- Sie können Ihren Machine-Learning-Anbieter auch mithilfe des Python-SDK hinzufügen. Diese Methode müssen Sie verwenden, wenn mehrere Anbieter zur Verfügung stehen sollen. Wenn Sie diesen Schritt programmgesteuert ausführen möchten, finden Sie weitere Informationen in [Bindung für angepasste Machine Learning-Engine erstellen](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-cusbind).


## Beispielnotebooks
{: #frmwrks-custom-smpl-ntbks}

- [Erstellung einer angepassten Machine Learning-Engine mit dem Kubernetes-Cluster](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix){: external}
- [Datamart-Erstellung, Überwachung der Modellbereitstellung und Datenanalyse](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}

## Weiterführende Informationen
{: #frmwrks-custom-mediumblogs}

[Angepasste Machine Learning-Engine mit Watson OpenScale überwachen](https://developer.ibm.com/patterns/monitor-custom-machine-learning-engine-with-ai-openscale/){: external}
