---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: release notes, what's new 

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

# What's new
{: #rn-relnotes}

This document outlines new features for {{site.data.keyword.aios_full_notm}}.
{: shortdesc}

## 25 April 2019
{: #rn-25April2019}

The following new features and changes to the service are available.

In addition to usability improvements and security updates, our developers have been busy with new features. {{site.data.keyword.aios_short}} features that have been added or enhanced over the preceding several weeks include:

- __*Automated setup tour*__: A new tour-led way to set up your {{site.data.keyword.aios_short}} environment. Use the [Automated setup](/docs/services/ai-openscale?topic=ai-openscale-wos-fast-start) to provision services and download and configure a model. You will notice this option when you have a new instance of {{site.data.keyword.aios_short}}.
- __*Switch to beta*__: ![beta tag](images/beta.png) A new toggle, **Explore the new beta version**, enables you to work in our beta environment, where you can check out all the latest features and new functionality. Don't like what you see? Just switch back by clicking **Go back to the original version**. Your configuration and monitors are unaffected. The following capabilities are part of the current beta program:
    - __*Confusion matrix*__: A [confusion matrix displays](/docs/services/ai-openscale?topic=ai-openscale-it-conf-mtx#it-conf-mtx) the false positives and false negatives. Click a cell to view the subset of feedback records.

## 5 March 2019
{: #rn-5March2019}

The following new features and changes to the service are available.

{{site.data.keyword.aios_short}} features that have been added or enhanced since the previous release include:

- __*New Credit Risk model*__: A new Credit Risk model example/tutorial is supported for all scoring engines. For more information see the [Getting started](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted#gettingstarted) and [Additional resources](/docs/services/ai-openscale?topic=ai-openscale-arsc-ov#arsc-ov) topics.

- __*Computing debias*__: You can toggle between your production model and a de-biased model created by {{site.data.keyword.aios_short}}. See [Production model and De-biased model](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-prdb) and [Understanding how de-biasing works](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor#mf-debias) for more information.

## 22 February 2019
{: #rn-22February2019}

The following new features and changes to the service are available.

{{site.data.keyword.aios_short}} features that have been added or enhanced since the previous release include:

- __*UI updates*__: You can import a JSON file to programmatically configure all monitors and features during subscription creation. You can also export the configuration file. See the [Configure deployment subscription using JSON files](/docs/services/ai-openscale?topic=ai-openscale-cf-ov) topic for more information.

## 7 February 2019
{: #rn-7February2019}

The following new features and changes to the service are available.

{{site.data.keyword.aios_short}} features that have been added or enhanced since the previous release include:

- __*UI updates*__: Several improvements have been made to the {{site.data.keyword.aios_short}} user interface, including a way to [check fairness and accuracy on demand](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdep), and the ability to see a list of transactions from the [fairness details chart](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra).

- __*Explainability enhancements*__: All numbers now have the same precision/scale across Pertinent Positive (PP) and Pertinent Negative (PN) values.

- __*Db2 SSL support*__: {{site.data.keyword.aios_short}} supports passing self-signed certificates (Base-64 encoded) with DB2 credentials.

- __*IBM Cloud Database support*__: {{site.data.keyword.aios_short}} now supports Databases for PostgreSQL, in addition to Compose for PostgreSQL and Db2)

## 14 December 2018
{: #rn-14December2018}

The following new features, changes, and known issues with the service are available.

{{site.data.keyword.aios_short}} features that have been added or enhanced since the beta release include:

- __*General availability*__: The General Availability (GA) release of {{site.data.keyword.aios_full_notm}} as an IBM Cloud Standard (paid) plan.

- __*IBM Cloud Private for Data V1.2*__: If you are using {{site.data.keyword.aios_short}} on IBM Cloud Private for Data V1.2, see the documentation, including installation instructions, here: [Installation checklist](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-inst-install-icp#install)

- __*Support for your model type*__: In addition to AI model deployments in Watson Machine Learning, {{site.data.keyword.aios_short}} supports model deployments in Microsoft Azure, Amazon SageMaker, and Custom environments. See [Supported model types](/docs/services/ai-openscale?topic=ai-openscale-in-ov) for more information.

- __*Free "lite" database*__: A free "lite" managed database provides everything you need to begin using {{site.data.keyword.aios_short}}. See the [{{site.data.keyword.aios_short}} pricing plans ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/catalog/services/watson-openscale){: new_window} for details.

- __*Bias monitoring*__: Support for protected attributes of type `float` and `double`, and bias detection on linear regression models. And {{site.data.keyword.aios_short}} can automatically de-bias your AI model for you. See [Understanding fairness](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor) for more information.

- __*Explainability*__: Support for regression models, Python functions, and complementary contrastive explanations. See [Monitoring explainability](/docs/services/ai-openscale?topic=ai-openscale-ie-ov) for more information.

- __*Data Store*__: Quality monitoring without reliance on Watson Machine Learning, and the ability to use your own database, whether it's Db2, Postgres or Db2 on Cloud.

- __*Enhanced UI*__: The {{site.data.keyword.aios_short}} UI has been improved to include a runtime histogram distribution with toggle for training data, Model ID & Versioning, and a Transaction ID table from the histogram. See [Visualizing data for a specific hour](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet) for more information.

- __*Alternate tutorial set-up option*__: To automate the provisioning and configuration of the required IBM Cloud services, and to see an IBM {{site.data.keyword.aios_full}} application, including sample data, you can install and run a Python module. See [Installing a Python module to set up {{site.data.keyword.aios_short}}](/docs/services/ai-openscale?topic=ai-openscale-as-module)

## 17 September 2018
{: #rn-17September2018}

- **Beta preview release** - Welcome to the beta preview release of {{site.data.keyword.aios_full_notm}}.

<p>&nbsp;</p>

## Next steps
{: #relnotes-in-next}

Still have questions? 

- [Limitations](/docs/services/ai-openscale?topic=ai-openscale-in-ov#in-lim)
- [Known issues](/docs/services/ai-openscale?topic=ai-openscale-in-ov#rn-12ki)
