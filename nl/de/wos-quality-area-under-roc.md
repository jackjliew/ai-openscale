---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Area under ROC

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

# Fläche unterhalb der ROC-Kurve
{: #quality_roc}

Bei der Fläche unterhalb der ROC-Kurve (ROC = Receiver Operating Characteristic) handelt es sich um die Fläche unter der Kurve für Trefferquote und Falsch-positiv-Rate. Die Kurve berechnet die Anfälligkeit in Bezug auf die Falsch-positiv-Rate.
{: shortdesc}

## Fläche unterhalb der ROC-Kurve - auf einen Blick
{: #quality_roc-glance}

- **Beschreibung**: Die Fläche, die sich unterhalb der Kurve für Trefferquote und Falsch-positiv-Rate befindet.
- **Standardschwellenwerte**: Unterer Grenzwert = 80 %
- **Standardempfehlung**:
   - **Aufwärtstrend**: Ein Aufwärtstrend gibt eine Verbesserung der Metrik an. Dies bedeutet, dass das Retraining des Modells effektiv ist.
   - **Abwärtstrend**: Ein Abwärtstrend gibt eine Verschlechterung der Metrik an. Die Differenz zwischen den Rückmeldedaten und den Trainingsdaten vergrößert sich signifikant.
   - **Ungleichmäßige oder unregelmäßige Variation**: Eine ungleichmäßige oder unregelmäßige Variation weist darauf hin, dass die Rückmeldedaten zwischen den Bewertungen nicht konsistent sind. Erhöhen Sie den Mindeststichprobenumfang für die Qualitätsüberwachung.
- **Problemtyp**: Binäre Klassifizierung
- **Diagrammwerte**: Letzter Wert im Zeitrahmen
- **Verfügbare Metrikdetails**: Wahrheitsmatrix

## Anzeige interpretieren
{: #quality_roc-display}

![Abbildung des Diagramms für Fläche unterhalb der ROC-Kurve](images/quality-area-under-roc.png)

## Berechnung
{: #quality_roc-math}

Die Fläche unterhalb der ROC-Kurve wird parametrisiert als `Wahr-positiv-Rate` gegenüber der `Falsch-positiv-Rate` in Bezug auf einen Schwellenwert `T` dargestellt.



