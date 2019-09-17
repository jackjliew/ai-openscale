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

{{site.data.keyword.aios_short}} detects both [drift in accuracy](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-ovr) and [drift in data](/docs/services/ai-openscale?topic=ai-openscale-behavior-anomalies). 
{: shortdesc}

- [Drop in accuracy](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-ovr)

  Estimates the drop in accuracy of the model at runtime. Model accuracy drops if there is an increase in transactions that are similar to those that the model did not evaluate correctly in the training data. This type of drift is calculated for structured binary and multi-class classification models only.

- [Drop in data consistency](/docs/services/ai-openscale?topic=ai-openscale-behavior-anomalies)

  Estimates the drop in consistency of the data at runtime as compared to the characteristics of the data at training time. 
  
A drop in either model accuracy or data consistency lead to a negative impact on the business outcomes that are associated with the model and must be addressed by retraining the model.

### Drift visualization
{: #behavior-drift-display}

The drift visualization includes both graphical and numeric statistical data:

![fairness metrics chart showing drift lower than the set threshold](images/wos-drift-example.png)

By clicking the chart, you can display specific transactions that contribute to drift. The top reasons for detected drift display and includes a natural-language description of the observation as well as a list of unexpected values.

Specifically, from the **Select a transaction set from the chart or list below** section, you can choose the following views:

- Transactions responsible for drop in accuracy
  
  The following example shows transactions that are responsible for drop in accuracy and data consistency for the German Credit Risk sample model:
  
  ![fairness metrics chart showing drift lower than the set threshold](images/wos-drift-detection-example-accuracy.png)

- Transactions responsible for drop in accuracy and data consistency
   
  The following example shows transactions that are responsible for drop in accuracy and data consistency for the German Credit Risk sample model:
  
  ![fairness metrics chart showing drift lower than the set threshold](images/wos-drift-detection-example.png)
  
- Transactions responsible for drop in data consistency
  
  The following example shows transactions that are responsible for drop in accuracy and data consistency for the German Credit Risk sample model:
  
  ![fairness metrics chart showing drift lower than the set threshold](images/wos-drift-detection-example-data.png)

- Drift transactions are available in the transaction details screen, where you can click **Explain** to understand how a specific transaction has made it into the drift category:
  
  ![fairness metrics chart showing drift lower than the set threshold](images/wos-drift-detection-transactions.png)


## Limitations
{: #behavior-ovr-limitations}

The following limitations apply to the drift monitor:

- Drift is supported for structured data only. 
- Although classification models support both data and accuracy drift, regression models support only data drift. 
- Drift is not supported for Python functions.