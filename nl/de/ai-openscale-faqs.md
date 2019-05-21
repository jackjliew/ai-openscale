---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

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

# Häufig gestellte Fragen (FAQs)
{: #wos-faqs}

Hier finden Sie eine Auswahl der am häufigsten gestellten Fragen von Benutzern von {{site.data.keyword.aios_full}}.
{: shortdesc}

## Fragen
{: #wos-faqs-questions}

- [Wie konvertiere ich die Daten in einer Vorhersagespalte vom ganzzahligen Datentyp in den kategorialen Datentyp?](#wos-faqs-convert-data-types)

### Wie konvertiere ich die Daten in einer Vorhersagespalte vom ganzzahligen Datentyp in den kategorialen Datentyp?
{: #wos-faqs-convert-data-types}

Bei der Konfiguration der Fairnessüberwachung für ein Modell lässt die Spalte für die Vorhersage nur ganzzahlige numerische Werte zu, obwohl die Vorhersage mit der Bezeichnung 'Kategorial' versehen ist. Wie kann ich die Konfiguration für die kategoriale (und nicht ganzzahlige) Funktion erzielen? Ist eine manuelle Konvertierung erforderlich? 

Die Trainingsdaten könnten mit Klassenbezeichnungen wie 'Darlehen abgelehnt', 'Darlehen bewilligt' versehen sein. Der Vorhersagewert, den der WML-Scoring-Endpunkt zurückgegeben hat, beinhaltet hat Werte wie '0.0', '1.0' usw. Der Scoring-Endpunkt umfasst außerdem eine optionale Spalte, die die Textdarstellung der Vorhersage enthält. Wenn zum Beispiel prediction=1.0 gilt, könnte die Spalte 'predictionLabel' einen Wert 'Darlehen bewilligt' enthalten. Wenn eine solche Spalte verfügbar ist, können Sie bei der Konfiguration des günstigen und des ungünstigen Ergebnisses für das Modell die Zeichenfolgewerte 'Darlehen bewilligt' und 'Darlehen abgelehnt' angeben.
Ist keine solche Spalte verfügbar, müssen Sie für die Klasse 'favourable' bzw. 'unfavourable' für ein günstiges bzw. ungünstiges Ergebnis jeweils die Werte 1.0, 0.0 vom Typ Integer/Double für die Klasse 'favourable'/'unfavourable' angeben.

WML hat ein Konzept von Ausgabeschema, bei dem das Schema der Ausgabe des WML-Scoring-Endpunkts und die Rolle für die verschiedenen Spalten definiert wird. Anhand der Rollen wird angegeben, welche Spalte den Vorhersagewert, welche Spalte die Vorhersagewahrscheinlichkeit, welche den Klassenbezeichnungswert enthält, usw. Das Schema kann auch über den WML-Python-Client festgelegt werden. Benutzer können mithilfe des Ausgabeschemas eine Spalte definieren, die die Zeichenfolgedarstellung der Vorhersage enthält. Dies geschieht, indem für die Spalte für 'modeling-role' der Wert 'decoded-target' festgelegt wird. Die Dokumentation für den WML-Python-Client ist unter der folgenden Adresse verfügbar: http://wml-api-pyclient-dev.mybluemix.net/#repository. Suchen Sie nach 'OUTPUT_DATA_SCHEMA', um das Ausgabeschema zu verstehen. Als API wird die API 'store_model' verwendet, die OUTPUT_DATA_SCHEMA als Parameter akzeptiert.



