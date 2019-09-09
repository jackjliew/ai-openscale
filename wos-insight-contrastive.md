---

copyright:
  years: 2018, 2019
lastupdated: "2019-09-09"

keywords: accuracy, LIME, contrastive, explainability, pertinent positives, pertinent negatives

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

For contrastive explanations, {{site.data.keyword.aios_short}} displays pertinent positive and pertinent negative values. These help explain the behavior of the model in the vicinity of the data point for which an explanation is generated.
{: shortdesc}

- Pertinent positives (PP) are feature values obtained by changing the value of each feature towards its median such that the model prediction remains the same.

  ![pertinent positive panel is displayed and shows features and maximum values that allow for the same outcome](images/wos-contrastive-pp.png)

- Pertinent negatives (PN) are feature values obtained by changing the value of each feature away from its median such that the model prediction changes.

  ![pertinent negative panel is displayed and shows features and minimum values that allow for a different outcome](images/wos-contrastive-pn.png)


Consider an example of a model used for loan processing. It can have one of three predictions: Loan Approved, Loan Partially Approved and Loan Denied. For the sake of simplicity, let us assume that the model takes only one feature in input: salary. Let us consider a data point where the salary=150000 and the model predicts Loan Partially Approved. Let the median value of salary be 90000. A pertinent positive could be: Even if the salary of the person was 100000, the model would have still predicted Loan Partially Approved. On the other hand, the pertinent negative will be: If the salary of the person was 200000, the model prediction would have changed to Loan Approved. Thus PP and PP together are explaining the behaviour of the model in the vicinity of the data point for which explanation is to be generated.

{{site.data.keyword.aios_short}} always displays a pertinent positive, however, sometimes there are no pertinent negatives to be displayed. To understand this better, consider that when {{site.data.keyword.aios_short}} calculates the pertinent negative value, it changes the values of all the features away from their median value. If even after changing the value away from median, the prediction does not change, then there are no pertinent negatives to display. In case of pertinent positives, {{site.data.keyword.aios_short}} finds the maximum change in the feature values towards the median such that the prediction does not change. Practically, this means that there is almost always a pertinent positive to explain a transaction (and it could be the feature value of the input data point itself).

![no pertinent negative displays, instead there is a message that explains that values are already at the median or the prediction has not changed as a rsult of moving values from the median](images/wos-contrastive-no-pn.png)

## Understanding the difference between contrastive explanations and LIME
{: #ie-pp-pn}

Local Interpretable Model-Agnostic Explanations (LIME) is a Python library that {{site.data.keyword.aios_short}} uses to analyze the input and ouput values of a model to create human-understandable interpretations of the model. Both LIME and contrastive explanation are valuable tools for making sense of a model, however, they offer very different perspectives. Contrastive explanations reveal how much values need to change to either change the prediction or still have the same prediction. The factors which need the maximum change are considered more important in this type of explanation. In other words the features with highest importance in contrastive explanations are those where the model is least sensitive. On the other hand, LIME reveals which features are most important for a specific data point. The 5000 perturbations that are typically done for analysis are very close to the data point and in an ideal setting the features with high importance in LIME are those which are most important for that specific data point. For these reasons, the features with high importance for LIME and those for contrastive explanations can be very different.


