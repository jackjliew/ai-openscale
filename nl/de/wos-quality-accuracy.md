---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds

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

# Genauigkeit
{: #accuracy-opener}

Genauigkeit ist ein Maß für den Anteil der richtigen Vorhersagen in Ihrem Modell.
{: shortdesc}

## Genauigkeit - auf einen Blick
{: #anlz_metrics_supqualdets_acc}

- **Beschreibung**: Die Proportion der richtigen Vorhersagen.
- **Standardschwellenwerte**: Unterer Grenzwert = 80 %
- **Standardempfehlung**:
   - **Aufwärtstrend**: Ein Aufwärtstrend gibt eine Verbesserung der Metrik an. Dies bedeutet, dass das Retraining des Modells effektiv ist.
   - **Abwärtstrend**: Ein Abwärtstrend gibt eine Verschlechterung der Metrik an. Die Differenz zwischen den Rückmeldedaten und den Trainingsdaten vergrößert sich signifikant.
   - **Ungleichmäßige oder unregelmäßige Variation**: Eine ungleichmäßige oder unregelmäßige Variation weist darauf hin, dass die Rückmeldedaten zwischen den Bewertungen nicht konsistent sind. Erhöhen Sie den Mindeststichprobenumfang für die Qualitätsüberwachung.
- **Problemtypen**: Binäre Klassifizierung und Klassifizierung mit mehreren Klassen
- **Diagrammwerte**: Letzter Wert im Zeitrahmen
- **Verfügbare Metrikdetails**: Wahrheitsmatrix


## Informationen zu Genauigkeit
{: #acc-understand}

Genauigkeit kann je nach Typ des Algorithmus unterschiedliche Dinge bedeuten:

- *Mehrklassige Klassifizierung*: Die Genauigkeit misst die Zahl der korrekten Vorhersagen einer beliebigen Klasse bei Normalisierung der Anzahl der Datenpunkte. Weitere Details hierzu enthält die Dokumentation zu Apache Spark unter [Multi-class classification](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#multiclass-classification){: external}.

- *Binäre Klassifizierung*: Bei einem Algorithmus für die binäre Klassifizierung wird die Genauigkeit als die Fläche unter einer ROC-Kurve gemessen. Weitere Details hierzu enthält die Dokumentation zu Apache Spark unter [Binary classification](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#binary-classification){: external}.

- *Regression*: Regressionsalgorithmen werden mit dem Bestimmtheitskoeffizienten (R2) gemessen. Weitere Details hierzu enthält die Dokumentation zu Apache Spark unter [Regression model evaluation](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#regression-model-evaluation){: external}.

### Funktionsweise
{: #acc-works}

Sie müssen mithilfe eines [Python-Clients](http://ai-openscale-python-client.mybluemix.net/#feedbacklogging){: external} oder einer [REST-API](https://cloud.ibm.com/apidocs/ai-openscale#post-feedback-payload){: external} manuell gekennzeichnete Rückmeldedaten über die {{site.data.keyword.aios_short}}-Benutzerschnittstelle hinzufügen.

Überprüfen Sie die [unterstützten Frameworks](/docs/services/ai-openscale?topic=ai-openscale-in-ov#in-fram) auf Einschränkungen hinsichtlich der Genauigkeitsüberwachung.

### Verzerrungsbereinigte Genauigkeit
{: #acc-debias-view}

Wenn die entsprechenden Daten zur Unterstützung vorhanden sind, wird die Genauigkeit sowohl anhand des ursprünglichen Modells als auch anhand des verzerrungsbereinigten Modells berechnet.{{site.data.keyword.aios_full_notm}} berechnet die Genauigkeit für die verzerrungsbereinigte Ausgabe und speichert sie als zusätzliche Spalte in der Nutzdatenprotokolltabelle.

![Modellvisualisierung mit der berechneten Genauigkeit für das ursprüngliche und das verzerrungsbereinigte Modell](images/debiased-accuracy.png)
