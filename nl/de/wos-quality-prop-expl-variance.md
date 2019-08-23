---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Proportion explained variance

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

# Proportion der erklärten Varianz
{: #quality_var}

Die Proportion der erklärten Varianz stellt das Verhältnis der erklärten Varianz zur Zielvarianz dar. Die erklärte Varianz gibt die Differenz zwischen der Zielvarianz und der Varianz eines Vorhersagefehlers an.
{: shortdesc}

## Proportion der erklärten Varianz - auf einen Blick
{: #quality_var-glance}

- **Beschreibung**: Die Proportion der erklärten Varianz stellt das Verhältnis der erklärten Varianz zur Zielvarianz dar. Die erklärte Varianz gibt die Differenz zwischen der Zielvarianz und der Varianz eines Vorhersagefehlers an.
- **Standardschwellenwerte**: Unterer Grenzwert = 80 %
- **Standardempfehlung**:
   - **Aufwärtstrend**: Ein Aufwärtstrend gibt eine Verbesserung der Metrik an. Dies bedeutet, dass das Retraining des Modells effektiv ist.
   - **Abwärtstrend**: Ein Abwärtstrend gibt eine Verschlechterung der Metrik an. Die Differenz zwischen den Rückmeldedaten und den Trainingsdaten vergrößert sich signifikant.
   - **Ungleichmäßige oder unregelmäßige Variation**: Eine ungleichmäßige oder unregelmäßige Variation weist darauf hin, dass die Rückmeldedaten zwischen den Bewertungen nicht konsistent sind. Erhöhen Sie den Mindeststichprobenumfang für die Qualitätsüberwachung.
- **Problemtyp**: Regression
- **Diagrammwerte**: Letzter Wert im Zeitrahmen
- **Verfügbare Metrikdetails**: Keine

## Anzeige interpretieren
{: #quality_var-display}

![Abbildung des Diagramms für die Proportion der erklärten Varianz](images/xxxx.png)

## Berechnung
{: #quality_var-math}

Die Proportion der erklärten Varianz wird berechnet, indem die Zahlen gemittelt werden, dann für jede Zahl der Mittelwert abgezogen wird und die Ergebnisse quadriert werden. Berechnen Sie dann die Quadrate.

```
                                  Summe der Quadrate für Gruppen
Proportion erklärter Varianz =  __________________________________

                                      Quadratsumme insgesamt
```
