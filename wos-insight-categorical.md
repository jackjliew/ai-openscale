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

# Explaining a categorical model
{: #ie-class}

This example of explainability is for a binary classification model that approves or denies insurance claims. You can see the factors that contributed positively or negatively to the final outcome of `DENIED` in this case.
{: shortdesc}

The feature *POLICY AGE* having a value of `< 1 year` had the maximum impact in the model deciding a DENIED outcome. The other features that contributed to this outcome were *CLAIM FREQUENCY* (`High`) and *AGE* (`18`), with only a minor impact from *CAR VALUE* (`$50,000`).

![Explainability binary classification](images/insight-explain-binary.png)

While the charts are useful in showing the most significant factors in determining the outcome of a transaction, classification models can also include advanced explanations, detailed in the `Minimum changes for Approved outcome` and `Minimum changes for this outcome` sections.

Advanced explanations are not available for regression, image, and unstructured text models.
{: note}

The `Minimum changes for Approved outcome` tells us that, if the values of the features were changed to the values listed in this section, then the prediction of the model will change.

Likewise, the `Minimum changes for this outcome` tells us that, even if the values of the features were changed to those listed in this section, the prediction of the model would not have changed.

Thus, these two values tell us the behavior of the model in the vicinity of the data point for which the explanation is being generated.

![Explainability binary classification](images/insight-explain-binary2.png)