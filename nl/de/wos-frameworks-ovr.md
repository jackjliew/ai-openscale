---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits

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

# Unterstützte Machine Learning-Engines, Frameworks und Modelle
{: #in-fram}

Der {{site.data.keyword.aios_short}}-Service unterstützt die folgenden Machine Learning-Engines. Jede Laufzeit unterstützt Modelle, die in den folgenden Frameworks erstellt werden:

- [{{site.data.keyword.pm_full}}](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-wml#frmwrks-wml) 
- [Azure ML Studio](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azure#frmwrks-azure)
- [Azure ML Service](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azureservice#frmwrks-azureservice)
- [AWS SageMaker](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-aws-sage#frmwrks-aws-sage)
- [Angepasst](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-custom#frmwrks-custom)
- [SPSS C&DS](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-spss#frmwrks-spss) (nur in {{site.data.keyword.wos4d_full}} verfügbar)


Die vollständige Unterstützung umfasst die folgenden Funktionen für das jeweilige Framework, das jeweilige Problem und den jeweiligen Datentyp:

- Protokollierung von Nutzdaten	
- Protokollierung von Rückmeldedaten	
- Genauigkeit der Leistung	
- Verzerrungserkennung zur Laufzeit	
- Erklärbarkeit	
- Automatische Verzerrungsbereinigung

<p>&nbsp;</p>


## Unterstützte Modelltypen
{: #abt-models}

Tabelle 1. Details der Modellunterstützung

| Algorithmen | **Fairness** | **Automatische Verzerrungsbereinigung** | **Erklärung** | **Genauigkeit** |
|:---|:---:|:---:|:---:|:---:|
| **Strukturierte Klassifizierung** | Ja | Ja<sup>1</sup> | Ja<sup>1</sup> | Ja |
| **Strukturierte Regression**     | Ja | In Kürze | Ja | Ja |
| **Textklassifikation**       | Nein - Gegenstand der aktiven Forschung | Nein - Gegenstand der aktiven Forschung | Ja<sup>1</sup> | Nein |
| **Imageklassifikation**      | Nein - Gegenstand der aktiven Forschung | Nein - Gegenstand der aktiven Forschung | Ja<sup>1</sup> | Nein ||
{: caption="Details der Modellunterstützung" caption-side="top"}

<sup>1</sup> Erklärbarkeit wird unterstützt, wenn Ihr Modell/Framework Vorhersagewahrscheinlichkeiten ausgibt.

<p>&nbsp;</p>

## Browserunterstützung
{: #in-brw}

Für die Tools des {{site.data.keyword.aios_short}}-Service ist dieselbe Browsersoftware erforderlich wie für {{site.data.keyword.cloud_notm}}. Genaueres hierzu enthält der Abschnitt {{site.data.keyword.cloud_notm}} [Voraussetzungen](/docs/overview?topic=overview-prereqs-platform#browsers-platform).

<p>&nbsp;</p>

## CLI-Tool für ModelOps
{: #in-mop}

Das [{{site.data.keyword.aios_short}}-CLI-Tool für Modelloperationen](https://github.com/IBM-Watson/aiopenscale-modelops-cli){: external} ermöglicht Ihnen die Ausführung von Tasks, die sich auf das Lebenszyklusmanagement von Machine Learning-Modellen beziehen. Dieses Tool ergänzt das {{site.data.keyword.cloud_notm}}-CLI-Tool und ist mit dem [Machine Learning-Plug-in](https://www.ibm.com/support/knowledgecenter/DSXDOC/analyze-data/ml_dlaas_environment.html){: external} erweitert.

<p>&nbsp;</p>

## Python-Client
{: #in-pyc}

Der [Python-Client für {{site.data.keyword.aios_short}}](http://ai-openscale-python-client.mybluemix.net/){: external} ist eine Python-Bibliothek, die Ihnen ermöglicht, direkt mit dem {{site.data.keyword.aios_short}}-Service in {{site.data.keyword.cloud_notm}} zu arbeiten. Anstelle der Benutzerschnittstelle des {{site.data.keyword.aios_short}}-Clients können Sie den Python-Client verwenden, um eine Datenbank für die Protokollierung direkt zu konfigurieren, Ihre Machine Learning-Engine zu binden und Bereitstellungen auszuwählen und zu überwachen. Beispiele, in denen der Python-Client auf diese Weise verwendet wird, enthalten die [{{site.data.keyword.aios_short}}-Beispielnotebooks](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks).

<p>&nbsp;</p>

## Weitere Schritte
{: #in-next}

- Sichten Sie das [Referenzmaterial für die API](https://{DomainName}/apidocs/ai-openscale){: external}.

Haben Sie immer noch offene Fragen? 

- [Neuerungen](/docs/services/ai-openscale?topic=ai-openscale-rn-relnotes)
- [IBM kontaktieren](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: external}.
