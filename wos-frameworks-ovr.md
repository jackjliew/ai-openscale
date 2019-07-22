---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits

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

# Supported machine learning engines, frameworks, and models
{: #in-fram}

The {{site.data.keyword.aios_short}} service supports the following machine learning engines. Each runtime supports models that are created in the following frameworks:

- [{{site.data.keyword.pm_full}}](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-wml#frmwrks-wml) 
- [Azure ML Studio](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azure#frmwrks-azure)
- [Azure ML Service](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azureservice#frmwrks-azureservice)
- [AWS SageMaker](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-aws-sage#frmwrks-aws-sage)
- [Custom](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-custom#frmwrks-custom)
- [SPSS C&DS](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-spss#frmwrks-spss) (only available in {{site.data.keyword.wos4d_full}})


Full support includes the following features for the specific framework, problem, and data type:

- Payload logging	
- Feedback logging	
- Performance	Accuracy	
- Run-time bias detection	
- Explainability	
- Auto-Debias

<p>&nbsp;</p>


## Supported model types
{: #abt-models}

Table 1. Model support details

| Algorithms | **Fairness** | **Auto-debias** | **Explain** | **Accuracy** |
|:---|:---:|:---:|:---:|:---:|
| **Structured Classification** | Yes | Yes<sup>1</sup> | Yes<sup>1</sup> | Yes |
| **Structured Regression**     | Yes | Coming soon | Yes | Yes |
| **Text Classification**       | No - active research topic | No - active research topic | Yes<sup>1</sup> | No |
| **Image Classification**      | No - active research topic | No - active research topic | Yes<sup>1</sup> | No ||
{: caption="Model support details" caption-side="top"}

<sup>1</sup> Explainability is supported if your model / framework outputs prediction probabilities.

<p>&nbsp;</p>

## Browser support
{: #in-brw}

The {{site.data.keyword.aios_short}} service tooling requires the same level of browser software as is required by {{site.data.keyword.cloud_notm}}. See the {{site.data.keyword.cloud_notm}} [Prerequisites](/docs/overview?topic=overview-prereqs-platform#browsers-platform) topic for details.

<p>&nbsp;</p>

## ModelOps CLI tool
{: #in-mop}

The [{{site.data.keyword.aios_short}} CLI model operations tool](https://github.com/IBM-Watson/aiopenscale-modelops-cli){: external} allows you to execute tasks related to the lifecycle management of machine learning models. This tool is complementary to the {{site.data.keyword.cloud_notm}} CLI tool, augmented with the [machine learning plugin](https://www.ibm.com/support/knowledgecenter/DSXDOC/analyze-data/ml_dlaas_environment.html){: external}.

<p>&nbsp;</p>

## Python client
{: #in-pyc}

The [{{site.data.keyword.aios_short}} Python client](http://ai-openscale-python-client.mybluemix.net/){: external} is a Python library that allows you to work directly with the {{site.data.keyword.aios_short}} service on {{site.data.keyword.cloud_notm}}. You can use the Python client, instead of the {{site.data.keyword.aios_short}} client UI, to directly configure a logging database, bind your machine learning engine, and select and monitor deployments. For examples using the Python client in this way, see the [{{site.data.keyword.aios_short}} sample notebooks](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks).

<p>&nbsp;</p>

## Next steps
{: #in-next}

- View the [API Reference material](https://{DomainName}/apidocs/ai-openscale){: external}.

Still have questions? 

- [What's new](/docs/services/ai-openscale?topic=ai-openscale-rn-relnotes)
- [Contact IBM](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: external}.