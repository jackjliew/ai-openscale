---

copyright:
  years: 2018, 2019
lastupdated: "2019-09-09"

keywords: drift, anomalies, data, data drift, drift detection, transactions

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

# Drift in data
{: #behavior-anomalies}

In addition to checking for the drift in model accuracy, the drift monitor can detect the drift in data. This type of drift is defined as something that deviates from what is standard, normal, or expected. {{site.data.keyword.aios_short}} detects data drift so that you can make changes to the model.
{: shortdesc}

## Understanding drift detection
{: #behavior-anomalies-understand}

Drift is the degradation of predictive performance over time because of hidden context. As your data changes over time, the ability of your model to make accurate predictions may deteriorate. {{site.data.keyword.aios_short}} both detects and highlights drift so that you can take corrective action.

### How it works
{: #behavior-anomalies-works}

{{site.data.keyword.aios_short}} analyzes all transactions to find the ones that contribute to drift. It then groups the records based on the similarity of data inconsistency patterns that were significant in contributing to drift.



### Do the math
{: #behavior-anomalies-math}

Data drift determines the extent of the drift in the features of the model. Every three hours, {{site.data.keyword.aios_short}} calculates data drift by analyzing all transactions for data inconsistency by
comparing the transaction data with the training data. Where there are changes or discrepancies, {{site.data.keyword.aios_short}} calculates the extent of the data drift.

### Drift visualization
{: #behavior-anomalies-display}

The drift visualization includes both graphical and numeric statistical data:

![fairness metrics chart showing drift lower than the set threshold](images/wos-drift-example.png)

By clicking the chart, you can display specific transactions that contribute to drift. The top reasons for detected drift display and includes a natural-language description of the observation as well as a list of unexpected values.

![fairness metrics chart showing drift lower than the set threshold](images/wos-drift-detection-example.png)

Drift transactions are available in the transaction details screen, where you can click **Explain** to understand how a specific transaction has made it into the drift category:

![fairness metrics chart showing drift lower than the set threshold](images/wos-drift-detection-transactions.png)


## Next steps
{: #behavior-anomalies-ns}

- For information on how to set up drift detection, see [Configuring the drift detection monitor](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-config).
- To mitigate drift, after it has been detected by Watson OpenScale, you must build a new version of the model that fixes the problem. A good place to start is with the data points that are highlighted as reasons for the drift. Introduce the new data to the predictive model after you have manually labeled the drifted transactions and use them to re-train the model.
