---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: fairness, monitoring, charts, de-biasing, bias, accuracy

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

# Contrastive explanations use pertinent positives and pertinent negatives
{: #ie-pp-pn}

For contrastive explanations, {{site.data.keyword.aios_short}} displays pertinent positive and pertinent negative values. 
{: shortdesc}

- Pertinent positives are findings that are critical for determining what something is.
- Pertinent negatives are non-findings that are important by their absence.

{{site.data.keyword.aios_short}} always displays a pertinent positive, however, sometimes there are no pertinent negatives to be displayed. In this case, values for this feature are either already at the median or the prediction has not changed as a result of moving values away from the median.

To understand this better, consider that when {{site.data.keyword.aios_short}} calculates the pertinent negative value, it changes the values of all the features away from their median value. For pertinent negatives this means the feature values that are farthest away from the median. If the values of a data point are already at the median or if even after changing the value away from median, the prediction does not change, then there are no pertinent negatives to display. In case of pertinent positives, {{site.data.keyword.aios_short}} finds the maximum change in the feature values towards the median such that the prediction does not change. Practically, this means that there is almost always a pertinent positive to explain a transaction.

