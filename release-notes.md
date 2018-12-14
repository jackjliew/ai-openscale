---

copyright:
  years: 2018
lastupdated: "2018-12-13"

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

The following new features and changes to the service are available.

### New features and changes

- **GA release**

    - Welcome to the General Availability (GA) release of {{site.data.keyword.aios_full_notm}}. This release contains the following features:

<!---
        - __*Releases*__: {{site.data.keyword.aios_short}} is available as an IBM Cloud Standard (paid) plan, and on IBM Cloud Private for Data V1.2

          The IBM Neural Network Synthesizer (NeuNetS) is also available as a beta release (public cloud only). See the [NeuNetS documentation](https://dataplatform.cloud.ibm.com/ml/neunets) for more information

        - __*Enhanced UI*__: The {{site.data.keyword.aios_short}} UI now includes a runtime histogram distribution with toggle, Model ID & Versioning, and a Transaction ID table from the histogram

        - __*Bias*__: Support for protected attributes of type `float` and `double`, bias detection on linear regression models, and bias remediation

        - __*Explainability*__: Support for regression models, Python functions, and IBM Explainer, along with LIME, algorithms

        - __*Data Store*__: Quality monitoring without reliance on Watson Machine Learning, and Db2 support
--->

### Known issues

- **Microsoft Azure**

    - Of the two types of Azure Machine Learning web services, only the `New` type is supported by {{site.data.keyword.aios_short}}. The `Classic` type is not supported.

    - __*Default input name must be used*__: In the Azure web service, the default input name is `"input1"`. Currently, this field is mandated for {{site.data.keyword.aios_short}} and, if it is missing, Accuracy monitoring will fail.

      If your Azure web service does not use the default name, change the input field name to `"input1"`, then the code will work.

- **AWS SageMaker**

    - __*BlazingText algorithm is not supported name must be used*__: The AWS SageMaker BlazingText algorithm input payload format is not supported in the current release of {{site.data.keyword.aios_short}}.

## 17 September 2018
{: #17September2018}

### New features and changes

- **Beta preview release** - Welcome to the beta preview release of {{site.data.keyword.aios_full_notm}}.
