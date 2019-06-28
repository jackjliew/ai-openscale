---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Angepasste Überwachungen und Metriken erstellen ![Beta-Tag](images/beta.png)
{: #cst_mtrcs}

Mit angepassten Überwachungen wird eine Gruppe angepasster Metriken konsolidiert, die Ihnen die quantitative Verfolgung beliebiger Aspekte Ihrer Modellbereitstellung und Geschäftsanwendung ermöglichen. Sie können angepasste Metriken definieren und sie zusammen mit den Standardmetriken, wie z. B. Modellqualitäts-, Leistungs- oder Fairnessmetriken, verwenden, die in {{site.data.keyword.aios_full}}überwacht werden.
{: shortdesc}

Um angepasste Überwachungen und Metriken zu verwalten, müssen Sie die programmgesteuerte Schnittstelle verwenden, die Teil des Python-SDK ist. Entsprechend können Sie angepasste Metriken im {{site.data.keyword.aios_short}}-Datamart speichern und bei Bedarf darauf zugreifen. Angepasste Metriken werden auch im {{site.data.keyword.aios_short}}-Dashboard visualisiert.

## Angepasste Metriken verwalten
{: #cst_mtrc_mgmt}

Führen Sie die folgenden Tasks aus, um mit angepassten Metriken zu arbeiten:

1. Registrieren Sie die angepasste Überwachung mit der Metrikdefinition.
2. Aktivieren Sie die angepasste Überwachung.
3. Speichern Sie die Metrikwerte.

In den folgenden Lernprogrammen für Fortgeschrittene wird die Vorgehensweise veranschaulicht:

- [Mit Watson Machine Learning arbeiten](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine.ipynb)
- [Mit der angepassten Machine Learning-Engine arbeiten](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb)

Sie können die angepasste Überwachung jederzeit inaktivieren und wieder aktivieren. Wenn Sie die angepasste Überwachung nicht mehr benötigen, können Sie sie entfernen.

Weitere Informationen finden Sie in der [Dokumentation zum Python-SDK](http://ai-openscale-python-client.mybluemix.net/).

## Auf angepasste Metriken zugreifen und diese visualisieren
{: #cst_mtrcs_viz}

Sie können eine programmgesteuerte Schnittstelle verwenden, um auf angepasste Metriken zuzugreifen und diese zu visualisieren. In den folgenden Lernprogrammen für Fortgeschrittene wird die Vorgehensweise veranschaulicht:

- [Mit Watson Machine Learning arbeiten](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine.ipynb)
- [Mit der angepassten Machine Learning-Engine arbeiten](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb)

   Weitere Informationen finden Sie in der [Dokumentation zum Python-SDK](http://ai-openscale-python-client.mybluemix.net/).

Visualisierungen der angepassten Metriken werden auch im {{site.data.keyword.aios_short}}-Dashboard angezeigt.

<!---
![screen shot with metrics from Advanced Tutorial](images/adv_tutorial_metrics.png)
--->
