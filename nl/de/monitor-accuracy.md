---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

keywords: accuracy, 

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

# Genauigkeit
{: #acc-monitor}

Die Genauigkeit gibt an, wie gut Ihr Modell Ergebnisse vorhersagt.
{: shortdesc}

## Genauigkeit verstehen
{: #acc-understand}

Genauigkeit kann je nach Typ des Algorithmus unterschiedliche Dinge bedeuten:

- *Mehrklassige Klassifikation*: Die Genauigkeit misst die Zahl der korrekten Vorhersagen einer beliebigen Klasse bei Normalisierung der Anzahl der Datenpunkte.
Weitere Details hierzu enthält der Abschnitt [Mehrklassige Klassifikation ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#multiclass-classification){: new_window} in der Dokumentation für Apache Spark.

- *Binäre Klassifikation*: Bei einem Algorithmus für die binäre Klassifikation wird die Genauigkeit als die Fläche unter einer ROC-Kurve gemessen. Weitere Details hierzu enthält der Abschnitt [Binäre Klassifikation ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#binary-classification){: new_window} in der Dokumentation für Apache Spark.

- *Regression*: Regressionsalgorithmen werden mit dem Bestimmtheitskoeffizienten (R2) gemessen. Weitere Details hierzu enthält der Abschnitt [Auswertung von Regressionsmodellen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#regression-model-evaluation){: new_window} in der Dokumentation für Apache Spark.

### Funktionsweise
{: #acc-works}

Sie müssen wie unten gezeigt manuell bezeichnete Rückmeldedaten Über die Benutzerschnittstelle von {{site.data.keyword.aios_short}} mit einem [Python-Client ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://ai-openscale-python-client.mybluemix.net/#feedbacklogging){: new_window} oder einer [Rest-API ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/apidocs/ai-openscale#post-feedback-payload){: new_window} hinzufügen.

Informieren Sie sich in den Abschnitten [Unterstützte Modelltypen](/docs/services/ai-openscale?topic=ai-openscale-in-ov#in-mod) und [Unterstützte Frameworks](/docs/services/ai-openscale?topic=ai-openscale-in-ov#in-fram) über die Einschränkungen bei der Genauigkeitsüberwachung.

<!---
You need to add manually-labelled data into your feedback table for the accuracy computation to trigger. The feedback table is in the posgres schema with the name <model_id>_feedback.

You can create a performance monitoring system for your predictive models by creating an evaluation instance, and then defining the metrics and triggers for the automatic retraining and deploying of the new model. Spark, Keras and TensorFlow models are supported at this stage, with the following requirements:

- A training definition must be stored in the repository
- `training_data_reference` - must be defined as a part of the stored model's metadata
- `training_definition_url` - must be defined as a part of the stored model's metadata

Use the available [REST API ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://watson-ml-api.mybluemix.net/){: new_window} end-points directly to provide feedback data and kick off evaluation activities. For more information, see the [WML documentation ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://dataplatform.cloud.ibm.com/docs/content/analyze-data/ml-continuous-learning.html?audience=wdp&context=wdp){: new_window}.
--->

## Genauigkeitsüberwachung konfigurieren
{: #acc-config}

1.  Klicken Sie auf der Seite *Was ist Genauigkeit?* auf **Weiter**, um den Konfigurationsprozess zu starten.

    ![Seite 'Was ist Genauigkeit?'](images/accuracy-what-is.png)

1.  Wählen Sie auf der Seite *Genauigkeitsschwellenwert festlegen* einen Wert aus, der einen akzeptablen Genauigkeitsgrad darstellt.

    Genauigkeit ist ein Wert, der aus relevanten Data-Science-Metriken, die jedem Modelltyp zugeordnet sind, synthetisch erstellt ist. Die Bewertung ist ein normalisiertes Maß, mit dem Sie die Genauigkeit unterschiedlicher Modelltypen ohne großen Aufwand miteinander vergleichen können.  In typischen Situationen ist ein Genauigkeitswert von 80 ausreichend.
    {: note}

    ![Grenzwert für Genauigkeit festlegen](images/accuracy-set-limit.png)

    Klicken Sie zum Fortfahren auf **Weiter**.

1.  Legen Sie jetzt den Mindest- und den Maximalstichprobenumfang fest. Der Mindeststichprobenumfang verhindert die Messung der Genauigkeit so lange, bis im Dataset für die Auswertung eine Mindestanzahl von Datensätzen zur Verfügung steht, um sicherzustellen, dass die Ergebnisse nicht etwa durch einen zu kleinen Stichprobenumfang verfälscht werden. Der Maximalstichprobenumfang hilft, den für die Datasetauswertung anfallenden Zeit- und Arbeitsaufwand besser zu steuern. Bei Überschreitung der Angabe für den Umfang werden nur die neuesten Datensätze ausgewertet.

     ![Stichprobenumfang konfigurieren](images/accuracy-config-sample.png)

1.  Klicken Sie auf die Schaltfläche **Weiter**.

    Zur Überprüfung wird eine Zusammenfassung der von Ihnen getroffenen Auswahl angezeigt. Falls Sie Änderungen vornehmen möchten, klicken Sie für den betreffenden Abschnitt auf den Link **Bearbeiten**.

1.  Klicken Sie zum Abschließen Ihrer Konfiguration auf **Speichern**.

Ihnen wird nun die Möglichkeit geboten, Ihrem Modell direkt Rückmeldedaten zur Verfügung zu stellen, die auf Genauigkeit ausgewertet werden sollen.


  ![Rückmeldedaten senden](images/accuracy-send-feedback0.png)

Klicken Sie auf die Schaltfläche *Rückmeldedaten hinzufügen*, eine in Dateidatei in CSV-Format hochzuladen und legen Sie das Begrenzungszeichen fest, sodass es Ihren Daten entspricht.

Es wird erwartet, dass die CSV-Datei mit den Rückmeldedaten alle Merkmalswerte sowie den manuell zugewiesenen Ziel-/Bezeichnungswert enthält. Beispielsweise enthalten die Trainingsdaten des Medikamentenmodells die Merkmalwerte `"AGE"`, `"SEX"`, `"BP"`, `"CHOLESTEROL"`,`"NA"` und `"K"` sowie den Ziel-/Bezeichnungswert `"DRUG"`. Die CSV-Datei mit den Rückmeldedaten muss Werte für diese Felder enthalten und könnte zum Beispiel folgendermaßen aussehen: `[43, M, HIGH, NORMAL, 0.6345, 1.4587, DrugX]`. Wenn für die CSV-Datei mit den Rückmeldedaten ein Header vorgesehen ist, erfolgt die Zuordnung der Feldnamen unter Verwendung des Headers. Andernfalls **MUSS** die Reihenfolge der Felder identisch mit der im Trainingsschema sein.
{: important}

Beachten Sie, dass die von Ihrem Modell zurückgegebenen Vorhersagetypen und die Ziel-/Bezeichnungsspalte in Ihren Rückmeldedaten übereinstimmen müssen.
{: note}

  ![Begrenzungszeichen bei Genauigkeit](images/accuracy-delimit.png)

Die Größe für Dateien ist gegenwärtig auf 8 MB begrenzt
{: note}

Alternativ können Sie Rückmeldedaten mit den bereitgestellten `cURL`- oder `Python`-Code-Snippets veröffentlichen.

Die Felder und Werte in den Code-Snippets müssen durch die tatsächlichen Werte ersetzt werden, da es sich bei den angegebenen Werten lediglich um Beispiele handelt.
{: important}

Auf Wunsch können Sie diesen optionalen Schritt auch durch Auswahl von **Beenden** überspringen. Sie haben immer noch die Möglichkeit, zu einem späteren Zeitpunkt eine CSV-Datei zur Bewertung hochzuladen.

### Weitere Schritte
{: #acc-next}

Auf der Seite *Überwachungen konfigurieren* können Sie eine weitere Überwachungskategorie auswählen.
