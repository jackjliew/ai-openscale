---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, F1-Measure

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

# F1-Maß ![Beta-Tag](images/beta.png)
{: #quality_f1-measr}

Das F1-Maß liefert das harmonische Mittel für Genauigkeit und Trefferquote.
{: shortdesc}

## F1-Maß - auf einen Blick
{: #quality_f1-measr-glance}

- **Beschreibung**: Harmonisches Mittel zwischen Genauigkeit und Trefferquote.
- **Standardschwellenwerte**: Unterer Grenzwert = 80 %
- **Standardempfehlung**:
   - **Aufwärtstrend**: Ein Aufwärtstrend gibt eine Verbesserung der Metrik an. Dies bedeutet, dass das Retraining des Modells effektiv ist.
   - **Abwärtstrend**: Ein Abwärtstrend gibt eine Verschlechterung der Metrik an. Die Differenz zwischen den Rückmeldedaten und den Trainingsdaten vergrößert sich signifikant.
   - **Ungleichmäßige oder unregelmäßige Variation**: Eine ungleichmäßige oder unregelmäßige Variation weist darauf hin, dass die Rückmeldedaten zwischen den Bewertungen nicht konsistent sind. Erhöhen Sie den Mindeststichprobenumfang für die Qualitätsüberwachung.
- **Problemtyp**: Binäre Klassifizierung
- **Diagrammwerte**: Letzter Wert im Zeitrahmen
- **Verfügbare Metrikdetails**: Wahrheitsmatrix

## Anzeige interpretieren
{: #quality_f1-measr-display}

![Abbildung des Diagramms für das F1-Maß](images/quality-f1-meas.png)

## Berechnung
{: #quality_f1-measr-math}

Das F1-Maß ist das gewichtete harmonische Mittel bzw. der gewichtete harmonische Durchschnitt für Genauigkeit und Trefferquote.

```
          (Genauigkeit * Trefferquote)
F1 = 2 *  ____________________________

          (Genauigkeit + Trefferquote)
```

