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

# Wahr-positiv-Rate (TPR)
{: #quality_tpr}

Die Wahr-positiv-Rate (TPR) gibt den Anteil der richtigen Vorhersagen an den Vorhersagen der positiven Klasse an. 
{: shortdesc}

## Wahr-positiv-Rate (TPR) - auf einen Blick
{: #quality_tpr-glance}

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
{: #quality_tpr-display}

![Abbildung des Diagramms für die Wahr-positiv-Rate](images/quality-tpr.png)

## Berechnung
{: #quality_tpr-math}

Die Wahr-positiv-Rate wird anhand der folgenden Formel berechnet:

```
                  Anzahl der wahr-positiven Ergebnisse
Wahr-positiv-Rate (TPR) =  _______________________________________________________________________________

        (Anzahl der wahr-positiven Ergebnisse + Anzahl der falsch-negativen Ergebnisse)
```
