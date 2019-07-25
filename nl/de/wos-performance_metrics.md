---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds

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

# Übersicht zu Leistungsmetriken ![Beta-Tag](images/beta.png)
{: #anlz_metrics_performance}

Mithilfe der Leistungsüberwachung können Sie die Geschwindigkeit ermitteln, mit der Datensätze in Ihrer Bereitstellung verarbeitet werden. Die Leistungsüberwachung wird bei der Auswahl der Bereitstellung aktiviert, die mithilfe von {{site.data.keyword.aios_short}} verfolgt und überwacht werden soll.
{: shortdesc}

Leistungsmetriken werden auf der Basis der folgenden Informationen berechnet:

- Scoring-Nutzdaten

Für eine korrekte Überwachung muss jede Scoring-Anforderung auch in {{site.data.keyword.aios_short}} protokolliert werden. Die Protokollierung von Nutzdaten ist für {{site.data.keyword.pm_full}}-Engines automatisiert. Bei anderen Machine Learning-Engines können die Nutzdaten entweder über den Python-Client oder über die REST-API bereitgestellt werden. Bei der Leistungsüberwachung werden keine zusätzlichen Scoring-Anforderungen für die überwachte Bereitstellung erstellt.

Leistungsmetrikwerte für einen bestimmten Zeitraum können im {{site.data.keyword.aios_short}}-Dashboard überwacht werden:

![Leistungsdiagramm](images/performance_metrics_001.png)

## Unterstützte Leistungsmetriken
{: #anlz_metrics_performance_supp_quality_mets}

Die folgenden Leistungsmetriken werden von {{site.data.keyword.aios_short}} unterstützt:

- [Durchsatz](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-performance_mets_through)
