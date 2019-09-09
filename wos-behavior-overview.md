---

copyright:
  years: 2018, 2019
lastupdated: "2019-09-09"

keywords: fairness, fairness monitor, payload, perturbation, training data, debiased

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

# Drift detection
{: #behavior-ovr}

{{site.data.keyword.aios_short}} detects both [drift in accuracy](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-ovr) and [drift in data](/docs/services/ai-openscale?topic=ai-openscale-behavior-anomalies). Drift is supported for structured data only. Regression models support data drift, while classification models support both data and accuracy drift.
{: shortdesc}

- [Drop in accuracy](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-ovr)

  Estimates the drop in accuracy of the model at runtime. Model accuracy drops if there is an increase in transactions that are similar to those that the model did not evaluate correctly in the training data. This type of drift is calculated for structured binary and multi-class classification models only.

- [Drop in data consistency](/docs/services/ai-openscale?topic=ai-openscale-behavior-anomalies)

  Estimates the drop in consistency of the data at runtime as compared to the characteristics of the data at training time. 
  
A drop in either model accuracy or data consistency lead to a negative impact on the business outcomes that are associated with the model and must be addressed by retraining the model.