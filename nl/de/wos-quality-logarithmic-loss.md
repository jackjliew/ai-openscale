---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: fairness, fairness monitor, payload, perturbation, training data, debiased, Logarithmic loss

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

# Logarithmischer Verlust
{: #quality_log_loss}

Der logarithmische Verlust gibt den Mittelwert der Zielklassenwahrscheinlichkeit (Konfidenz) der Logarithmen an. Der Verlust wird auch als 'erwartete Log-Likelihood' bezeichnet und stellt eine nützliche Kennzahl für die Modellleistung dar.
{: shortdesc}

## Logarithmischer Verlust - auf einen Blick
{: #quality_log_loss-glance}

- **Beschreibung**: Mittelwert der Zielklassenwahrscheinlichkeit (Konfidenz) der Logarithmen. Wird auch als erwartete Log-Likelihood bezeichnet.
- **Standardschwellenwerte**: Unterer Grenzwert = 80 %
- **Standardempfehlung**:
   - **Aufwärtstrend**: Ein Aufwärtstrend gibt eine Verschlechterung der Metrik an. Die Differenz zwischen den Rückmeldedaten und den Trainingsdaten vergrößert sich signifikant.
   - **Abwärtstrend**: Ein Abwärtstrend gibt eine Verbesserung der Metrik an. Dies bedeutet, dass das Retraining des Modells effektiv ist.
   - **Ungleichmäßige oder unregelmäßige Variation**: Eine ungleichmäßige oder unregelmäßige Variation weist darauf hin, dass die Rückmeldedaten zwischen den Bewertungen nicht konsistent sind. Erhöhen Sie den Mindeststichprobenumfang für die Qualitätsüberwachung.
- **Problemtypen**: Binäre Klassifizierung und Klassifizierung mit mehreren Klassen
- **Diagrammwerte**: Letzter Wert im Zeitrahmen
- **Verfügbare Metrikdetails**: Keine

## Anzeige interpretieren
{: #quality_log_loss-display}

![Darstellung zum logarithmischen Verlust](images/quality-log-loss.png)

### Fairness-Score
{: #quality_log_loss-display-fairness-score}

Für die Metrik für logarithmischen Verlust wird der folgende Fairness-Score angezeigt. 

![Darstellung des Trefferquoten-Score-Prozentsatzes.](images/wos-quality-logloss-score.png)

### Zeitplan
{: #quality_log_loss-display-schedule}

Das Fenster **Zeitplan** zeigt die Uhrzeiten für **Letzte Bewertung** und **Nächste Bewertung** an. Qualitätsmetriken werden stündlich ausgewertet. Sie können die Bewertung erzwingen, indem Sie auf **Qualität jetzt überprüfen** klicken. Sie können auch eine Rückmeldung hinzufügen, indem Sie auf **Rückmeldedaten hinzufügen** klicken.

![Darstellung des Zeitplan-Fensters mit Uhrzeiten für letzte und nächste Bewertung](images/wos-quality-schedule.png)


### Empfehlung
{: #quality_log_loss-display-recommendations}

Zur Erleichterung der Diagramminterpretation wird im Teilfenster **Empfehlung** angezeigt, welche Trends auf eine Verbesserung oder Verschlechterung der Modelleffektivität hinweisen.

![Darstellung des Empfehlungsfensters.](images/wos-quality-negative-recommendation.png)



## Berechnung
{: #quality_log_loss-math}

Bei einem binären Modell wird der logarithmische Verlust anhand der folgenden Formel berechnet:

```
-(y log(p) + (1-y)log(1-p))
```

Dabei ist p die wahre Kennzeichnung und y die vorhergesagte Wahrscheinlichkeit.

Bei einem Modell mit mehreren Klassen wird der logarithmische Verlust anhand der folgenden Formel berechnet:

```
  M
-SUM Yo,c log(Po,c)
 c=1 
```

Dabei ist M > 2, p die wahre Kennzeichnung und y die vorhergesagte Wahrscheinlichkeit.
