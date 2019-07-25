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

# Genauigkeits- oder Qualitätsüberwachung konfigurieren
{: #acc-monitor}

Mithilfe der Qualitätsüberwachung (bisher unter der Bezeichnung 'Genauigkeitsüberwachung' bekannt) können Sie die Genauigkeit der von Ihrem Modell gelieferten Vorhersagen ermitteln.
{: shortdesc}

## Konfigurationsschritte
{: #acc-config}

Klicken Sie auf der Registerkarte **Genauigkeit** auf der Seite **Was ist Genauigkeit?** auf **Beginnen**, um den Konfigurationsprozess zu starten.

![Seite 'Was ist Genauigkeit?'](images/accuracy-what-is.png)

Konfigurieren Sie auf den nachfolgenden Seiten der Registerkarte 'Genauigkeit' die folgenden Einstellungen:

-  Legen Sie den Schwellenwert für Genauigkeitsalerts fest. Wählen Sie einen Wert aus, der eine akzeptable Genauigkeitsstufe liefert.

    Genauigkeit ist ein Wert, der aus relevanten Data-Science-Metriken, die jedem Modelltyp zugeordnet sind, synthetisch erstellt ist. Die Bewertung ist ein normalisiertes Maß, mit dem Sie die Genauigkeit unterschiedlicher Modelltypen ohne großen Aufwand miteinander vergleichen können. In typischen Situationen ist ein Genauigkeitswert von 80 ausreichend.
    {: note}

-  Legen Sie die minimale und die maximale Stichprobengröße fest. Der Mindeststichprobenumfang verhindert die Messung der Genauigkeit so lange, bis im Dataset für die Auswertung eine Mindestanzahl von Datensätzen zur Verfügung steht, um sicherzustellen, dass die Ergebnisse nicht etwa durch einen zu kleinen Stichprobenumfang verfälscht werden. Der Maximalstichprobenumfang hilft, den für die Datasetauswertung anfallenden Zeit- und Arbeitsaufwand besser zu steuern. Bei Überschreitung der Angabe für den Umfang werden nur die neuesten Datensätze ausgewertet.


Zur Überprüfung wird eine Zusammenfassung der von Ihnen getroffenen Auswahl angezeigt. Falls Sie Änderungen vornehmen möchten, klicken Sie für den betreffenden Abschnitt auf den Link **Bearbeiten**. Klicken Sie andernfalls zum Abschließen Ihrer Konfiguration auf **Speichern**.

### Weitere Schritte
{: #acc-next}

Auf der Seite **Überwachungen konfigurieren** können Sie eine weitere Überwachungskategorie auswählen.
