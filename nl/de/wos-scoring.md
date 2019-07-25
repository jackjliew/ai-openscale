---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: databases, connections, scoring, requests

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

# Scoring-Anforderung senden
{: #cdb-score}

Zum Konfigurieren von Überwachungen ist für {{site.data.keyword.aios_short}} das Senden von Scoring-Nutzdaten erforderlich, damit mit dem Protokollieren der zu überwachenden Daten begonnen werden kann.

- Bei in {{site.data.keyword.pm_full}} bereitgestellten Modellen haben Sie die Möglichkeit, in {{site.data.keyword.pm_full}} ein Scoring für bereitgestellte Modelle durchzuführen oder die API für Nutzdatenprotokollierung für das Scoring zu verwenden. Bereitgestellte Modelle, für die ein Scoring in {{site.data.keyword.pm_short}} durchgeführt wird, werden automatisch an {{site.data.keyword.aios_short}} gesendet. 
- Bei anderen Machine Learning-Engines, wie z. B. Microsoft Azure, Amazon SageMaker oder einer angepassten Machine Learning-Engine, müssen die Scoringnutzdaten über die API für die Nutzdatenprotokollierung gesendet werden. Weitere Informationen hierzu finden Sie im Abschnitt [Nutzdatenprotokollierung für andere Serviceinstanzen als {{site.data.keyword.pm_full}}-Serviceinstanzen](/docs/services/ai-openscale?topic=ai-openscale-cml-connect).

## Schritte zur Nutzdatenprotokollierung
{: #cdb-score-apisteps}

1. Wählen Sie eine Bereitstellung aus und wechseln Sie zur Seite **Nutzdatenprotokollierung**.
2. Wählen Sie aus, ob der `cURL`- oder `Python`-Code verwendet werden soll, indem Sie auf die Registerkarte `cURL` oder `Python` klicken.
3. Klicken Sie auf **In Zwischenablage kopieren** und fügen Sie die Zwischenablage ein, um Anforderungs- und Antwortdaten der Modellbereitstellung zu protokollieren. Weitere Informationen hierzu finden Sie im Abschnitt [Nutzdatenprotokollierung für andere Serviceinstanzen als {{site.data.keyword.pm_full}}-Serviceinstanzen](/docs/services/ai-openscale?topic=ai-openscale-cml-connect).

Die Felder und Werte in den Code-Snippets müssen durch die tatsächlichen Werte ersetzt werden, da es sich bei den angegebenen Werten lediglich um Beispiele handelt.
{: important}

![Datenbank auswählen](images/config-send-scoring.png)

Nach der Nutzdatenprotokollierung wird für die ausgewählte Bereitstellung in der Spalte **Bereit zur Überwachung** ein Häkchen angezeigt. Klicken Sie zum Fortfahren auf **Überwachungen konfigurieren**.

## Erläuterungen zur Anzahl der Scoring-Anforderungen
{: #cdb-score-capacity}

Scoring-Anforderungen sind ein integraler Bestandteil der {{site.data.keyword.aios_short}}-Verarbeitung. Jeder Transaktionsdatensatz, den Sie an das zu bewertende Modell senden, generiert eine zusätzliche Verarbeitung, damit der {{site.data.keyword.aios_short}}-Service eine Perturbation durchführen und Erklärungen erstellen kann.

- Bei Tabellen-, Text- und Imagemodellen generiert die folgende Basisanforderung Datenpunkte:

   - 1 Scoring-Anforderung generiert 5000 Datenpunkte.

- Für Tabellenklassifizierungsmodelle gibt es zusätzliche Scoring-Anforderungen, die für eine kontrastive Erklärung konzipiert sind. Die folgenden Anforderungen werden zur Basisanforderung hinzugefügt:

   - 100 Scoring-Anforderungen generieren 51 zusätzliche Datenpunkte pro Anforderung.
   - 101 Scoring-Anforderungen generieren 1 zusätzlichen Datenpunkt pro Anforderung.


## Weitere Schritte
{: #cdb-score-next-steps-scoringreq}

[Überwachungen konfigurieren](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-mo-config).
