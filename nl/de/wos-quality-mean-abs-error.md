---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Mean absolute error

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

# Mittlerer absoluter Fehler
{: #quality_abserror}

Der mittlere absolute Fehler gibt den Mittelwert der absoluten Differenz zwischen Modellvorhersage und -zielwert an.
{: shortdesc}

## Mittlerer absoluter Fehler - auf einen Blick
{: #quality_abserror-glance}

- **Beschreibung**: Der Mittelwert der absoluten Differenz zwischen der Modellvorhersage und dem Zielwert.
- **Standardschwellenwerte**: Oberer Grenzwert = 80 %
- **Standardempfehlung**:
   - **Aufwärtstrend**: Ein Aufwärtstrend gibt eine Verschlechterung der Metrik an. Die Differenz zwischen den Rückmeldedaten und den Trainingsdaten vergrößert sich signifikant.
   - **Abwärtstrend**: Ein Abwärtstrend gibt eine Verbesserung der Metrik an. Dies bedeutet, dass das Retraining des Modells effektiv ist.
   - **Ungleichmäßige oder unregelmäßige Variation**: Eine ungleichmäßige oder unregelmäßige Variation weist darauf hin, dass die Rückmeldedaten zwischen den Bewertungen nicht konsistent sind. Erhöhen Sie den Mindeststichprobenumfang für die Qualitätsüberwachung.
- **Problemtyp**: Regression
- **Diagrammwerte**: Letzter Wert im Zeitrahmen
- **Verfügbare Metrikdetails**: Keine

## Anzeige interpretieren
{: #quality_abserror-display}

![Abbildung des Diagramms für den mittleren absoluten Fehler](images/xxxx.png)

## Berechnung
{: #quality_abserror-math}

Der mittlere absolute Fehler wird berechnet, indem alle absoluten Fehler addiert und durch die Anzahl der Fehler dividiert werden.

```
                         SUM  | Yi - Xi |
Mittlere absolute Fehler =  _____________________

                          Anzahl der Fehler
```
