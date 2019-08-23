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

# Wurzel für mittleren quadratischen Fehler
{: #supqualdets_squ_errors_mean}

Die Ansicht für die Wurzel des mittleren quadratischen Fehlers (Root-Mean-Squared Error, RMSE) zeigt den Unterschied zwischen den vorhergesagten und den beobachteten Werten in Ihrem Modell an.
{: shortdesc}

## Wurzel des mittleren quadratischen Fehlers - auf einen Blick
{: #anlz_metrics_supqualdets_squ_errors_mean}

- **Beschreibung**: Quadratwurzel des Mittelwerts der quadrierten Differenz zwischen der Modellvorhersage und dem Zielwert.
- **Standardschwellenwerte**: Oberer Grenzwert = 80 %
- **Standardempfehlung**:
   - **Aufwärtstrend**: Ein Aufwärtstrend gibt eine Verschlechterung der Metrik an. Die Differenz zwischen den Rückmeldedaten und den Trainingsdaten vergrößert sich signifikant.
   - **Abwärtstrend**: Ein Abwärtstrend gibt eine Verbesserung der Metrik an. Dies bedeutet, dass das Retraining des Modells effektiv ist.
   - **Ungleichmäßige oder unregelmäßige Variation**: Eine ungleichmäßige oder unregelmäßige Variation weist darauf hin, dass die Rückmeldedaten zwischen den Bewertungen nicht konsistent sind. Erhöhen Sie den Mindeststichprobenumfang für die Qualitätsüberwachung.
- **Problemtyp**: Regression
- **Diagrammwerte**: Letzter Wert im Zeitrahmen
- **Verfügbare Metrikdetails**: Keine

## Anzeige interpretieren
{: #supqualdets_squ_errors_mean-display}

![Abbildung des Diagramms für die Wurzel des mittleren quadratischen Fehlers](images/xxxx.png)

## Berechnung
{: #supqualdets_squ_errors_mean-math}

Die Wurzel des mittleren quadratischen Fehlers ist gleich der Quadratwurzel des gemittelten Fehlerquadrats (Vorhersagen minus beobachtete Werte).

```
          ___________________________________________________________________
RMSE  =  √(Vorhersagen - beobachtete Werte)*(Vorhersagen - beobachtete Werte)
```
