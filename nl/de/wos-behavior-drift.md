---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: drift, behavior, metrics

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

# Drifterkennung ![Beta-Tag](images/beta.png)
{: #behavior-drift-ovr}

Im Laufe der Zeit ändern sich die Bedeutung und die Auswirkungen bestimmter Merkmale bei einem Modellwechsel. Dies wirkt sich auf die zugeordneten Anwendungen und die daraus resultierenden Geschäftsergebnisse aus. Die Drifterkennung bietet {{site.data.keyword.aios_short}} eine Möglichkeit, Modellmetriken, Modellleistung und die Art und Weise zu verfolgen, in der sich die Gewichtung von Merkmalen im Laufe der Zeit ändert.
{: shortdesc}

## Erläuterungen zur Drifterkennung
{: #behavior-drift-understand}

Bei einer Drift handelt es sich um die Verschlechterung der Vorhersageleistung im Laufe der Zeit durch verdeckten Kontext. Die Genauigkeit Ihres Modells bei Vorhersagen nimmt möglicherweise nach und nach ab, wenn Ihre Daten sich im Laufe der Zeit ändern. {{site.data.keyword.aios_short}} erkennt die Drift und hebt sie hervor, sodass Sie Korrekturmaßnahmen ergreifen können.

### Funktionsweise
{: #behavior-drift-works}

{{site.data.keyword.aios_short}} analysiert alle Transaktionen im Hinblick auf Transaktionen, die zu einer Drift beitragen. Anschließend werden die Datensätze anhand der Attributwerte, die signifikant zu einer Drift beitragen, zu Gruppen zusammengefasst.

### Berechnung
{: #behavior-drift-math}

Im Abstand von drei Stunden berechnet {{site.data.keyword.aios_short}} die Drift, indem dieselben Trainingsdaten analysiert werden, die bereits von Ihrem Vorhersagemodell analysiert wurden. Anschließend werden die Ergebnisse mit den Vorhersagen des Modells verglichen. Wenn Änderungen oder Diskrepanzen vorliegen, berechnet {{site.data.keyword.aios_short}} das Ausmaß der Drift und benachrichtigt Sie ausgerichtet an dem von Ihnen festgelegten Schwellenwert über das Vorliegen der Drift. 


### Visualisierung der Drift
{: #behavior-drift-display}

Die Driftvisualisierung beinhaltet sowohl grafische als auch numerische statistische Daten:

![Diagramm mit Fairnessmetriken, das die Drift unterhalb des definierten Schwellenwerts anzeigt](images/drift-example.png)

Durch einen Klick auf das Diagramm können Sie bestimmte Transaktionen anzeigen, die zu der Drift beitragen. Es werden die wichtigsten Gründe für die Drift einschließlich einer Erläuterung der Beobachtung angezeigt und durch eine Liste nicht erwarteter Werte ergänzt.

![Diagramm mit Fairnessmetriken, das die Drift unterhalb des definierten Schwellenwerts anzeigt](images/drift-detection-example.png)

Drifttransaktionen sind in der Anzeige mit den Transaktionsdetails verfügbar. In dieser Anzeige können Sie auf **Erklären** klicken, um Informationen anzuzeigen, die erläutern, aus welchem Grund eine bestimmte Transaktion zur Driftkategorie gehört:

![Diagramm mit Fairnessmetriken, das die Drift unterhalb des definierten Schwellenwerts anzeigt](images/drift-detection-transactions.png)


## Weitere Schritte

- Informationen zum Interpretieren der Drift finden Sie im Abschnitt [Überwachung der Drifterkennung konfigurieren](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-config).
- Machen Sie sich anhand der [Erläuterungen zum Modelldrift mit IBM Watson OpenScale](https://medium.com/@manish.bhide/4c5401aa8da4) mit dem Potenzial vertraut, das die Drifterkennung bietet.
