---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: explainability, monitoring, explain, explaining, transactions, transaction ID

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Transaktionen erklären
{: #ie-ov}

Für jede Bereitstellung können Sie Erklärungsdaten für bestimmte Transaktionen anzeigen. Transaktionen werden nur angezeigt, wenn Daten zur Unterstützung der Überwachungen vorhanden sind, die auf den von Ihnen festgelegten Schwellenwerten, der geplanten Ausführungszeit für die Überwachungen und der Verfügbarkeit von Nutzdaten aus {{site.data.keyword.pm_full}} beruhen.
{: shortdesc}

## Erklärungen nach Transaktions-ID anzeigen
{: #ie-view}

1. Klicken Sie auf eine Bereitstellungskachel.
2. Klicken Sie auf die Registerkarte **Transaktion erklären** (![Registerkarte 'Transaktion erklären'](images/insight-transact-tab.png)) im Navigator.
3. Geben Sie eine Transaktions-ID ein.

Wann immer Daten zwecks Scoring an das Modell gesendet werden, legt es eine Transaktions-ID im HTTP-Header fest, indem es das Feld `X-Global-Transaction-Id` entsprechend angibt. Diese Transaktions-ID wird in der Nutzdatentabelle gespeichert. Wenn Sie eine Erklärung des Modellverhaltens für ein bestimmtes Scoring suchen, geben Sie die Transaktions-ID an, die dieser Scoring-Anforderung zugeordnet ist. Beachten Sie bitte, dass dieses Verhalten nur {{site.data.keyword.pm_full}}-Transaktionen betrifft und nicht für andere Transaktionen (Nicht-WML-Transaktionen) gilt.
{: note}

## Transaktions-ID in {{site.data.keyword.aios_short}} suchen
{: #ie-find}

1.  Verschieben Sie die Markierung im Zeitdiagramm für Ihre Bereitstellung über das Diagramm und klicken Sie auf den Link **Details anzeigen**, um eine [Visualisierung von Daten eine bestimmte Uhrzeit](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet) anzuzeigen.
1.  Klicken Sie auf die Schaltfläche **Transaktionen anzeigen**, um die [Liste der Transaktions-IDs anzuzeigen](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra).
1.  Kopieren Sie eine der Transaktions-IDs aus der Liste, fügen Sie sie in das Suchfeld auf der Seite **Transaktion erklären** ein und drücken Sie die Eingabetaste.

    Die Liste der Transaktions-IDs bietet auch die Möglichkeit, für eine beliebige Transaktions-ID in der Spalte 'Aktion' einfach auf den Link **Erklären** zu klicken, woraufhin diese Transaktion in der Registerkarte 'Erklärbarkeit' geöffnet wird.
    {: note}

  Die den folgenden Abschnitten enthalten Beispiele für Erklärungen zu verschiedenen Modelltypen.

  ![Transaktions-ID für Erklärbarkeit](images/insight-explain-trans-id.png)

## Erklärungen durch Diagrammdetails suchen
{: #ie-view-ui}

Da es Erklärungen für Fairness- und für Driftmetriken gibt, können Sie auf die Diagramme klicken, um eine detaillierte Ansicht des Datenbestands abzurufen, und anschließend entweder auf die Schaltfläche **Transaktionen anzeigen** (für Fairness-Metriken) oder auf eine Drift-Transaktionskachel, um die Transaktionserklärungen anzuzeigen.

- Klicken Sie bei einem der Fairnessattribute, wie z. B. Geschlecht oder Alter, auf das Attribut, klicken Sie dann auf das Diagramm und danach auf die Schaltfläche **Transaktionen anzeigen**.
- Klicken Sie für die Driftüberwachung auf **Ausmaß der Drift**, klicken Sie auf das Diagramm und dann auf eine Kachel, um die Transaktionen anzuzeigen, die dieser einen Driftgruppe zugeordnet sind.

## Weitere Schritte
{: #ie-trans-id-next}

- [Kategoriale Modelle erklären](/docs/services/ai-openscale?topic=ai-openscale-ie-class)
- [Imagemodelle erklären](/docs/services/ai-openscale?topic=ai-openscale-ie-image)
- [Modelle mit unstrukturiertem Text erklären](/docs/services/ai-openscale?topic=ai-openscale-ie-unstruct)
- [Kontrastierende Erklärungen](/docs/services/ai-openscale?topic=ai-openscale-ie-pp-pn)
