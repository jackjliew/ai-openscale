---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

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

# Drift detection ![beta tag](images/beta.png)
{: #behavior-drift-ovr}

Over time, the importance and impact of certain features in a model change. This affects the associated applications and resulting business outcomes. Through drift detection, {{site.data.keyword.aios_short}} provides a way to track model metrics, model performance, and the way in which feature weights change over time. Drift is the degradation of predictive performance over time because of hidden context. As your data changes over time, the ability of your model to make accurate predictions may decay. {{site.data.keyword.aios_short}} both detects and highlights drift so that you can take corrective action.
{: shortdesc}

{{site.data.keyword.aios_short}} analyzes all transactions to find the ones that contribute to drift. It then groups the records based on the attribute values that were significant in contributing to drift .

## Drift at a glance
{: #behavior-drift-glance}




## Interpreting the display
{: #behavior-drift-display}

![fairness metrics chart showing drift lower than the set threshold](images/fairness_metrics_001.png)


## Do the math
{: #behavior-drift-math}

{{site.data.keyword.aios_short}} calculates drift 