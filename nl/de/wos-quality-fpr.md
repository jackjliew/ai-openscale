---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, False positive rate, fpr

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

# Falsch-positiv-Rate (FPR) ![Beta-Tag](images/beta.png)
{: #quality_fpr_false}

Die Rate falsch-positiver Ergebnisse gibt den Anteil der falschen Vorhersagen in der positiven Klasse an.
{: shortdesc}

## Falsch-positiv-Rate (FPR)
{: #quality_fpr_false-glance}

- **Beschreibung**: Anteil der falschen Vorhersagen innerhalb der positiven Klasse.
- **Standardschwellenwerte**: Unterer Grenzwert = 80 %
- **Standardempfehlung**:
   - **Aufwärtstrend**: Ein Aufwärtstrend gibt eine Verschlechterung der Metrik an. Die Differenz zwischen den Rückmeldedaten und den Trainingsdaten vergrößert sich signifikant.
   - **Abwärtstrend**: Ein Abwärtstrend gibt eine Verbesserung der Metrik an. Dies bedeutet, dass das Retraining des Modells effektiv ist.
   - **Ungleichmäßige oder unregelmäßige Variation**: Eine ungleichmäßige oder unregelmäßige Variation weist darauf hin, dass die Rückmeldedaten zwischen den Bewertungen nicht konsistent sind. Erhöhen Sie den Mindeststichprobenumfang für die Qualitätsüberwachung.
- **Problemtyp**: Binäre Klassifizierung
- **Diagrammwerte**: Letzter Wert im Zeitrahmen
- **Verfügbare Metrikdetails**: Wahrheitsmatrix

## Anzeige interpretieren
{: #quality_fpr_false-display}

![Abbildung des Diagramms zur falsch-positiv-Rate](images/quality-fpr.png)

## Berechnung
{: #quality_fpr_false-math}

Die Falsch-positiv-Rate wird als Gesamtzahl der falsch-positiven Ergebnisse dividiert durch die Anzahl falsch-positiven Ergebnisse und die Anzahl der richtig-negativen Ergebnisse berechnet.

```
                                         Anzahl falsch-positiver Ergebnisse
Falsch-positiv-Rate =  __________________________________________________________________________

                       (Anzahl falsch-positiver Ergebnisse + Anzahl richtig-negativer Ergebnisse)
```
