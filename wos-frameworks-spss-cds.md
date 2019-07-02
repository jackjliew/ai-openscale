---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"


keywords: supported frameworks, models, model types, limitations, limits, spss, c&ds

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# IBM SPSS C&DS frameworks
{: #frmwrks-spss}

{{site.data.keyword.aios_full}} plans to fully support the following IBM SPSS Collaboration and Deployment Services (C&DS) frameworks:
{: shortdesc}

Currently, support is limited to {{site.data.keyword.wos4d_full}}.
{: note}

Table 1. Framework support details

| Framework | Problem type | Data type |
|:---|:---:|:---:|
| SPSS | Classification | Structure |
{: caption="Framework support details" caption-side="top"}

If the `deployment id` for a subscription contains an underscore, the debiased accuracy that normally appears on the debiased tab of fairness metrics will not be seen.
{: note}


## Explainability support for IBM SPSS Collaboration and Deployment Services (C&DS) frameworks
{: #frmwrks-spss-exp-supp}

- Explainability is supported for binary models and for SPSS multiclass models that return probabilities for all classes. 
- Explainability is not supported for SPSS multiclass models that return only the winning class probability.



