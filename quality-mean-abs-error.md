---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Mean absolute error

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

# Mean absolute error ![beta tag](images/beta.png)
{: #quality_abserror}

Mean absolute error gives the mean of absolute difference between model prediction and target value.
{: shortdesc}

## Mean absolute error at a glance
{: #quality_abserror-glance}

- **Description**: Mean of absolute difference between model prediction and target value
- **Default thresholds**: Upper limit = 80%
- **Default recommendation**:
   - **Upward trend**: An upward trend indicates that the metric is deteriorating. Feedback data is becoming significantly different than the training data.
   - **Downward trend**: A downward trend indicates that the metric is improving. This means that model retraining is effective.
   - **Erratic or irregular variation**: An erratic or irregular variation indicates that the feedback data is not consistent between evaluations. Increase the minimum sample size for the Quality monitor.
- **Problem type**: Regression
- **Chart values**: Last value in the time frame
- **Metrics details available**: None

## Interpreting the display
{: #quality_abserror-display}

![the Mean absolute error chart is displayed.](images/xxxx.png)

## Do the math
{: #quality_abserror-math}

The Mean absolute error is calculated by adding up all the absolute errors and dividing them by the number of errors.

```
                         SUM  | Yi - Xi | 
Mean absolute errors =  ____________________

                          number of errors
```