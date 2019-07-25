---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Weighted F1-Measure

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

# Gewichtetes F1-Maß ![Beta-Tag](images/beta.png)
{: #quality_wght_f1-measure}

Das gewichtete F1-Maß gibt den gewichteten Mittelwert des F1-Maßes mit Gewichtungen gleich der Klassenwahrscheinlichkeit an.
{: shortdesc}

## Gewichtetes F1-Maß - auf einen Blick
{: #quality_wght_f1-measure-glance}

- **Beschreibung**: Gewichteter Mittelwert des F1-Maßes mit Gewichtungen, die gleich der Klassenwahrscheinlichkeit sind.
- **Standardschwellenwerte**: Unterer Grenzwert = 80 %
- **Standardempfehlung**:
   - **Aufwärtstrend**: Ein Aufwärtstrend gibt eine Verbesserung der Metrik an. Dies bedeutet, dass das Retraining des Modells effektiv ist.
   - **Abwärtstrend**: Ein Abwärtstrend gibt eine Verschlechterung der Metrik an. Die Differenz zwischen den Rückmeldedaten und den Trainingsdaten vergrößert sich signifikant.
   - **Ungleichmäßige oder unregelmäßige Variation**: Eine ungleichmäßige oder unregelmäßige Variation weist darauf hin, dass die Rückmeldedaten zwischen den Bewertungen nicht konsistent sind. Erhöhen Sie den Mindeststichprobenumfang für die Qualitätsüberwachung.
- **Problemtyp**: Klassifizierung mit mehreren Klassen
- **Diagrammwerte**: Letzter Wert im Zeitrahmen
- **Verfügbare Metrikdetails**: Wahrheitsmatrix

## Anzeige interpretieren
{: #quality_wght_f1-measure-display}

![Abbildung des Diagramms für das gewichtete F1-Maß](images/quality-f1-meas.png)

## Berechnung
{: #quality_wght_f1-measure-math}

Das gewichtete F1-Maß ist das Ergebnis der Verwendung gewichteter Daten.

```
          (Genauigkeit * Trefferquote)
F1 = 2 *  ____________________________

          (Genauigkeit + Trefferquote)
```
