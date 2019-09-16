---

copyright:
  years: 2018, 2019
lastupdated: "2019-09-09"

keywords: FAQs, frequently asked questions, questions

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

# FAQs
{: #wos-faqs}

Here you'll find some of the most frequently-asked questions from users of {{site.data.keyword.aios_full}}.
{: shortdesc}

## Questions
{: #wos-faqs-questions}

- [What is {{site.data.keyword.aios_short}}?](#faq-whatsa)
- [How is {{site.data.keyword.aios_short}} priced?](#faq-pricing)
- [Is there a free trial for {{site.data.keyword.aios_short}}?](#faq-freetrial)
- [All of my AI models are in Azure. Can I use Microsoft Azure ML engine with {{site.data.keyword.aios_short}}?](#faq-azure)
- [All of my AI models are in Amazon. Can I use Amazon SageMaker ML engine with {{site.data.keyword.aios_short}}?](#faq-sagemaker)
- [Is {{site.data.keyword.aios_short}} available on {{site.data.keyword.icp4dfull_notm}}?](#faq-icp)
- [I want to run {{site.data.keyword.aios_short}} on my own servers. How much computer processing power should I allocate?](#faq-sizing)
- [How do I convert a prediction column from an integer data type to a categorical data type?](#wos-faqs-convert-data-types)
- [Why does {{site.data.keyword.aios_short}} need access to my training data?](#trainingdata)
- [What internet browser does {{site.data.keyword.aios_short}} support?](#in-brw)
- [Is there a command line tool that I can use?](#in-mop)
- [What version of Python can I use with {{site.data.keyword.aios_short}}?](#in-pyc)

<p>&nbsp;</p>


### What is {{site.data.keyword.aios_short}}
{: #faq-whatsa}

{{site.data.keyword.aios_full}} tracks and measures outcomes from your AI models, and helps ensure they remain fair, explainable and compliant wherever your models were built or are running. {{site.data.keyword.aios_short}} also detects and helps correct the drift in accuracy when an AI model is in production

Get a quick overview of {{site.data.keyword.aios_short}} by watching the following video:

<p>
  <div class="embed-responsive embed-responsive-16by9">
     <iframe class="embed-responsive-item" id="WOS-bias-vid" title="Mitigating AI Bias with IBM Watson OpenScale" type="text/html" src="https://cdnapisec.kaltura.com/p/1773841/sp/177384100/embedIframeJs/uiconf_id/39954662/partner_id/1773841?iframeembed=true&playerId=kplayer&entry_id=1_1shu3261&flashvars[streamerType]=auto" width="560" height="395" allowfullscreen webkitallowfullscreen mozAllowFullScreen allow="autoplay *; fullscreen *; encrypted-media *" frameborder="0"></iframe>
  </div>
</p>


<p>&nbsp;</p>


### How is {{site.data.keyword.aios_short}} priced?
{: #faq-pricing}

When your ready to transition from the Lite plan, there's a **Standard** pricing plan that includes monitoring of up to 24 deployed models, with no restrictions on the number of payload, feedback rows or transactions for Explainability. The up-to-date information is availabe in the [{{site.data.keyword.Bluemix}} catalog](https://cloud.ibm.com/catalog/services/watson-openscale?cm_sp=WatsonPlatform-WatsonPlatform-_-OnPageNavCTA-IBMWatson_OpenScale-_-AIOSProductPage){: external}.

<p>&nbsp;</p>


### Is there a free trial for {{site.data.keyword.aios_short}}?
{: #faq-freetrial}

{{site.data.keyword.aios_short}} offers a free trial through the Lite plan. To sign up, visit the [{{site.data.keyword.aios_short}} web page](https://www.ibm.com/cloud/watson-openscale/){: external} and click **Get started now**. You'll be able to use the Lite plan for as long as you want (subject to monthly usage limits which refresh every month).

<p>&nbsp;</p>


### All of my AI models are in Azure. Can I use Microsoft Azure ML engine with {{site.data.keyword.aios_short}}?
{: #faq-azure}

{{site.data.keyword.aios_short}} supports both Microsoft Azure ML Studio and Microsoft Azure ML Service engines. For more information, see [Microsoft Azure ML Studio frameworks](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-frmwrks-azure) and [Microsoft Azure ML Service frameworks](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-frmwrks-azure-service).

<p>&nbsp;</p>


### All of my AI models are in Amazon. Can I use Amazon SageMaker ML engine with {{site.data.keyword.aios_short}}?
{: #faq-sagemaker}

{{site.data.keyword.aios_short}} supports Amazon SageMaker ML engine. For more information, see [Amazon SageMaker frameworks](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-frmwrks-aws-sage).

<p>&nbsp;</p>


### Is {{site.data.keyword.aios_short}} available on {{site.data.keyword.icp4dfull_notm}}?
{: #faq-icp}

{{site.data.keyword.aios_short}} is one of the premium add-ons for {{site.data.keyword.icp4dfull_notm}}. 

<p>&nbsp;</p>


### I want to run {{site.data.keyword.aios_short}} on my own servers. How much computer processing power should I allocate?
{: #faq-sizing}

There are specific guidelines for [hardware configuration](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-inst-install-icp#inst-hwt) for three-node and six-node configurations. Your IBM Technical Sales team can also help you with sizing your specific configuration. Because {{site.data.keyword.aios_short}} run as an add-on to {{site.data.keyword.icp4dfull_notm}}, you need to consider the requirements for both software products.

<p>&nbsp;</p>


### How do I convert a prediction column from an integer data type to a categorical data type?
{: #wos-faqs-convert-data-types}

When configuring fairness monitoring for a model, the prediction column only allows for integer numerical value even though the prediction label is categorical How do I configure this for categorical feature (that is not integer)? is a manual conversion required? 

The training data could have class labels such as “Loan Denied”, “Loan Granted”. The prediction value returned by {{site.data.keyword.pm_full}} scoring end point has values such as “0.0”, “1.0", etc. The scoring end point also has an optional column which contains the text representation of prediction. E.g., if prediction=1.0, the predictionLabel column could have a value “Loan Granted”. If such a column is available, then while configuring the favourable and unfavourable outcome for the model, you can specify the string values “Loan Granted” and “Loan Denied”. If such a column is not available then you need to specify the integer/double values of 1.0, 0.0 for the favourable/unfavourable class.

{{site.data.keyword.pm_full}} has a concept of output schema which defines the schema of the output of {{site.data.keyword.pm_full}} scoring end point and the role for the different columns. The roles are used to identify which column contains the prediction value, which column contains the prediction probability, and the class label value, etc. The output schema is automatically set for models created using model builder. It can also be set using the {{site.data.keyword.pm_full}} Python client. Users can use the output schema to define a column which contains the string representation of the prediction. This is done by setting the modeling_role for the column to ‘decoded-target’. The documentation for the {{site.data.keyword.pm_full}} Python client is available at: http://wml-api-pyclient-dev.mybluemix.net/#repository. Search for “OUTPUT_DATA_SCHEMA” to understand the output schema and the API to use is to store_model API which accepts the OUTPUT_DATA_SCHEMA as a parameter.

<p>&nbsp;</p>


### Why does {{site.data.keyword.aios_short}} need access to my training data?
{: #trainingdata}

You must either provide {{site.data.keyword.aios_short}} access to training data that is stored in Db2 or {{site.data.keyword.cos_full_notm}}, or you must run a notebook that can access the training data. {{site.data.keyword.aios_short}} needs access to your training data for the following reasons:

- To generate contrastive explanations: To create explanations, access to statistics, such as median value, standard deviation, and distinct values from the training data is required.
- To display training data statistics: To populate the bias details page, {{site.data.keyword.aios_short}} must have training data from which to generate statistics.

In the notebook-based approach, you are expected to upload the statistics and other information when configuring a deployment in {{site.data.keyword.aios_short}}. This implies that {{site.data.keyword.aios_short}} no longer has access to the training data outside the notebook, which is run in your environment. It only has access to the information uploaded during the configuration.

<p>&nbsp;</p>


### What internet browser does {{site.data.keyword.aios_short}} support?
{: #in-brw}

The {{site.data.keyword.aios_short}} service tooling requires the same level of browser software as is required by {{site.data.keyword.cloud_notm}}. See the {{site.data.keyword.cloud_notm}} [Prerequisites](/docs/overview?topic=overview-prereqs-platform#browsers-platform){: external} topic for details.

<p>&nbsp;</p>

### Is there a command line tool that I can use? 
{: #in-mop}

Yes! It's commonly referred to as the ModelOps CLI tool, but its official name is the [{{site.data.keyword.aios_short}} CLI model operations tool](https://github.com/IBM-Watson/aiopenscale-modelops-cli){: external}. Use it to execute tasks related to the lifecycle management of machine learning models. This tool is complementary to the {{site.data.keyword.cloud_notm}} CLI tool, augmented with the [machine learning plugin](https://www.ibm.com/support/knowledgecenter/DSXDOC/analyze-data/ml_dlaas_environment.html){: external}.

<p>&nbsp;</p>

### What version of Python can I use with {{site.data.keyword.aios_short}}?
{: #in-pyc}

Because {{site.data.keyword.aios_short}} is designed to be independent of your model-creation process, it supports whatever Python versions your machine learning provider supports. The [{{site.data.keyword.aios_short}} Python client](http://ai-openscale-python-client.mybluemix.net/){: external} is a Python library that allows you to work directly with the {{site.data.keyword.aios_short}} service on {{site.data.keyword.cloud_notm}}. For the most up-to-date version information, see [the Requirements section](http://ai-openscale-python-client.mybluemix.net/#requirements){: external}. You can use the Python client, instead of the {{site.data.keyword.aios_short}} client UI, to directly configure a logging database, bind your machine learning engine, and select and monitor deployments. For examples using the Python client in this way, see the [{{site.data.keyword.aios_short}} sample notebooks](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks){: external}.

<p>&nbsp;</p>

