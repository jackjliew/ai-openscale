---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, R squared

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

# R im Quadrat
{: #quality_r_squared}

R im Quadrat gibt das Verhältnis der Differenz zwischen Zielvarianz und Varianz für einen Vorhersagefehler in Bezug zur Zielvarianz an. Dieser Wert gibt Aufschluss über die Eignung der Daten, die Sie zum Erstellen des Modells verwendet haben, für die Regression.
{: shortdesc}

## R im Quadrat - auf einen Blick
{: #quality_r_squared-glance}

- **Beschreibung**: Das Verhältnis der Differenz zwischen der Zielvarianz und der Varianz für einen Vorhersagefehler in Bezug zur Zielvarianz.
- **Standardschwellenwerte**: Unterer Grenzwert = 80 %
- **Standardempfehlung**:
   - **Aufwärtstrend**: Ein Aufwärtstrend gibt eine Verbesserung der Metrik an. Dies bedeutet, dass das Retraining des Modells effektiv ist.
   - **Abwärtstrend**: Ein Abwärtstrend gibt eine Verschlechterung der Metrik an. Die Differenz zwischen den Rückmeldedaten und den Trainingsdaten vergrößert sich signifikant.
   - **Ungleichmäßige oder unregelmäßige Variation**: Eine ungleichmäßige oder unregelmäßige Variation weist darauf hin, dass die Rückmeldedaten zwischen den Bewertungen nicht konsistent sind. Erhöhen Sie den Mindeststichprobenumfang für die Qualitätsüberwachung.
- **Problemtyp**: Regression
- **Diagrammwerte**: Letzter Wert im Zeitrahmen
- **Verfügbare Metrikdetails**: Keine

## Anzeige interpretieren
{: #quality_r_squared-display}

![Darstellung des Diagramms für R im Quadrat](images/xxxx.png)

## Berechnung
{: #quality_r_squared-math}

Die Metrik 'R im Quadrat' ist durch die folgende Formel definiert.

```
                  erklärte Variation
R im Quadrat =ai-open-scale-ibm-aios-scheduling  | 1 | Zeitplanungsservice-  _____________________

                    gesamte Variation
```
