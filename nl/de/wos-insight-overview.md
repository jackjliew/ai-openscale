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

- ***Genauigkeitsalerts*** - In den unten aufgeführten Kacheln werden insgesamt drei Genauigkeitsalerts dargestellt. In diesem Beispiel weisen die Bereitstellungen `Treiberleistung`, `Marktanalyse` und `Preisrisiko` Genauigkeitswerte in Höhe von `60 %`, `65 %` bzw. `79 %` auf.

- ***Fairnessalerts*** - Es werden insgesamt sechs Fairnessalerts angegeben, die in den folgenden Kacheln und mit einer kleinen Markierung `BIAS` dargestellt werden. In diesem Beispiel weisen die Bereitstellungen `Treiberleistung`, `Marktanalyse`, `Einhaltung gesetzlicher Bestimmungen`, `Betrugserkennung`, `Premium-Optimierung` und `Kostenschätzer für Schaden` Fairnesswerte von `59 %`, `68 %`, `62 %`, `64 %`, `79 %` und `63 %` auf.

Jede Kachel liefert eine Zusammenfassung der Überwachungsaktivitäten für diese Bereitstellung. Beachten Sie, dass die Kachel für die Bereitstellung `Call-Center-Routing` keine Probleme aufweist, was auf ein recht stabiles, genaues Modell hinweist.

### Weitere Schritte
{: #io-next}

Wählen Sie eine beliebige einzelne Bereitstellungskachel aus, damit weitere Details zu dieser Bereitstellung angezeigt werden. Weitere Informationen enthalten die Abschnitte [Fairness, durchschnittliche Zahl der Anforderungen pro Minute und Genauigkeit überwachen](/docs/services/ai-openscale?topic=ai-openscale-it-ov) und [Erklärbarkeit überwachen](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).



## Transaktionen
{: #io-tran}

Mit der Registerkarte **Transaktion erklären** (![Registerkarte 'Transaktion erklären'](images/insight-transact-tab.png)) können Sie nach einer bestimmten Transaktions-ID suchen, um eine Erklärung einer bestimmten Bereitstellungstransaktion zu erhalten. Weitere Informationen hierzu enthält der Abschnitt [Erklärbarkeit überwachen](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).


