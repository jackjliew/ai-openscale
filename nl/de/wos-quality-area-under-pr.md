---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Area under PR

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

# Fläche unterhalb der PR-Kurve ![Beta-Tag](images/beta.png)
{: #quality-area-pr}

Die Fläche unterhalb der PR-Kurve (PR = Precision Recall, Trefferquote und Genauigkeit) gibt den Bereich unter der Kurve für Genauigkeit und Trefferquote an. Diese Metrik ist hilfreich, wenn ein besonders großes Ungleichgewicht im Hinblick auf die Klassen besteht.
{: shortdesc}

## Fläche unterhalb der PR-Kurve - auf einen Blick
{: #quality-area-pr-glance}

- **Beschreibung**: Die Fläche, die sich unterhalb der PR-Kurve (PR = Precision Recall) befindet.
- **Standardschwellenwerte**: Unterer Grenzwert = 80 %
- **Standardempfehlung**:
   - **Aufwärtstrend**: Ein Aufwärtstrend gibt eine Verbesserung der Metrik an. Dies bedeutet, dass das Retraining des Modells effektiv ist.
   - **Abwärtstrend**: Ein Abwärtstrend gibt eine Verschlechterung der Metrik an. Die Differenz zwischen den Rückmeldedaten und den Trainingsdaten vergrößert sich signifikant.
   - **Ungleichmäßige oder unregelmäßige Variation**: Eine ungleichmäßige oder unregelmäßige Variation weist darauf hin, dass die Rückmeldedaten zwischen den Bewertungen nicht konsistent sind. Erhöhen Sie den Mindeststichprobenumfang für die Qualitätsüberwachung.
- **Problemtyp**: Binäre Klassifizierung
- **Diagrammwerte**: Letzter Wert im Zeitrahmen
- **Verfügbare Metrikdetails**: Wahrheitsmatrix

## Anzeige interpretieren
{: #quality-area-pr-display}

![Abbildung zur Fläche unterhalb der PR-Kurve mit einem Abwärtstrend bei den Metriken](images/quality-area-under-pr.png)


## Berechnung
{: #quality-area-pr-math}

Der Bereich unter der PR-Kurve entspricht der Summe von `Genauigkeit und Trefferquote`. 

Die Genauigkeit (P) ist definiert als die Anzahl der wahr-positiven Ergebnisse (Tp) im Verhältnis zur Anzahl der wahr-positiven Ergebnisse zuzüglich der Anzahl der falsch-positiven Ergebnisse (Fp).

```
                                 Anzahl der wahr-positiven Ergebnisse
Genauigkeit =  ______________________________________________________________________________
               (Anzahl der wahr-positiven Ergebnisse + Anzahl der falsch-positiven Ergebnisse)
```

Die Trefferquote (R) ist definiert als die Anzahl der wahr-positiven Ergebnisse (Tp) im Verhältnis zur Anzahl der wahr-positiven Ergebnisse zuzüglich der Anzahl der falsch-negativen Ergebnisse (Fn).

```
                                 Anzahl der wahr-positiven Ergebnisse
Trefferquote =  ______________________________________________________________________________
                (Anzahl der wahr-positiven Ergebnisse + Anzahl der falsch-negativen Ergebnisse)
```
