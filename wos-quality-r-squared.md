---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, R squared

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

# R squared ![beta tag](images/beta.png)
{: #quality_r_squared}

R squared is the ratio of difference between target variance and variance for prediction error to target variance. It can tell you how well the data that you used to create the model fits the regression.
{: shortdesc}

## R squared at a glance
{: #quality_r_squared-glance}

- **Description**: Ratio of difference between target variance and variance for prediction error to target variance
- **Default thresholds**: Lower limit = 80%
- **Default recommendation**:
   - **Upward trend**: An upward trend indicates that the metric is improving. This means that model retraining is effective.
   - **Downward trend**: A downward trend indicates that the metric is deteriorating. Feedback data is becoming significantly different than the training data.
   - **Erratic or irregular variation**: An erratic or irregular variation indicates that the feedback data is not consistent between evaluations. Increase the minimum sample size for the Quality monitor.
- **Problem type**: Regression
- **Chart values**: Last value in the time frame
- **Metrics details available**: None

## Interpreting the display
{: #quality_r_squared-display}

![the R squared chart is displayed.](images/xxxx.png)

## Do the math
{: #quality_r_squared-math}

The R squared metric is defined in the following formula.

```
                  explained variation
R squared = 1 -  _____________________

                    total variation
```