---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, precision

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

# Genauigkeit
{: #quality_precision}

Die Genauigkeit gibt den Anteil der richtigen Vorhersagen an den Vorhersagen der positiven Klasse an.
{: shortdesc}

## Genauigkeit - auf einen Blick
{: #quality_precision-glance}

- **Beschreibung**: Anteil der richtigen Vorhersagen innerhalb der Vorhersagen in der positiven Klasse.
- **Standardschwellenwerte**: Unterer Grenzwert = 80 %
- **Standardempfehlung**:
   - **Aufwärtstrend**: Ein Aufwärtstrend gibt eine Verbesserung der Metrik an. Dies bedeutet, dass das Retraining des Modells effektiv ist.
   - **Abwärtstrend**: Ein Abwärtstrend gibt eine Verschlechterung der Metrik an. Die Differenz zwischen den Rückmeldedaten und den Trainingsdaten vergrößert sich signifikant.
   - **Ungleichmäßige oder unregelmäßige Variation**: Eine ungleichmäßige oder unregelmäßige Variation weist darauf hin, dass die Rückmeldedaten zwischen den Bewertungen nicht konsistent sind. Erhöhen Sie den Mindeststichprobenumfang für die Qualitätsüberwachung.
- **Problemtyp**: Binäre Klassifizierung
- **Diagrammwerte**: Letzter Wert im Zeitrahmen
- **Verfügbare Metrikdetails**: Wahrheitsmatrix

## Anzeige interpretieren
{: #quality_precision-display}

![Abbildung des Diagramms für Genauigkeit](images/quality-precision.png)

## Berechnung
{: #quality_precision-math}

Die Genauigkeit (P) ist definiert als die Anzahl der wahr-positiven Ergebnisse (Tp) im Verhältnis zur Anzahl der wahr-positiven Ergebnisse zuzüglich der Anzahl der falsch-positiven Ergebnisse (Fp).


```
             Anzahl der wahr-positiven Ergebnisse
Genauigkeit =  __________________________________________________________________________________

             (Anzahl der wahr-positiven Ergebnisse + Anzahl der falsch-positiven Ergebnisse)
```
