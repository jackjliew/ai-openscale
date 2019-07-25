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

# Überwachung der Drifterkennung konfigurieren
{: #behavior-drift-config}

Sie müssen die Überwachung der Drifterkennung in {{site.data.keyword.aios_full}} konfigurieren, bevor diese mit der Analyse des Modells beginnen kann. Zwei Möglichkeiten stehen zur Auswahl: Sie können das Modell online trainieren oder ein Notebook verwenden.
{: shortdesc}

Sie können Ihr Modell mit {{site.data.keyword.aios_short}} online trainieren, wenn Sie {{site.data.keyword.pm_full}} verwenden und Ihre Daten 500 MB nicht überschreiten. Andernfalls müssen Sie zum Trainieren Ihres Modells ein Notebook verwenden.

## Schritte zur Konfiguration der Drifterkennung in {{site.data.keyword.aios_short}}
{: #behavior-drift-config-steps-wos}

Bei der Verwendung von {{site.data.keyword.pm_full}} steht Ihnen die Option zur Verfügung, die Drifterkennung über die {{site.data.keyword.aios_short}}-Benutzerschnittstelle zu konfigurieren.

1. Klicken Sie auf der Registerkarte **Drift** auf der Seite **Was ist Drift?** auf **Starten**, um den Konfigurationsprozess zu starten.

   ![Seite 'Was ist Drift?'](images/drift-config-1.png)

2. Klicken Sie auf die Kachel **In Watson OpenScale trainieren**.

   ![Seite 'Was ist Drift?'](images/drift-config-2.png)

3. Legen Sie den Alertschwellenwert fest.

   ![Seite 'Was ist Drift?'](images/drift-config-3.png)

3. Legen Sie die Stichprobengröße fest.

   ![Seite 'Was ist Drift?'](images/drift-config-4.png)
   
3. Klicken Sie auf **Speichern**.


## Schritte zur Konfiguration der Drifterkennung mithilfe eines Notebooks
{: #behavior-drift-config-steps-ntbk}

Bei anderen Machine Learning-Engines als {{site.data.keyword.pm_full}}, z. B. Microsoft Azure, Amazon SageMaker oder einer angepassten Machine Learning-Engine, müssen Sie die Drifterkennung über ein Notebook konfigurieren. Auf diese Weise können Sie auch die Drift selbst für {{site.data.keyword.pm_full}} konfigurieren.

Diese Option ist hilfreich, wenn die Trainingsdaten nicht in Db2 oder {{site.data.keyword.cos_full}} gespeichert sind. Wenn Sie ein Notebook verwenden, müssen Sie die Trainingsdaten mit einem Lesezugriff in einen Datenrahmen laden. Das speziell dafür konzipierte Notebook, das Sie von {{site.data.keyword.aios_short}} herunterladen können, erstellt dann eine spezielle Ausgabe, die Sie in {{site.data.keyword.aios_short}} hochladen können.

1. Erstellen Sie ein Notebook, um das Drifterkennungsmodell zu generieren. Verwenden Sie das [Beispielnotebook](https://github.com/IBM-Watson/aios-data-distribution/blob/master/training_statistics_notebook.ipynb), das in der {{site.data.keyword.aios_short}}-Benutzerschnittstelle zur Verfügung steht.
2. Komprimieren Sie das Drifterkennungsmodell mit einer Komprimierungssoftware in einer .TAR.GZ-Datei.

1. Klicken Sie auf der Registerkarte **Drift** auf der Seite **Was ist Drift?** auf **Starten**, um den Konfigurationsprozess zu starten.

   ![Seite 'Was ist Drift?'](images/drift-config-1.png)

2. Klicken Sie auf die Kachel **In einem Notebook trainieren**.

   ![Seite 'Was ist Drift?'](images/drift-config-2.png)

3. Ziehen Sie die komprimierte Modelldatei in die Zielzone oder wählen Sie sie aus und klicken Sie dann auf **Weiter**.

   ![Seite 'Was ist Drift?'](images/drift-config-2b.png)
   
3. Laden Sie das Drifterkennungsmodell hoch und klicken Sie auf **Weiter**.

   ![Seite 'Was ist Drift?'](images/drift-config-upload.png)
   
3. Legen Sie den Alertschwellenwert fest.

   ![Seite 'Was ist Drift?'](images/drift-config-3.png)

3. Legen Sie die Stichprobengröße fest.

   ![Seite 'Was ist Drift?'](images/drift-config-4.png)
   
3. Klicken Sie auf **Speichern**.

## Weitere Schritte
{: #behavior-drift-config-next-steps}

- Machen Sie sich anhand der [Erläuterungen zum Modelldrift mit IBM Watson OpenScale](https://medium.com/@manish.bhide/4c5401aa8da4) mit dem Potenzial der Drifterkennung vertraut.
