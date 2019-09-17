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



Every three hours, {{site.data.keyword.aios_short}} analyzes each transaction for data inconsistency, by comparing the transaction content with the training data patterns. If a transaction violates one or more of the training data patterns, the transaction is marked as drifted. {{site.data.keyword.aios_short}} then estimates the magnitude of data inconsistency as the fraction of drifted transactions to the total number of transactions analyzed. Further, {{site.data.keyword.aios_short}} analyzes all the drifted transactions; and then, groups transactions that violate similar training data patterns into different clusters. In each cluster, {{site.data.keyword.aios_short}} also estimates the important features that played a major role in the data inconsistency and classifies their feature impact as large, some, and small.

## Next steps
{: #behavior-anomalies-ns}

- For information on how to set up drift detection, see [Configuring the drift detection monitor](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-config).
- To mitigate drift, after it has been detected by Watson OpenScale, you must build a new version of the model that fixes the problem. A good place to start is with the data points that are highlighted as reasons for the drift. Introduce the new data to the predictive model after you have manually labeled the drifted transactions and use them to re-train the model.
