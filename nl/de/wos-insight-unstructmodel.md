---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: fairness, monitoring, charts, de-biasing, bias, accuracy

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

# Modelle mit unstrukturiertem Text erklären
{: #ie-unstruct}

{{site.data.keyword.aios_short}} unterstützt die Erklärbarkeit für unstrukturierte Textdaten.
{: shortdesc}

## Mit Modellen für unstrukturierten Text arbeiten
{: #ie-unstruct-steps}

1. Richten Sie die Umgebung ein.
   2. Installieren Sie die Pakete {{site.data.keyword.aios_short}} und {{site.data.keyword.pm_full}}.
   3. Konfigurieren Sie die Berechtigungsnachweise.
   4. Installieren Sie die Bibliotheken, die für die Erstellung der Modelle und die Ausführung von Analysen erforderlich sind. Hierzu gehören die folgenden Bibliotheken:
      - `pandas`
      - `pyspark` (wenn {{site.data.keyword.DSX}} nicht verwendet wird)

1. Erstellen Sie das imagebasierte Modell und stellen Sie es bereit.
   2. Laden Sie Trainingsdaten in einen Pandas-Rahmen.
   2. Trainieren Sie das Modell mit den Daten.
   3. Veröffentlichen Sie das Modell.
   4. Stellen Sie das Modell bereit und führen Sie das Scoring durch.

7. Konfigurieren Sie {{site.data.keyword.aios_short}}, indem Sie den API-Client (`APIClient`) zuordnen, das Asset abonnieren und das Scoring für das Modell durchführen.
8. Konfigurieren Sie die Erklärbarkeit.
   9. Aktivieren Sie die Erklärbarkeit.
   10. Rufen Sie Erklärungen für die Transaktionen ab.

## Transaktionen mit unstrukturiertem Text erklären
{: #ie-unstruct-xplan}

Bei dem folgenden Beispiel für Erklärbarkeit wird ein Klassifizierungsmodell gezeigt, das unstrukturierten Text auswertet. Die Erklärung zeigt die Schlüsselwörter an, die sowohl einen positiven als auch einen negativen Einfluss auf die Modellvorhersage hatten. Außerdem wird die Position der ermittelten Schlüsselwörter auch im Originaltext angezeigt, der dem Modell als Eingabe zugeführt wurde.

![Ein Diagramm zur Imageklassifikation für Erklärbarkeit wird dargestellt; es zeigt Konfidenzniveaus für den unstrukturierten Text](images/insight-explain-text.png)

## Beispiel eines Modells für unstrukturierten Text
{: #ie-unstruct-ntbkssample}

Verwenden Sie das folgende Notebook, um detaillierte Codebeispiele anzuzeigen und eigene {{site.data.keyword.aios_short}}-Bereitstellungen zu entwickeln:

- [Lernprogramm zum Generieren einer Erklärung für ein textbasiertes Modell](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/text_explanation.ipynb){: external}

