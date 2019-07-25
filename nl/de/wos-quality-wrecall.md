---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, weighted recal

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

# Gewichtete Trefferquote ![Beta-Tag](images/beta.png)
{: #quality_weighted_recall}

Die gewichtete Trefferquote gibt den gewichteten Mittelwert der Trefferquote mit Gewichtungen gleich der Klassenwahrscheinlichkeit an.
{: shortdesc}

## Gewichtete Trefferquote - auf einen Blick
{: #quality_weighted_recall-glance}

- **Beschreibung**: Gewichteter Mittelwert der Trefferquote mit Gewichtungen, die gleich der Klassenwahrscheinlichkeit sind.
- **Standardschwellenwerte**: Unterer Grenzwert = 80 %
- **Standardempfehlung**:
   - **Aufwärtstrend**: Ein Aufwärtstrend gibt eine Verbesserung der Metrik an. Dies bedeutet, dass das Retraining des Modells effektiv ist.
   - **Abwärtstrend**: Ein Abwärtstrend gibt eine Verschlechterung der Metrik an. Die Differenz zwischen den Rückmeldedaten und den Trainingsdaten vergrößert sich signifikant.
   - **Ungleichmäßige oder unregelmäßige Variation**: Eine ungleichmäßige oder unregelmäßige Variation weist darauf hin, dass die Rückmeldedaten zwischen den Bewertungen nicht konsistent sind. Erhöhen Sie den Mindeststichprobenumfang für die Qualitätsüberwachung.
- **Problemtyp**: Klassifizierung mit mehreren Klassen
- **Diagrammwerte**: Letzter Wert im Zeitrahmen
- **Verfügbare Metrikdetails**: Wahrheitsmatrix

## Anzeige interpretieren
{: #quality_weighted_recall-display}

![Abbildung des Diagramms für die gewichtete Trefferquote](images/quality-recall.png)

## Berechnung
{: #quality_weighted_recall-math}

Die gewichtete Trefferquote (wR) ist definiert als die Anzahl der wahr-positiven Ergebnisse (Tp) im Verhältnis zur Anzahl der wahr-positiven Ergebnisse zuzüglich der Anzahl der falsch-negativen Ergebnisse (Fn) mit gewichteten Daten. 

```
                                 Anzahl der wahr-positiven Ergebnisse
Trefferquote =  ______________________________________________________________________________
                (Anzahl der wahr-positiven Ergebnisse + Anzahl der falsch-negativen Ergebnisse)
```
