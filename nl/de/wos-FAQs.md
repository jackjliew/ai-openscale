---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: FAQs, frequently asked questions, questions

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

# Häufig gestellte Fragen (FAQs)
{: #wos-faqs}

Hier finden Sie eine Auswahl der am häufigsten gestellten Fragen von Benutzern von {{site.data.keyword.aios_full}}.
{: shortdesc}

## Fragen
{: #wos-faqs-questions}

- [Was ist {{site.data.keyword.aios_short}}?](#faq-whatsa)
- [Welche Preisstruktur gilt für {{site.data.keyword.aios_short}}?](#faq-pricing)
- [Gibt es eine kostenlose Testversion für {{site.data.keyword.aios_short}}?](#faq-freetrial)
- [Meine AI-Modelle sind in Azure gespeichert. Kann ich die Microsoft Azure ML-Engine mit {{site.data.keyword.aios_short}} verwenden?](#faq-azure)
- [Meine AI-Modelle sind in Amazon gespeichert. Kann ich die Amazon SageMaker ML-Engine mit {{site.data.keyword.aios_short}} verwenden?](#faq-sagemaker)
- [Ist {{site.data.keyword.aios_short}} auf {{site.data.keyword.icp4dfull_notm}} verfügbar?](#faq-icp)
- [Ich möchte {{site.data.keyword.aios_short}} auf meinen eigenen Servern ausführen. Wie viel Verarbeitungskapazität sollte ich zuordnen?](#faq-sizing)
- [Wie konvertiere ich die Daten in einer Vorhersagespalte vom ganzzahligen Datentyp in den kategorialen Datentyp?](#wos-faqs-convert-data-types)
- [Warum benötigt {{site.data.keyword.aios_short}} Zugriff auf meine Trainingsdaten?](#trainingdata)

### Was ist {{site.data.keyword.aios_short}}
{: #faq-whatsa}

Watson OpenScale verfolgt und misst Ergebnisse der künstlichen Intelligenz über den gesamten Lebenszyklus hinweg, passt die künstliche Intelligenz an wechselnde Geschäftssituationen an und reguliert diese Situationen - für Modelle, die auf der ganzen Welt erstellt und ausgeführt werden.

Mit dem folgenden Video können Sie sich einen schnellen Überblick über {{site.data.keyword.aios_short}} verschaffen.

<p>
  <div class="embed-responsive embed-responsive-16by9">
    <iframe class="embed-responsive-item" id="youtubeplayer" title="Vertrauen und Transparenz in AI" type="text/html" width="640" height="390" src="https://www.youtube.com/embed/6Ei8rPVtCf8" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>
  </div>
</p>

### Welche Preisstruktur gilt für {{site.data.keyword.aios_short}}?
{: #faq-pricing}

Wenn bei Ihnen der Wechsel vom Lite-Plan ansteht, gibt es einen **Standard**-Preisplan, der die Überwachung von bis zu 24 bereitgestellten Modellen umfasst - ohne Einschränkungen für die Anzahl der Nutzdaten, Rückmeldezeilen oder Transaktionen für Erklärbarkeit. Aktuelle Informationen hierzu finden Sie im [{{site.data.keyword.Bluemix}}-Katalog](https://cloud.ibm.com/catalog/services/watson-openscale?cm_sp=WatsonPlatform-WatsonPlatform-_-OnPageNavCTA-IBMWatson_OpenScale-_-AIOSProductPage){: external}.


### Gibt es eine kostenlose Testversion für {{site.data.keyword.aios_short}}?
{: #faq-freetrial}

{{site.data.keyword.aios_short}} ist über den Lite-Plan als kostenlose Testversion verfügbar. Rufen Sie zum Anmelden die [{{site.data.keyword.aios_short}}-Webseite](https://www.ibm.com/cloud/watson-openscale/){: external} auf und klicken Sie auf die Schaltfläche für den Programmeinstieg****. Sie können den Lite-Plan so lange nutzen, wie Sie möchten (abhängig von den monatlichen Nutzungsbeschränkungen, die jeden Monat aktualisiert werden).

### Meine AI-Modelle sind in Azure gespeichert. Kann ich die Microsoft Azure ML-Engine mit {{site.data.keyword.aios_short}} verwenden?
{: #faq-azure}

{{site.data.keyword.aios_short}} unterstützt sowohl Microsoft Azure ML Studio- als auch Microsoft Azure ML Service-Engines. Weitere Informationen finden Sie in den Abschnitten [Microsoft Azure ML Studio-Frameworks](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azure) und [Microsoft Azure ML Service-Frameworks](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azure-service).

### Meine AI-Modelle sind in Amazon gespeichert. Kann ich die Amazon SageMaker ML-Engine mit {{site.data.keyword.aios_short}} verwenden?
{: #faq-sagemaker}

{{site.data.keyword.aios_short}} unterstützt die Amazon SageMaker ML-Engine. Weitere Informationen hierzu enthält der Abschnitt [Amazon SageMaker-Frameworks](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-aws-sage).

### Ist {{site.data.keyword.aios_short}} auf {{site.data.keyword.icp4dfull_notm}} verfügbar?
{: #faq-icp}

{{site.data.keyword.aios_short}} gehört zu den Premium-Add-ons für {{site.data.keyword.icp4dfull_notm}}. 

### Ich möchte {{site.data.keyword.aios_short}} auf meinen eigenen Servern ausführen. Wie viel Verarbeitungskapazität sollte ich zuordnen?
{: #faq-sizing}

Es gibt bestimmte Richtlinien für die [Hardwarekonfiguration](/docs/services/ai-openscale?topic=ai-openscale-inst-install-icp#inst-hwt) für Konfigurationen mit drei Knoten und sechs Knoten. Das IBM Technical Sales-Team kann Ihnen auch bei der Dimensionierung Ihrer spezifischen Konfiguration behilflich sein. Da {{site.data.keyword.aios_short}} als Add-on für {{site.data.keyword.icp4dfull_notm}} ausgeführt wird, müssen Sie die Anforderungen für beide Softwareprodukte berücksichtigen.

### Wie konvertiere ich die Daten in einer Vorhersagespalte vom ganzzahligen Datentyp in den kategorialen Datentyp?
{: #wos-faqs-convert-data-types}

Bei der Konfiguration der Fairnessüberwachung für ein Modell lässt die Spalte für die Vorhersage nur ganzzahlige numerische Werte zu, obwohl die Vorhersage mit der Bezeichnung 'Kategorial' versehen ist. Wie kann ich die Konfiguration für die kategoriale (und nicht ganzzahlige) Funktion erzielen? Ist eine manuelle Konvertierung erforderlich? 

Die Trainingsdaten könnten mit Klassenbezeichnungen wie 'Darlehen abgelehnt', 'Darlehen bewilligt' versehen sein. Der Vorhersagewert, den der Der Vorhersagewert, den der {{site.data.keyword.pm_full}}-Scoring-Endpunkt zurückgegeben hat, beinhaltet hat Werte wie '0.0', '1.0' usw. Der Scoring-Endpunkt umfasst außerdem eine optionale Spalte, die die Textdarstellung der Vorhersage enthält. Wenn zum Beispiel prediction=1.0 gilt, könnte die Spalte 'predictionLabel' einen Wert 'Darlehen bewilligt' enthalten. Wenn eine solche Spalte verfügbar ist, können Sie bei der Konfiguration des günstigen und des ungünstigen Ergebnisses für das Modell die Zeichenfolgewerte 'Darlehen bewilligt' und 'Darlehen abgelehnt' angeben. Ist keine solche Spalte verfügbar, müssen Sie für die Klasse 'favourable' bzw. 'unfavourable' für ein günstiges bzw. ungünstiges Ergebnis jeweils die Werte 1.0, 0.0 vom Typ Integer/Double für die Klasse 'favourable'/'unfavourable' angeben.

{{site.data.keyword.pm_full}} hat ein Konzept von Ausgabeschema, bei dem das Schema der Ausgabe des {{site.data.keyword.pm_full}}-Scoring-Endpunkts und die Rolle für die verschiedenen Spalten definiert wird. Anhand der Rollen wird angegeben, welche Spalte den Vorhersagewert, welche Spalte die Vorhersagewahrscheinlichkeit, welche den Klassenbezeichnungswert enthält, usw. Das Schema kann auch über den {{site.data.keyword.pm_full}}-Python-Client festgelegt werden. Benutzer können mithilfe des Ausgabeschemas eine Spalte definieren, die die Zeichenfolgedarstellung der Vorhersage enthält. Dies geschieht, indem für die Spalte für 'modeling-role' der Wert 'decoded-target' festgelegt wird. Die Dokumentation für den {{site.data.keyword.pm_full}} Python-Client ist unter der folgenden Adresse verfügbar: http://wml-api-pyclient-dev.mybluemix.net/#repository. Suchen Sie nach 'OUTPUT_DATA_SCHEMA', um das Ausgabeschema zu verstehen. Als API wird die API 'store_model' verwendet, die OUTPUT_DATA_SCHEMA als Parameter akzeptiert.

### Warum benötigt {{site.data.keyword.aios_short}} Zugriff auf meine Trainingsdaten?
{: #trainingdata}

Sie müssen {{site.data.keyword.aios_short}} entweder Zugriff auf die in Db2 oder {{site.data.keyword.cos_full_notm}} gespeicherten Trainingsdaten ermöglichen oder Sie müssen ein Notebook ausführen, dass auf die Trainingsdaten zugreifen kann. {{site.data.keyword.aios_short}} benötigt aus den folgenden Gründen Zugriff auf Ihre Trainingsdaten:

- Zur Generierung kontrastierender Erklärungen: Für die Erstellung von Erklärungen ist der Zugriff auf Statistikdaten wie z. B. Medianwert, Standardabweichung und einzelne Werte der Trainingsdaten erforderlich.
- Zum Anzeigen von Statistikdaten für Trainingsdaten: Zum Ausfüllen der Seite mit Verzerrungsdetails benötigt {{site.data.keyword.aios_short}} Trainingsdaten, auf deren Basis Statistikdaten erstellt werden.

<!---
- To compute drift: Training data is required to build the drift detection model.
- To identify and suggest features to monitor for fairness: {{site.data.keyword.aios_short}} needs access to training data to suggest reference and monitored ranges.
--->

Wenn ein Notebook verwendet wird, wird erwartet, dass Sie bei der Konfiguration einer Bereitstellung in {{site.data.keyword.aios_short}} die Statistikdaten und weitere Informationen hochladen. Dies bedeutet, dass {{site.data.keyword.aios_short}} nicht mehr auf die Trainingsdaten außerhalb des Notebooks zugreifen kann, das in Ihrer Umgebung ausgeführt wird. Der Service verfügt nur über Zugriff auf die bei der Konfiguration hochgeladenen Informationen.


