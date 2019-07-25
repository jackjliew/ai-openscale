---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Mean squared error

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

# Mittlerer quadratischer Fehler ![Beta-Tag](images/beta.png)
{: #quality_squerror}

Der mittlere quadratische Fehler gibt den Mittelwert der quadrierten Differenz zwischen Modellvorhersage und -zielwert an. Er kann als Maß für die Qualität eines Schätzverfahrens verwendet werden.
{: shortdesc}

## Mittlerer quadratischer Fehler - auf einen Blick
{: #quality_squerror-glance}

- **Beschreibung**: Der Mittelwert der quadrierten Differenz zwischen der Modellvorhersage und dem Zielwert.
- **Standardschwellenwerte**: Oberer Grenzwert = 80 %
- **Standardempfehlung**:
   - **Aufwärtstrend**: Ein Aufwärtstrend gibt eine Verschlechterung der Metrik an. Die Differenz zwischen den Rückmeldedaten und den Trainingsdaten vergrößert sich signifikant.
   - **Abwärtstrend**: Ein Abwärtstrend gibt eine Verbesserung der Metrik an. Dies bedeutet, dass das Retraining des Modells effektiv ist.
   - **Ungleichmäßige oder unregelmäßige Variation**: Eine ungleichmäßige oder unregelmäßige Variation weist darauf hin, dass die Rückmeldedaten zwischen den Bewertungen nicht konsistent sind. Erhöhen Sie den Mindeststichprobenumfang für die Qualitätsüberwachung.
- **Problemtyp**: Regression
- **Diagrammwerte**: Letzter Wert im Zeitrahmen
- **Verfügbare Metrikdetails**: Keine

## Anzeige interpretieren
{: #quality_squerror-display}

![Abbildung des Diagramms für den mittleren quadratischen Fehler](images/xxxx.png)

## Berechnung
{: #quality_squerror-math}

Der mittlere quadratische Fehler in seiner einfachsten Form wird durch die folgende Formel dargestellt.

```
                                 SUMME  (Yi - ^Yi) * (Yi - ^Yi)
Mittlere quadratische Fehler  =  ____________________________

                                      Anzahl der Fehler
```
