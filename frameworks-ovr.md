---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: supported frameworks, models, model types, limitations, limits

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
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
- [AWS SageMaker](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-aws-sage#frmwrks-aws-sage)
- [Custom](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-custom#frmwrks-custom)
- [SPSS C&DS](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-spss#frmwrks-spss) (only available in {{site.data.keyword.wos4d_full}})

- [SAS AI Studio](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-sas#frmwrks-sas)
{: download}
- [Google Cloud ML Engine](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-google#frmwrks-google)
{: download}

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

<sup>1</sup> If your model / framework outputs prediction probabilities

<p>&nbsp;</p>

## Browser support
{: #in-brw}

The {{site.data.keyword.aios_short}} service tooling requires the same level of browser software as is required by {{site.data.keyword.cloud_notm}}. See the {{site.data.keyword.cloud_notm}} [Prerequisites](/docs/overview?topic=overview-prereqs-platform#browsers-platform) topic for details.

<p>&nbsp;</p>

## ModelOps CLI tool
{: #in-mop}

The [{{site.data.keyword.aios_short}} CLI model operations tool ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Watson/aiopenscale-modelops-cli){: new_window} allows you to execute tasks related to the lifecycle management of machine learning models. This tool is complementary to the {{site.data.keyword.cloud_notm}} CLI tool, augmented with the [machine learning plugin ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/DSXDOC/analyze-data/ml_dlaas_environment.html){: new_window}.

<p>&nbsp;</p>

## Python client
{: #in-pyc}

The [{{site.data.keyword.aios_short}} Python client ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://ai-openscale-python-client.mybluemix.net/){: new_window} is a Python library that allows you to work directly with the {{site.data.keyword.aios_short}} service on {{site.data.keyword.cloud_notm}}. You can use the Python client, instead of the {{site.data.keyword.aios_short}} client UI, to directly configure a logging database, bind your machine learning engine, and select and monitor deployments. For examples using the Python client in this way, see the [{{site.data.keyword.aios_short}} sample notebooks ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks).

<p>&nbsp;</p>

## Next steps
{: #in-next}

- [Get started](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted) with the service.
- View the [API Reference material ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/ai-openscale){: new_window}.

Still have questions? 

- [What's new](/docs/services/ai-openscale?topic=ai-openscale-rn-relnotes)
- [Contact IBM ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: new_window}.
