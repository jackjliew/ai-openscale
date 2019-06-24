---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

keywords: machine learning engines, frameworks, Microsoft Azure, Amazone SageMaker, custom ML engine 

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

# Custom machine learning engine
{: #fmrk-workaround-customengine}

A custom machine learning engine provides the infrastructure and hosting capabilities for machine learning models and web applications. Custom machine learning engines that are supported by {{site.data.keyword.aios_short}} must conform to the following requirements:

- Expose two types of REST API endpoints:

   * discovery endpoint (GET list of deployments and details)
   * scoring endpoints (online and real-time scoring)

- All endpoints need to be compatible with the swagger specification to be supported.

- Input payload and output to or from the deployment must be compliant with the JSON file format that is described in the specification.

At this stage only the `BasicAuth` or `none` formats are supported.
{: Note}

The following example shows the REST API endpoints specification:

![The REST API endpoints specification is displayed from the swagger document](images/wosdeployments.png)


The following example shows the format for an input payload:

![Input payload example is shown](images/wosinputdata.png)


## When is a custom machine learning engine the best choice for me?
{: #fmrk-workaround-enging-choice}

A custom machine learning engine is the best choice when the following situations are true:

- You are not using any available out-of-the-box products to serve your machine learning models. You have just developed your own system to do that. There is no, and will be no, direct support in {{site.data.keyword.aios_short}} for that.
- The serving engine you are using from a 3rd-party supplier is not supported by {{site.data.keyword.aios_short}} yet. In this case, consider developing a custom machine learning engine as a wrapper to your original or native deployments.

## Next steps
{: #fmrk-workaround-nxt-steps-over}

Implement your own solution by using one of these [Custom machine learning examples](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-cstmmlsengex).