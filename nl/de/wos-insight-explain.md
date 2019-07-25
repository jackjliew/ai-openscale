---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: explainability, monitoring, explain, explaining, transactions, transaction ID

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Transaktionen erklären
{: #ie-ov}

Für jede Bereitstellung können Sie Erklärungsdaten für bestimmte Transaktionen anzeigen.
{: shortdesc}

## Transaktionen erklären
{: #ie-view}

Wählen Sie in der Kachel für die ausgewählte Bereitstellung im Navigator die Registerkarte **Transaktion erklären** (![Registerkarte 'Transaktion erklären'](images/insight-transact-tab.png)) aus und geben Sie eine Transaktions-ID ein.

Wann immer Daten zwecks Scoring an das Modell gesendet werden, legt es eine Transaktions-ID im HTTP-Header fest, indem es das Feld `X-Global-Transaction-Id` entsprechend angibt. Diese Transaktions-ID wird in der Nutzdatentabelle gespeichert. Wenn Sie eine Erklärung des Modellverhaltens für ein bestimmtes Scoring suchen, geben Sie die Transaktions-ID an, die dieser Scoring-Anforderung zugeordnet ist. Beachten Sie bitte, dass dieses Verhalten nur {{site.data.keyword.pm_full}}-Transaktionen betrifft und nicht für andere Transaktionen (Nicht-WML-Transaktionen) gilt.
{: note}

### Transaktions-ID in {{site.data.keyword.aios_short}} suchen
{: #ie-find}

1.  Verschieben Sie die Markierung im Zeitdiagramm für Ihre Bereitstellung über das Diagramm und klicken Sie auf den Link **Details anzeigen**, um eine [Visualisierung von Daten eine bestimmte Uhrzeit](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet) anzuzeigen.
1.  Klicken Sie auf die Schaltfläche **Transaktionen anzeigen**, um die [Liste der Transaktions-IDs anzuzeigen](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra).
1.  Kopieren Sie eine der Transaktions-IDs aus der Liste, fügen Sie sie in das Suchfeld auf der Seite **Transaktion erklären** ein und drücken Sie die Eingabetaste.

    Die Liste der Transaktions-IDs bietet auch die Möglichkeit, für eine beliebige Transaktions-ID in der Spalte 'Aktion' einfach auf den Link **Erklären** zu klicken, woraufhin diese Transaktion in der Registerkarte 'Erklärbarkeit' geöffnet wird.
    {: note}

  Die den folgenden Abschnitten enthalten Beispiele für Erklärungen zu verschiedenen Modelltypen.

  ![Transaktions-ID für Erklärbarkeit](images/insight-explain-trans-id.png)

## Beispiel eines kategorialen Modells
{: #ie-class}

Dieses Beispiel für Erklärbarkeit bezieht sich auf ein binäres Klassifizierungsmodell, das Versicherungsansprüche freigibt oder ablehnt. Sie können die Faktoren sehen, die in diesem Fall positiv oder negativ zum Endergebnis `ABGELEHNT` beigetragen haben.

Das Merkmal *ALTER POLICE* mit dem Wert `< 1 year` übte den größten Einfluss auf die Entscheidung des Modells zugunsten von ABGELEHNT als Ergebnis aus. Die anderen Merkmale, die zu diesem Ergebnis beigetragen haben, waren *SCHADENSHÄUFIGKEIT* (`Hoch`) und *ALTER* (`18`), wobei *FAHRZEUGWERT* (`$50,000`) nur einen geringfügigen Einfluss hatte.

![Erklärbarkeit bei binärer Klassifizierung](images/insight-explain-binary.png)

Die Diagramme sind zwar nützlich zur Darstellung der wichtigsten Faktoren bei der Bestimmung des Ergebnisses einer Transaktion, doch Klassifizierungsmodelle können auch erweiterte Erklärungen enthalten, die in den Abschnitten `Mindeständerungen für Ergebnis 'Genehmigt'` und `Mindeständerungen für dieses Ergebnis` detailliert beschrieben sind.

Erweiterte Erklärungen stehen nicht für Regressions- oder Imagemodelle und Modelle für unstrukturierten Text zur Verfügung.
{: note}

`Mindeständerungen für Ergebnis 'Genehmigt'` besagt, dass sich die Vorhersage des Modells ändern würde, wenn die Werte der Merkmale in die in diesem Abschnitt aufgeführten Werte geändert würden.

`Mindeständerungen für dieses Ergebnis` besagt hingegen, dass sich die Vorhersage des Modells nicht ändern würde, selbst wenn die Werte der Merkmale in die in diesem Abschnitt aufgeführten Werte geändert würden.

Diese beiden Werte geben Auskunft über das Verhalten des Modells im Umkreis des Datenpunktes mit, für den die Erklärung generiert wird.

![Erklärbarkeit bei binärer Klassifizierung](images/insight-explain-binary2.png)

## Imagemodelle
{: #ie-image}

{{site.data.keyword.aios_short}} unterstützt die Erklärbarkeit für Imagedaten.

### Mit einem Imagemodell arbeiten
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

### Imagemodelltransaktionen erklären
{: #ie-image-workingviewing}

Am folgenden Beispiel für die Erklärbarkeit bei einem Imageklassifizierungsmodell können Sie ablesen, welche Teile eines Images positiv zum vorhergesagten Ergebnis beigetragen haben und welche negativ. Im folgenden Beispiel stellt das Image im als positiv gekennzeichneten Fenster die Teile dar, die sich positiv auf die Vorhersage ausgewirkt haben, und das Image im als negativ gekennzeichneten Fenster zeigt die Teile des Image an, deren Auswirkung auf das Ergebnis negativ war.

![Erklärbarkeit bei Imageklassifikation](images/insight-explain-image.png)

Für {{site.data.keyword.pm_full}} kann die Scoring-Eingabe für Imageklassifizierungsmodelle, die zur Nutzdatenprotokollierung gesendet werden, eine Größe von 1 MB nicht überschreiten. Um Probleme aufgrund von Zeitlimitüberschreitungen zu vermeiden, dürfen Images nicht mehr als 125 x 125 Pixel aufweisen und sie müssen nacheinander gesendet werden, damit die Erklärung für das zweite Image angefordert wird, nachdem die erste abgeschlossen ist.
{: note}


### Beispiele für Imagemodelle
{: #ie-image-working-ntbks}

Verwenden Sie die folgenden beiden Notebooks, um detaillierte Codebeispiele anzuzeigen und eigene {{site.data.keyword.aios_short}}-Bereitstellungen zu entwickeln:

- [Lernprogramm zum Generieren einer Erklärung für ein imagebasiertes Modell](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/image_explanation.ipynb){: external}
- [Lernprogramm zum Generieren einer Erklärung für ein imagebasiertes binäres Klassifizierungsmodell](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/image_explanation_binary.ipynb){: external}


## Modelle für unstrukturierten Text
{: #ie-unstruct}

{{site.data.keyword.aios_short}} unterstützt die Erklärbarkeit für Modelle für unstrukturierten Text.

### Mit Modellen für unstrukturierten Text arbeiten
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

### Transaktionen mit unstrukturiertem Text erklären
{: #ie-unstruct-xplan}

Bei dem folgenden Beispiel für Erklärbarkeit wird ein Klassifizierungsmodell gezeigt, das unstrukturierten Text auswertet. Die Erklärung zeigt die Schlüsselwörter an, die sowohl einen positiven als auch einen negativen Einfluss auf die Modellvorhersage hatten. Außerdem wird die Position der ermittelten Schlüsselwörter auch im Originaltext angezeigt, der dem Modell als Eingabe zugeführt wurde.

![Erklärbarkeit bei Imageklassifikation](images/insight-explain-text.png)

### Beispiel eines Modells für unstrukturierten Text
{: #ie-unstruct-ntbkssample}

Verwenden Sie das folgende Notebook, um detaillierte Codebeispiele anzuzeigen und eigene {{site.data.keyword.aios_short}}-Bereitstellungen zu entwickeln:

- [Lernprogramm zum Generieren einer Erklärung für ein textbasiertes Modell](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/text_explanation.ipynb){: external}

## Kontrastierende Erklärungen verwenden relevante positive und relevante negative Werte.
{: #ie-pp-pn}

Bei kontrastiven Erklärungen zeigt {{site.data.keyword.aios_short}} immer relevante positive und relevante negative Werte an. 

- Relevante positive Werte sind die Ergebnisse, die bei der Ermittlung eines Gegenstands oder Sachverhalts von entscheidender Bedeutung sind.
- Relevante negative Werte sind die Nicht-Ergebnisse, die durch ihre Abwesenheit von Bedeutung sind.

{{site.data.keyword.aios_short}} zeigt immer einen relevanten positiven Wert an, in einigen Fällen werden jedoch keine relativen negativen Werte angezeigt. In diesem Fall sind Werte für das jeweilige Merkmal entweder bereits gemittelt oder die Vorhersage hat sich durch das Entfernen von Werten vom Mittelwert nicht geändert.

Dies ist leichter zu verstehen, wenn man bedenkt, dass {{site.data.keyword.aios_short}} beim Berechnen des relativen negativen Werts die Werte aller Merkmale vom zugehörigen Mittelwert entfernt werden. Bei relevanten negativen Werten handelt es sich dabei um die Merkmalwerte, die am weitesten vom Mittelwert entfernt sind. Befinden sich die Werte eines Datenpunkts bereits auf dem Mittelwert oder ändert sich die Vorhersage auch nach dem Ändern des Werts in einen vom Mittelwert entfernten Wert nicht, gibt es keine relativen negativen Werte, die anzuzeigen sind. Im Hinblick auf relevante positive Werte findet {{site.data.keyword.aios_short}} die maximale Änderung bei den Merkmalwerten nahe dem Mittelwert, sodass sich die Vorhersage nicht ändert. Dies bedeutet in der Praxis, dass es fast immer einen relevanten positiven Wert gibt, der eine Transaktion erklärt.

