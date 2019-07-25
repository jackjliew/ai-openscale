---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: machine learning engines, frameworks, Microsoft Azure, Amazone SageMaker, custom ML engine 

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

# Angepasste Machine Learning-Engine
{: #fmrk-workaround-customengine}

Eine angepasste Machine Learning-Engine stellt die Infrastruktur und Hosting-Funktionalität für Machine Learning-Modelle und -Webanwendungen bereit. Angepasste Machine Learning-Engines, die von {{site.data.keyword.aios_short}} unterstützt werden, müssen den folgenden Anforderungen entsprechen:

- Sie müssen zwei Typen von REST-API-Endpunkten zugänglich machen:

   * Erkennungsendpunkte (GET-Liste der Bereitstellungen und Details)
   * Scoring-Endpunkte (Online- und Echtzeit-Scoring)

- Alle Endpunkte müssen mit der Swagger-Spezifikation kompatibel sein, die unterstützt werden soll.

- Die Nutzdaten für die Eingabe in die Bereitstellung und für die Ausgabe aus der Bereitstellung müssen mit dem JSON-Dateiformat konform sein, das in der Spezifikation beschrieben wird.

Zum gegenwärtigen Zeitpunkt werden lediglich die Formate `BasicAuth` oder `none` (Keines) unterstützt.
{: Note}

Im folgenden Beispiel wird die Spezifikation für die REST-API-Endpunkte angezeigt:

![Anzeige der Spezifikation für die REST-API-Endpunkte aus dem Swagger-Dokument](images/wosdeployments.png)


Das folgende Beispiel veranschaulicht das Format für Eingabenutzdaten:

![Anzeige eines Beispiels für Eingabenutzdaten](images/wosinputdata.png)


## Wenn ist die Verwendung einer angepassten Machine Learning-Engine die Option der Wahl?
{: #fmrk-workaround-enging-choice}

Eine angepasste Machine Learning-Engine ist die beste Wahl, wenn die folgenden Situationen zutreffen:

- Sie verwenden keines der verfügbaren Out-of-the-box-Produkte für Ihre Machine Learning-Modelle. Für Ihre Modelle haben Sie gerade ein eigenes System entwickelt. Dafür gibt es weder gegenwärtig noch künftig direkte Unterstützung in {{site.data.keyword.aios_short}}.
- Die von Ihnen verwendete Bedienungsengine eines anderen Anbieters wird von {{site.data.keyword.aios_short}} gegenwärtig (noch) nicht unterstützt. In diesem Fall sollten Sie die Entwicklung einer angepassten Engine für maschinelles Lernen als Wrapper für Ihre ursprünglichen oder nativen Bereitstellungen in Betracht ziehen.

## Weitere Schritte
{: #fmrk-workaround-nxt-steps-over}

Implementieren Sie Ihre eigene Lösung, indem Sie eines der folgenden [Beispiele für angepasstes Machine Learning](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-cstmmlsengex) verwenden.
