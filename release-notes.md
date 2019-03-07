---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-07"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Release notes
{: #rn-relnotes}

This document outlines new features and known issues for {{site.data.keyword.aios_full_notm}}.
{: shortdesc}

## 5 March 2019
{: #rn-5March2019}

The following new features and changes to the service are available.

### New features and changes
{: #rn-5March2019nf}

{{site.data.keyword.aios_short}} features that have been added or enhanced since the previous release include:

- __*New Credit Risk model*__: A new Credit Risk model example/tutorial is supported for all scoring engines. For more information see the [Getting started](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted#gettingstarted) and [Additional resources](/docs/services/ai-openscale?topic=ai-openscale-arsc-ov#arsc-ov) topics.

- __*Computing debias*__: You can toggle between your production model and a de-biased model created by {{site.data.keyword.aios_short}}. See [Production model and De-biased model](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-prdb) and [Understanding how de-biasing works](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor#mf-debias) for more information.

## 22 February 2019
{: #rn-22February2019}

The following new features and changes to the service are available.

### New features and changes
{: #rn-22February2019nf}

{{site.data.keyword.aios_short}} features that have been added or enhanced since the previous release include:

- __*UI updates*__: You can import a JSON file to programmatically configure all monitors and features during subscription creation. You can also export the configuration file. See the [Configure deployment subscription using JSON files](/docs/services/ai-openscale?topic=ai-openscale-cf-ov) topic for more information.

## 7 February 2019
{: #rn-7February2019}

The following new features and changes to the service are available.

### New features and changes
{: #rn-7February2019nf}

{{site.data.keyword.aios_short}} features that have been added or enhanced since the previous release include:

- __*UI updates*__: Several improvements have been made to the {{site.data.keyword.aios_short}} user interface, including a way to [check fairness and accuracy on demand](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdep), and the ability to see a list of transactions from the [fairness details chart](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra).

- __*Explainability enhancements*__: All numbers now have the same precision/scale across Pertinent Positive (PP) and Pertinent Negative (PN) values.

- __*Db2 SSL support*__: {{site.data.keyword.aios_short}} supports passing self-signed certificates (Base-64 encoded) with DB2 credentials.

- __*IBM Cloud Database support*__: {{site.data.keyword.aios_short}} now supports Databases for PostgreSQL, in addition to Compose for PostgreSQL and Db2)

### Known issues
{: #rn-7February2019ki}

- **Custom ML service instance**

    - The [Python module](/docs/services/ai-openscale?topic=ai-openscale-as-module) does not currently have Explainability working for the Custom service instance. This is because the Custom service instance requires a numerical prediction in the response data, which is not included with the module script.

## 14 December 2018
{: #rn-14December2018}

The following new features, changes, and known issues with the service are available.

### New features and changes
{: #rn-12nf}

{{site.data.keyword.aios_short}} features that have been added or enhanced since the beta release include:

- __*General availability*__: The General Availability (GA) release of {{site.data.keyword.aios_full_notm}} as an IBM Cloud Standard (paid) plan.

- __*IBM Cloud Private for Data V1.2*__: If you are using {{site.data.keyword.aios_short}} on IBM Cloud Private for Data V1.2, see the documentation, including installation instructions, here: [Installation checklist](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-inst-install-icp#install)

- __*Support for your model type*__: In addition to AI model deployments in Watson Machine Learning, {{site.data.keyword.aios_short}} supports model deployments in Microsoft Azure, Amazon SageMaker, and Custom environments. See [Supported model types](/docs/services/ai-openscale?topic=ai-openscale-in-ov) for more information.

- __*Free "lite" database*__: A free "lite" managed database provides everything you need to begin using {{site.data.keyword.aios_short}}. See the [{{site.data.keyword.aios_short}} pricing plans ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/catalog/services/watson-openscale){: new_window} for details.

- __*Bias monitoring*__: Support for protected attributes of type `float` and `double`, and bias detection on linear regression models. And {{site.data.keyword.aios_short}} can automatically de-bias your AI model for you. See [Understanding fairness](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor) for more information.

- __*Explainability*__: Support for regression models, Python functions, and complementary contrastive explanations. See [Monitoring explainability](/docs/services/ai-openscale?topic=ai-openscale-ie-ov) for more information.

- __*Data Store*__: Quality monitoring without reliance on Watson Machine Learning, and the ability to use your own database, whether it's Db2, Postgres or Db2 on Cloud.

- __*NeuNetS (Beta)*__: The IBM Neural Network Synthesizer (NeuNetS) is available as a beta release (public cloud only). See the [NeuNetS documentation ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://dataplatform.cloud.ibm.com/ml/neunets){: new_window} for more information.

- __*Enhanced UI*__: The {{site.data.keyword.aios_short}} UI has been improved to include a runtime histogram distribution with toggle for training data, Model ID & Versioning, and a Transaction ID table from the histogram. See [Visualizing data for a specific hour](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet) for more information.

- __*Alternate tutorial set-up option*__: To automate the provisioning and configuration of the required IBM Cloud services, and to see an IBM {{site.data.keyword.aios_full}} application, including sample data, you can install and run a Python module. See [Installing a Python module to set up {{site.data.keyword.aios_short}}](/docs/services/ai-openscale?topic=ai-openscale-as-module)

### Known issues
{: #rn-12ki}

- **Microsoft Azure**

    - Of the two types of Azure Machine Learning web services, only the `New` type is supported by {{site.data.keyword.aios_short}}. The `Classic` type is not supported.

    - __*Default input name must be used*__: In the Azure web service, the default input name is `"input1"`. Currently, this field is mandated for {{site.data.keyword.aios_short}} and, if it is missing, {{site.data.keyword.aios_short}} will not work.

      If your Azure web service does not use the default name, change the input field name to `"input1"`, then the code will work.

- **AWS SageMaker**

    - __*BlazingText algorithm is not supported*__: The AWS SageMaker BlazingText algorithm input payload format is not supported in the current release of {{site.data.keyword.aios_short}}.

## 17 September 2018
{: #rn-17September2018}

### New features and changes
{: #rn-17nf}

- **Beta preview release** - Welcome to the beta preview release of {{site.data.keyword.aios_full_notm}}.
