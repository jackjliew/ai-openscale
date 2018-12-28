---

copyright:
  years: 2018
lastupdated: "2018-12-20"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Release notes

This document outlines new features and known issues for {{site.data.keyword.aios_full_notm}}.
{: shortdesc}

## 14 December 2018
{: #14December2018}

The following new features, changes, and known issues with the service are available.

### New features and changes

{{site.data.keyword.aios_short}} features that have been added or enhanced since the beta release include:

- __*General availability*__: The General Availability (GA) release of {{site.data.keyword.aios_full_notm}} as an IBM Cloud Standard (paid) plan.

- __*IBM Cloud Private for Data V1.2*__: If you are using {{site.data.keyword.aios_short}} on IBM Cloud Private for Data V1.2, see the documentation, including installation instructions, here: [https://cloud.ibm.com/docs/services/ai-openscale-icp/install-icp.html#install ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/docs/services/ai-openscale-icp/install-icp.html#install)

- __*Support for your model type*__: In addition to AI model deployments in Watson Machine Learning, {{site.data.keyword.aios_short}} supports model deployments in Microsoft Azure, Amazon SageMaker, and Custom environments. See [Supported model types](/docs/services/ai-openscale/index.html#supported-model-types) for more information.

- __*Free "lite" database*__: A free "lite" managed database provides everything you need to begin using {{site.data.keyword.aios_short}}. See the [{{site.data.keyword.aios_short}} pricing plans ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/catalog/services/ai-openscale) for details.

- __*Bias monitoring*__: Support for protected attributes of type `float` and `double`, and bias detection on linear regression models. And {{site.data.keyword.aios_short}} can automatically de-bias your AI model for you. See [Understanding fairness](/docs/services/ai-openscale/monitor-fairness.html#understand-fair) for more information.

- __*Explainability*__: Support for regression models, Python functions, and complementary contrastive explanations. See [Monitoring explainability](/docs/services/ai-openscale/insight-explain.html) for more information.

- __*Data Store*__: Quality monitoring without reliance on Watson Machine Learning, and the ability to use your own database, whether it's Db2, Postgres or Db2 on Cloud.

- __*NeuNetS (Beta)*__: The IBM Neural Network Synthesizer (NeuNetS) is available as a beta release (public cloud only). See the [NeuNetS documentation](https://dataplatform.cloud.ibm.com/ml/neunets) for more information.

- __*Enhanced UI*__: The {{site.data.keyword.aios_short}} UI has been improved to include a runtime histogram distribution with toggle for training data, Model ID & Versioning, and a Transaction ID table from the histogram. See [Visualizing data for a specific hour](/docs/services/ai-openscale/insight-timechart.html#insight-data-visual) for more information.

- __*Alternate tutorial set-up option*__: To automate the provisioning and configuration of the required IBM Cloud services, and to see an IBM AI OpenScale application, including sample data, you can install and run a Python module. See [Installing a Python module to set up AI OpenScale](https://cloud.ibm.com/docs/services/ai-openscale/alt-setup.html)

### Known issues

- **Microsoft Azure**

    - Of the two types of Azure Machine Learning web services, only the `New` type is supported by {{site.data.keyword.aios_short}}. The `Classic` type is not supported.

    - __*Default input name must be used*__: In the Azure web service, the default input name is `"input1"`. Currently, this field is mandated for {{site.data.keyword.aios_short}} and, if it is missing, {{site.data.keyword.aios_short}} will not work.

      If your Azure web service does not use the default name, change the input field name to `"input1"`, then the code will work.

- **AWS SageMaker**

    - __*BlazingText algorithm is not supported*__: The AWS SageMaker BlazingText algorithm input payload format is not supported in the current release of {{site.data.keyword.aios_short}}.

## 17 September 2018
{: #17September2018}

### New features and changes

- **Beta preview release** - Welcome to the beta preview release of {{site.data.keyword.aios_full_notm}}.
