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

# Integration von Machine Learning-Engines anderer Anbieter mit {{site.data.keyword.aios_short}}
{: #fmrk-workaround}

Eine Integration von externen Service-Engines für Machine Learning wie Microsoft Azure ML Studio und Amazon SageMaker mit {{site.data.keyword.aios_full}} ist möglich.
{: shortdesc}

Sie können {{site.data.keyword.aios_short}} auf verschiedene Weise mit Engines anderer Anbieter integrieren:

- Ebene der Enginebindungen: Möglichkeit zum Auflisten von Bereitstellungen und Abrufen von Bereitstellungsdetails.
  
- Ebene der Bereitstellungsabonnements: {{site.data.keyword.aios_short}} muss in der Lage sein, ein Scoring für die abonnierte Bereitstellung im erforderlichen Format, z. B. im {{site.data.keyword.pm_full}}-Format, durchzuführen und die Ausgabe in demselben kompatiblen Format zu empfangen. {{site.data.keyword.aios_short}} muss für die Verarbeitung von Eingabe- als auch von Ausgabeformaten konfiguriert sein.
   

- Nutzdatenprotokollierung: Jede Ein- und Ausgabe des bereitgestellten Modells, die durch eine Anwendung eines Benutzers ausgelöst wird, muss in einem Nutzdatenspeicher gespeichert werden. Das Format der Datensätze für Nutzdaten entspricht derselben Spezifikation wie der im vorhergehenden Abschnitt zu den Ebenen von Bereitstellungsabonnements genannten.
   
   {{site.data.keyword.aios_short}} verwendet diese Datensätze, um Verzerrungen, Erklärungen und andere Angaben zu berechnen. {{site.data.keyword.aios_short}} ist nicht in der Lage, automatisch Transaktionen zu speichern, die auf der Benutzersite ausgeführt werden, die sich außerhalb des {{site.data.keyword.aios_short}}-Systems befindet. Dies ist eine der Methoden, die {{site.data.keyword.aios_short}} verwendet, um urheberrechtlich geschützte Informationen zu schützen. Verwenden Sie die REST-API oder das Python-SDK von {{site.data.keyword.aios_short}}, um mit gesicherten Daten zu arbeiten.
   
## Schritte zur Implementierung der Lösung
{: #fmrk-workaround-steps}

1. [Informationen zu angepassten Machine Learning-Engines](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-customengine).
2. [Nutzdatenprotokollierung einrichten](/docs/services/ai-openscale?topic=ai-openscale-cdb-payload).
3. [Nutzdatenprotokollierung automatisieren](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-pyld-lg).
4. Angepasste Machine Learning-Engine mithilfe der [Beispiele für angepasste Machine Learning-Engine](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-cstmmlsengex) einrichten.

