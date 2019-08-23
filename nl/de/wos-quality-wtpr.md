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

# Gewichtete Wahr-positiv-Rate (wTPR)
{: #quality-wtpr}

Die gewichtete Wahr-positiv-Rate (True Positive Rate, TPR) gibt den gewichteten Mittelwert der Klassen-TPR mit Gewichtungen gleich der Klassenwahrscheinlichkeit an.
{: shortdesc)

## Gewichtete Wahr-positiv-Rate (wTPR) - auf einen Blick
{: #quality-wtpr-glance}

- **Beschreibung**: Gewichteter Mittelwert der Klasse TPR mit Gewichtungen, die gleich der Klassenwahrscheinlichkeit sind.
- **Standardschwellenwerte**: Unterer Grenzwert = 80 %
- **Standardempfehlung**:
   - **Aufwärtstrend**: Ein Aufwärtstrend gibt eine Verbesserung der Metrik an. Dies bedeutet, dass das Retraining des Modells effektiv ist.
   - **Abwärtstrend**: Ein Abwärtstrend gibt eine Verschlechterung der Metrik an. Die Differenz zwischen den Rückmeldedaten und den Trainingsdaten vergrößert sich signifikant.
   - **Ungleichmäßige oder unregelmäßige Variation**: Eine ungleichmäßige oder unregelmäßige Variation weist darauf hin, dass die Rückmeldedaten zwischen den Bewertungen nicht konsistent sind. Erhöhen Sie den Mindeststichprobenumfang für die Qualitätsüberwachung.
- **Problemtyp**: Klassifizierung mit mehreren Klassen
- **Diagrammwerte**: Letzter Wert im Zeitrahmen
- **Verfügbare Metrikdetails**: Wahrheitsmatrix

## Anzeige interpretieren
{: #quality-wtpr-display}

![Abbildung zur gewichteten Wahr-positiv-Rate](images/quality-tpr.png)

## Berechnung
{: #quality-wtpr-math}

Die Wahr-positiv-Rate wird anhand der folgenden Formel berechnet:

```
                  Anzahl der wahr-positiven Ergebnisse
Wahr-positiv-Rate (TPR) =  _______________________________________________________________________________

        (Anzahl der wahr-positiven Ergebnisse + Anzahl der falsch-negativen Ergebnisse)
```
