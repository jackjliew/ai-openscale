---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: dashboard, navigating, navigation, insights

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

# Insights mit {{site.data.keyword.aios_short}}
{: #io-ov}

Sie können alle Bereitstellungen, die Sie überwachen, über das {{site.data.keyword.aios_full}}-Dashboard verfolgen. Das Dashboard stellt die Hauptsicht für {{site.data.keyword.aios_short}} dar und ermöglicht es Ihnen, Einblicke in die Leistung Ihrer Modelle zu erhalten.
{: shortdesc}

## Insights
{: #io-ins}

Die Registerkarte **Insights** (![Dashboard für Insights](images/insight-dash-tab.png)) liefert eine allgemeine Ansicht Ihrer Bereitstellungsüberwachung.

  ![Dashboard für Insights](images/insight-dashboard.png)

- ***Überwachte Bereitstellungen***: In diesem Beispiel werden insgesamt 10 Bereitstellungen überwacht. Acht der zehn folgenden Bereitstellungen werden als einzelne Kacheln angezeigt.

- ***Qualitäts-Alerts*** - Insgesamt 3 Qualitäts- (zuvor als Genauigkeit bezeichnet) Alerts werden in den folgenden Kacheln dargestellt. In diesem Beispiel weisen die Bereitstellungen `Treiberleistung`, `Marktanalyse` und `Preisrisiko` Genauigkeitswerte in Höhe von `60 %`, `65 %` bzw. `79 %` auf.

- ***Fairnessalerts*** - Es werden insgesamt sechs Fairnessalerts angegeben, die in den folgenden Kacheln und mit einer kleinen Markierung `BIAS` dargestellt werden. In diesem Beispiel weisen die Bereitstellungen `Treiberleistung`, `Marktanalyse`, `Einhaltung gesetzlicher Bestimmungen`, `Betrugserkennung`, `Premium-Optimierung` und `Kostenschätzer für Schaden` Fairnesswerte von `59 %`, `68 %`, `62 %`, `64 %`, `79 %` und `63 %` auf.

Jede Kachel liefert eine Zusammenfassung der Überwachungsaktivitäten für diese Bereitstellung. Beachten Sie, dass die Kachel für die Bereitstellung `Call-Center-Routing` keine Probleme aufweist, was auf ein recht stabiles, genaues Modell hinweist.


## Einblicke in Fairness, Qualität, Leistung, Genauigkeit und Analyse
{: #it-ov}

Wählen Sie eine beliebige einzelne Bereitstellungskachel aus, damit weitere Details zu dieser Bereitstellung angezeigt werden. Überwachungsdaten für einzelne Bereitstellungen werden in einer Reihe von Diagrammen angezeigt. Die Diagramme verfolgen Metriken, wie z. B. Fairness, durchschnittliche Anforderungen pro Minute sowie Genauigkeit über Tage, Wochen oder Monate.

- [Daten für eine Bereitstellung anzeigen](/docs/services/ai-openscale?topic=ai-openscale-it-vdep)
- [Visualisierung von Daten für eine bestimmte Stunde anzeigen](/docs/services/ai-openscale?topic=ai-openscale-it-vdet)
- [Fairness](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics_fairness)
- [Qualität](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics)
- [Drift](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-ovr)
- [Leistung](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics_performance)
- [Analyse](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics_payload)
- [Optionen für die Verzerrungsbereinigung](/docs/services/ai-openscale?topic=ai-openscale-it-dbo)

## Erklärbarkeit
{: #io-tran}

Mit der Registerkarte **Transaktion erklären** (![Registerkarte 'Transaktion erklären'](images/insight-transact-tab.png)) können Sie nach einer bestimmten Transaktions-ID suchen, um eine Erklärung einer bestimmten Bereitstellungstransaktion zu erhalten.

- [Transaktionen erklären](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)
- [Kategoriale Modelle erklären](/docs/services/ai-openscale?topic=ai-openscale-ie-class)
- [Imagemodelle erklären](/docs/services/ai-openscale?topic=ai-openscale-ie-image)
- [Modelle mit unstrukturiertem Text erklären](/docs/services/ai-openscale?topic=ai-openscale-ie-unstruct)
- [Kontrastierende Erklärungen](/docs/services/ai-openscale?topic=ai-openscale-ie-pp-pn)

## Weitere Schritte
{: #io-next}

- [Weitere zu überwachende Bereitstellungen hinzufügen](/docs/services/ai-openscale?topic=ai-openscale-dpl-select).

