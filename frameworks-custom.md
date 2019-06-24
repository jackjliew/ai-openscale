---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

keywords: supported frameworks, models, model types, limitations, limits, custom machine learning engine, custom

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

# Custom ML frameworks
{: #frmwrks-custom}

{{site.data.keyword.aios_full}} fully supports the following custom machine learning frameworks:
{: shortdesc}

Table 1. Framework support details

| Framework | Problem type | Data type |
|:---|:---:|:---:|
| Equivalent to {{site.data.keyword.pm_full}} | Classification | Structured |
{: caption="Framework support details" caption-side="top"}

## Adding a custom machine learning engine to {{site.data.keyword.aios_short}}
{: #frmwrks-custom-add}

You can configure {{site.data.keyword.aios_short}} to work with a custom machine learning provider by using one of the following methods:

- If this is the first time that you are adding a custom machine learning provider to {{site.data.keyword.aios_short}}, you can use the configuration interface. For more information, see [Specifying a custom machine learning instance](/docs/services/ai-openscale?topic=ai-openscale-co-connect).
- You can also add your machine learning provider by using the Python SDK. You must use this method if you want to have more than one provider. For more information on performing this programmatically, see [Bind your custom machine learning engine](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-cusbind).


## Sample notebooks
{: #frmwrks-custom-smpl-ntbks}

- [Creation of Custom Machine Learning engine using Kubernetes cluster](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix){: external}
- [Data mart creation, model deployment monitoring and data analysis](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}

## Explore further
{: #frmwrks-custom-mediumblogs}

[Monitor custom machine learning engine with Watson OpenScale](https://developer.ibm.com/patterns/monitor-custom-machine-learning-engine-with-ai-openscale/){: external}