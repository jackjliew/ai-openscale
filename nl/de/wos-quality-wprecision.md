---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Weighted precision

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

# Gewichtete Genauigkeit
{: #quality_wgth_prec}

Die gewichtete Genauigkeit gibt den gewichteten Mittelwert der Genauigkeit mit Gewichtungen gleich der Klassenwahrscheinlichkeit an.
{: shortdesc}

## Gewichtete Genauigkeit - auf einen Blick
{: #quality_wgth_prec-glance}

- **Beschreibung**: Gewichteter Mittelwert der Genauigkeit mit Gewichtungen, die gleich der Klassenwahrscheinlichkeit sind.
- **Standardschwellenwerte**: Unterer Grenzwert = 80 %
- **Standardempfehlung**:
   - **Aufwärtstrend**: Ein Aufwärtstrend gibt eine Verbesserung der Metrik an. Dies bedeutet, dass das Retraining des Modells effektiv ist.
   - **Abwärtstrend**: Ein Abwärtstrend gibt eine Verschlechterung der Metrik an. Die Differenz zwischen den Rückmeldedaten und den Trainingsdaten vergrößert sich signifikant.
   - **Ungleichmäßige oder unregelmäßige Variation**: Eine ungleichmäßige oder unregelmäßige Variation weist darauf hin, dass die Rückmeldedaten zwischen den Bewertungen nicht konsistent sind. Erhöhen Sie den Mindeststichprobenumfang für die Qualitätsüberwachung.
- **Problemtyp**: Klassifizierung mit mehreren Klassen
- **Diagrammwerte**: Letzter Wert im Zeitrahmen
- **Verfügbare Metrikdetails**: Wahrheitsmatrix

## Anzeige interpretieren
{: #quality_wgth_prec-display}

![Abbildung des Diagramms für gewichtete Genauigkeit](images/quality-precision.png)

## Berechnung
{: #quality_wgth_prec-math}

Die Genauigkeit (P) ist definiert als die Anzahl der wahr-positiven Ergebnisse (Tp) im Verhältnis zur Anzahl der wahr-positiven Ergebnisse zuzüglich der Anzahl der falsch-positiven Ergebnisse (Fp).


```
                        Anzahl der wahr-positiven Ergebnisse
Genauigkeit =  __________________________________________________________________________________

             (Anzahl der wahr-positiven Ergebnisse + Anzahl der falsch-positiven Ergebnisse)
```
