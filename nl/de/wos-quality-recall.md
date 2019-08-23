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

# Trefferquote
{: #quality_recall}

Die Trefferquote gibt den Anteil der richtigen Vorhersagen an den Vorhersagen der positiven Klasse an.
{: shortdesc}

## Trefferquote - auf einen Blick
{: #quality_recall-glance}

- **Beschreibung**: Anteil der richtigen Vorhersagen innerhalb der positiven Klasse.
- **Standardschwellenwerte**: Unterer Grenzwert = 80 %
- **Standardempfehlung**:
   - **Aufwärtstrend**: Ein Aufwärtstrend gibt eine Verbesserung der Metrik an. Dies bedeutet, dass das Retraining des Modells effektiv ist.
   - **Abwärtstrend**: Ein Abwärtstrend gibt eine Verschlechterung der Metrik an. Die Differenz zwischen den Rückmeldedaten und den Trainingsdaten vergrößert sich signifikant.
   - **Ungleichmäßige oder unregelmäßige Variation**: Eine ungleichmäßige oder unregelmäßige Variation weist darauf hin, dass die Rückmeldedaten zwischen den Bewertungen nicht konsistent sind. Erhöhen Sie den Mindeststichprobenumfang für die Qualitätsüberwachung.
- **Problemtyp**: Binäre Klassifizierung
- **Diagrammwerte**: Letzter Wert im Zeitrahmen
- **Verfügbare Metrikdetails**: Wahrheitsmatrix

## Anzeige der Trefferquoten-Metrik
{: #quality_recall-display}

![Abbildung des Diagramms für Trefferquote](images/quality-recall.png)

### Fairness-Score
{: #quality_recall-display-fairness-score}

Für die Trefferquoten-Metrik wird der folgende Fairness-Score angezeigt. 

![Darstellung des Trefferquoten-Score-Prozentsatzes.](images/wos-quality-recall-score.png)

### Zeitplan
{: #quality_recall-display-schedule}

Das Fenster **Zeitplan** zeigt die Uhrzeiten für **Letzte Bewertung** und **Nächste Bewertung** an. Qualitätsmetriken werden stündlich ausgewertet. Sie können die Bewertung erzwingen, indem Sie auf **Qualität jetzt überprüfen** klicken. Sie können auch eine Rückmeldung hinzufügen, indem Sie auf **Rückmeldedaten hinzufügen** klicken.

![Darstellung des Zeitplan-Fensters mit Uhrzeiten für letzte und nächste Bewertung](images/wos-quality-schedule.png)


### Empfehlung
{: #quality_recall-display-recommendations}

Zur Erleichterung der Diagramminterpretation wird im Teilfenster **Empfehlung** angezeigt, welche Trends auf eine Verbesserung oder Verschlechterung der Modelleffektivität hinweisen.

![Darstellung des Empfehlungsfensters.](images/wos-quality-positive-recommendation.png)




## Berechnung
{: #quality_recall-math}

Die Trefferquote (R) ist definiert als die Anzahl der wahr-positiven Ergebnisse (Tp) im Verhältnis zur Anzahl der wahr-positiven Ergebnisse zuzüglich der Anzahl der falsch-negativen Ergebnisse (Fn).

```
                       Anzahl der wahr-positiven Ergebnisse
Trefferquote =  ______________________________________________________________________________

           (Anzahl der wahr-positiven Ergebnisse + Anzahl der falsch-negativen Ergebnisse)
```
