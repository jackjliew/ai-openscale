---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Weighted False Positive Rate, wFPR

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

# Gewichtete Falsch-positiv-Rate (wFPR)
{: #quality_wfpr_weighted}

Die gewichtete Falsch-positiv-Rate (weighted False Positive Rate, FPR) gibt das gewichtete Mittel der FPR-Klasse mit Gewichtungen gleich der Klassenwahrscheinlichkeit an.
{: shortdesc}

## Gewichtete Falsch-positiv-Rate (wFPR) - auf einen Blick
{: #quality_wfpr_weighted-glance}

- **Beschreibung**: Anteil der falschen Vorhersagen innerhalb der positiven Klasse.
- **Standardschwellenwerte**: Unterer Grenzwert = 80 %
- **Standardempfehlung**:
   - **Aufwärtstrend**: Ein Aufwärtstrend gibt eine Verschlechterung der Metrik an. Die Differenz zwischen den Rückmeldedaten und den Trainingsdaten vergrößert sich signifikant.
   - **Abwärtstrend**: Ein Abwärtstrend gibt eine Verbesserung der Metrik an. Dies bedeutet, dass das Retraining des Modells effektiv ist.
   - **Ungleichmäßige oder unregelmäßige Variation**: Eine ungleichmäßige oder unregelmäßige Variation weist darauf hin, dass die Rückmeldedaten zwischen den Bewertungen nicht konsistent sind. Erhöhen Sie den Mindeststichprobenumfang für die Qualitätsüberwachung.
- **Problemtyp**: Klassifizierung mit mehreren Klassen
- **Diagrammwerte**: Letzter Wert im Zeitrahmen
- **Verfügbare Metrikdetails**: Wahrheitsmatrix

## Anzeige interpretieren
{: #quality_wfpr_weighted-display}

![Abbildung des Diagramms für die gewichtete Falsch-positiv-Rate](images/quality-fpr.png)

## Berechnung
{: #quality_wfpr_weighted-math}

Die gewichtete Falsch-positiv-Rate ist die Anwendung der Falsch-positiv-Rate mit gewichteten Daten.

```
                   Anzahl falsch-positiver Ergebnisse
FPR =  __________________________________________________________________________

       (Anzahl falsch-positiver Ergebnisse + Anzahl richtig-negativer Ergebnisse)
```
