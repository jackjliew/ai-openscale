---

copyright:
  years: 2018, 2019
lastupdated: "2019-09-09"

keywords: metrics, monitoring, custom metrics, thresholds, Mean squared error

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

# Mean squared error
{: #quality_squerror}

Mean squared error gives the mean of squared difference between model prediction and target value. It can be used as the measure of the quality of an estimator.
{: shortdesc}

## Mean squared error at a glance
{: #quality_squerror-glance}

- **Description**: Mean of squared difference between model prediction and target value
- **Default thresholds**: Upper limit = 80%
- **Default recommendation**:
   - **Upward trend**: An upward trend indicates that the metric is deteriorating. Feedback data is becoming significantly different than the training data.
   - **Downward trend**: A downward trend indicates that the metric is improving. This means that model retraining is effective.
   - **Erratic or irregular variation**: An erratic or irregular variation indicates that the feedback data is not consistent between evaluations. Increase the minimum sample size for the Quality monitor.
- **Problem type**: Regression
- **Chart values**: Last value in the time frame
- **Metrics details available**: None

## Interpreting the display
{: #quality_squerror-display}

![the Mean squared error chart is displayed.](images/xxxx.png)

## Do the math
{: #quality_squerror-math}

The Mean squared error in its simplest form is represented by the following formual.

```
                         SUM  (Yi - ^Yi) * (Yi - ^Yi)
Mean squared errors  =  ____________________________

                             number of errors
```