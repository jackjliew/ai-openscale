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

# Imagemodelle erklären
{: #ie-image}

{{site.data.keyword.aios_short}} unterstützt die Erklärbarkeit für Imagedaten.
{: shortdesc}

## Mit einem Imagemodell arbeiten
{: #ie-image-working}

1. Richten Sie die Umgebung ein.
   2. Installieren Sie die Pakete {{site.data.keyword.aios_short}} und {{site.data.keyword.pm_full}}.
   3. Konfigurieren Sie die Berechtigungsnachweise.
   4. Installieren Sie die Bibliotheken, die für die Erstellung der Modelle und die Ausführung von Analysen erforderlich sind. Hierzu gehören die folgenden Bibliotheken:
      - `keras`
      - `tensorflow`
      - `keras_sequential_ascii`
      - `numpy`
      - `pillow`

1. Erstellen Sie das imagebasierte Modell und stellen Sie es bereit.
   2. Erstellen Sie Ordner für die Images auf der Basis der Klassifizierung.
       - Innerhalb des Hauptverzeichnisses `data` müssen die Unterverzeichnisse `train` und `validation` vorhanden sein.
       - In jedem der Unterverzeichnisse müssen die Klassifizierungsverzeichnisse vorhanden sein.
  2. Standardisieren Sie die Imagegröße und legen Sie dann die Unterverzeichnisse fest, die für das Training und die Validierung verwendet werden sollen.
  3. Führen Sie eine Vorverarbeitung der Daten durch, um eine Größenänderung vorzunehmen und um die Images und die zugehörigen Klassen abzurufen.
  4. Definieren und trainieren Sie das Modell.
  5. Speichern Sie das Modell.
  6. Stellen Sie das Modell bereit.

7. Konfigurieren Sie {{site.data.keyword.aios_short}}, indem Sie den API-Client (`APIClient`) zuordnen, das Asset abonnieren und das Scoring für das Modell durchführen.
8. Konfigurieren Sie die Erklärbarkeit.
   9. Aktivieren Sie die Erklärbarkeit.
   10. Rufen Sie Erklärungen für die Transaktionen ab.
   11. Zeigen Sie die erklärten Images an. 

## Imagemodelltransaktionen erklären
{: #ie-image-workingviewing}

Am folgenden Beispiel für die Erklärbarkeit bei einem Imageklassifizierungsmodell können Sie ablesen, welche Teile eines Images positiv zum vorhergesagten Ergebnis beigetragen haben und welche negativ. Im folgenden Beispiel stellt das Image im als positiv gekennzeichneten Fenster die Teile dar, die sich positiv auf die Vorhersage ausgewirkt haben, und das Image im als negativ gekennzeichneten Fenster zeigt die Teile des Images an, dessen Auswirkung auf das Ergebnis negativ war.

![Darstellung von Imageklassifikation für Erklärbarkeit - Konfidenzdetail mit Abbildung eines Hundes mit teilweise hervorgehobenen Bildteilen, um zu zeigen, welcher Teil des Bildes geholfen hat zu bestimmen, dass es sich um einen Hund handelt](images/insight-explain-image.png)

Für {{site.data.keyword.pm_full}} darf die Scoring-Eingabe für Imageklassifizierungsmodelle, die zur Nutzdatenprotokollierung gesendet werden, ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling serviceMB nicht überschreiten. Um Probleme aufgrund von Zeitlimitüberschreitungen zu vermeiden, dürfen Images nicht mehr als 125 x 125 Pixel aufweisen und sie müssen nacheinander gesendet werden, damit die Erklärung für das zweite Image angefordert wird, nachdem die erste abgeschlossen ist.
{: note}


## Beispiele für Imagemodelle
{: #ie-image-working-ntbks}

Verwenden Sie die folgenden beiden Notebooks, um detaillierte Codebeispiele anzuzeigen und eigene {{site.data.keyword.aios_short}}-Bereitstellungen zu entwickeln:

- [Lernprogramm zum Generieren einer Erklärung für ein imagebasiertes Modell](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/image_explanation.ipynb){: external}
- [Lernprogramm zum Generieren einer Erklärung für ein imagebasiertes binäres Klassifizierungsmodell](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/image_explanation_binary.ipynb){: external}

