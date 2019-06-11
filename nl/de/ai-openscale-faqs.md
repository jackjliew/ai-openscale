---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: FAQs, frequently asked questions, questions

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
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

# Häufig gestellte Fragen (FAQs)
{: #wos-faqs}

Hier finden Sie eine Auswahl der am häufigsten gestellten Fragen von Benutzern von {{site.data.keyword.aios_full}}.
{: shortdesc}

## Fragen
{: #wos-faqs-questions}

- [Wie konvertiere ich die Daten in einer Vorhersagespalte vom ganzzahligen Datentyp in den kategorialen Datentyp?](#wos-faqs-convert-data-types)
- [Warum benötigt {{site.data.keyword.aios_short}} Zugriff auf meine Trainingsdaten?](#trainingdata)

### Wie konvertiere ich die Daten in einer Vorhersagespalte vom ganzzahligen Datentyp in den kategorialen Datentyp?
{: #wos-faqs-convert-data-types}

Bei der Konfiguration der Fairnessüberwachung für ein Modell lässt die Spalte für die Vorhersage nur ganzzahlige numerische Werte zu, obwohl die Vorhersage mit der Bezeichnung 'Kategorial' versehen ist. Wie kann ich die Konfiguration für die kategoriale (und nicht ganzzahlige) Funktion erzielen? Ist eine manuelle Konvertierung erforderlich? 

Die Trainingsdaten könnten mit Klassenbezeichnungen wie 'Darlehen abgelehnt', 'Darlehen bewilligt' versehen sein. Der Vorhersagewert, den der WML-Scoring-Endpunkt zurückgegeben hat, beinhaltet hat Werte wie '0.0', '1.0' usw. Der Scoring-Endpunkt umfasst außerdem eine optionale Spalte, die die Textdarstellung der Vorhersage enthält. Wenn zum Beispiel prediction=1.0 gilt, könnte die Spalte 'predictionLabel' einen Wert 'Darlehen bewilligt' enthalten. Wenn eine solche Spalte verfügbar ist, können Sie bei der Konfiguration des günstigen und des ungünstigen Ergebnisses für das Modell die Zeichenfolgewerte 'Darlehen bewilligt' und 'Darlehen abgelehnt' angeben. Ist keine solche Spalte verfügbar, müssen Sie für die Klasse 'favourable' bzw. 'unfavourable' für ein günstiges bzw. ungünstiges Ergebnis jeweils die Werte 1.0, 0.0 vom Typ Integer/Double für die Klasse 'favourable'/'unfavourable' angeben.

WML hat ein Konzept von Ausgabeschema, bei dem das Schema der Ausgabe des WML-Scoring-Endpunkts und die Rolle für die verschiedenen Spalten definiert wird. Anhand der Rollen wird angegeben, welche Spalte den Vorhersagewert, welche Spalte die Vorhersagewahrscheinlichkeit, welche den Klassenbezeichnungswert enthält, usw. Das Schema kann auch über den WML-Python-Client festgelegt werden. Benutzer können mithilfe des Ausgabeschemas eine Spalte definieren, die die Zeichenfolgedarstellung der Vorhersage enthält. Dies geschieht, indem für die Spalte für 'modeling-role' der Wert 'decoded-target' festgelegt wird. Die Dokumentation für den WML-Python-Client ist unter der folgenden Adresse verfügbar: http://wml-api-pyclient-dev.mybluemix.net/#repository. Suchen Sie nach 'OUTPUT_DATA_SCHEMA', um das Ausgabeschema zu verstehen. Als API wird die API 'store_model' verwendet, die OUTPUT_DATA_SCHEMA als Parameter akzeptiert.

### Warum benötigt {{site.data.keyword.aios_short}} Zugriff auf meine Trainingsdaten?
{: #trainingdata}

Sie müssen {{site.data.keyword.aios_short}} entweder Zugriff auf die in Db2 oder {{site.data.keyword.cos_full_notm}} gespeicherten Trainingsdaten ermöglichen oder Sie müssen ein Notebook ausführen, dass auf die Trainingsdaten zugreifen kann. {{site.data.keyword.aios_short}} benötigt aus den folgenden Gründen Zugriff auf Ihre Trainingsdaten:

- Zur Generierung kontrastierender Erklärungen: Für die Erstellung von Erklärungen ist der Zugriff auf Statistikdaten, wie z. B. Medianwert, Standardabweichung und einzelne Werte der Trainingsdaten, erforderlich.
- Zum Anzeigen von Statistikdaten für Trainingsdaten: Zum Ausfüllen der Seite mit Verzerrungsdetails benötigt {{site.data.keyword.aios_short}} Trainingsdaten, auf deren Basis Statistikdaten erstellt werden.

<!---
- To compute drift: Training data is required to build the drift detection model.
- To identify and suggest features to monitor for fairness: {{site.data.keyword.aios_short}} needs access to training data to suggest reference and monitored ranges.
--->

Wenn ein Notebook verwendet wird, wird erwartet, dass Sie bei der Konfiguration einer Bereitstellung in {{site.data.keyword.aios_short}} die Statistikdaten und weitere Informationen hochladen. Dies bedeutet, dass {{site.data.keyword.aios_short}} nicht mehr auf die Trainingsdaten außerhalb des Notebooks zugreifen kann, das in Ihrer Umgebung ausgeführt wird. Der Service verfügt nur über Zugriff auf die bei der Konfiguration hochgeladenen Informationen.


