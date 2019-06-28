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

# Weighted True Positive Rate (wTPR) ![beta tag](images/beta.png)
{: #quality-wtpr}

The Weighted True Positive Rate gives the weighted mean of class TPR with weights equal to class probability.
{: shortdesc)

## Weighted True Positive Rate (wTPR) at a glance
{: #quality-wtpr-glance}

- **Description**: Weighted mean of class TPR with weights equal to class probability
- **Default thresholds**: Lower limit = 80%
- **Default recommendation**:
   - **Upward trend**: An upward trend indicates that the metric is improving. This means that model retraining is effective.
   - **Downward trend**: A downward trend indicates that the metric is deteriorating. Feedback data is becoming significantly different than the training data.
   - **Erratic or irregular variation**: An erratic or irregular variation indicates that the feedback data is not consistent between evaluations. Increase the minimum sample size for the Quality monitor.
- **Problem type**: Multiclass classification
- **Chart values**: Last value in the time frame
- **Metrics details available**: Confusion matrix

## Interpreting the display
{: #quality-wtpr-display}

![Weighted True Positive Rate is displayed](images/quality-tpr.png)

## Do the math
{: #quality-wtpr-math}

The True positive rate is calculated by the following formula:

```
                  number of true positives
TPR =  _________________________________________________________

        (number of true positives + number of false negatives)
```