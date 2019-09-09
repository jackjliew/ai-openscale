---

copyright:
  years: 2018, 2019
lastupdated: "2019-09-09"

keywords: payload, non-Watson, machine learning, services, subscription

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

# Payload logging for non-{{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.pm_short}} service instances
{: #cml-connect}

If your AI model is deployed in a machine learning engine other than {{site.data.keyword.pm_full}}, you must enable payload logging for the external machine learning engine with a Python client.
{: shortdesc}

See more complete information in the [{{site.data.keyword.aios_short}} Python client documentation](http://ai-openscale-python-client.mybluemix.net/){: external}, and in the sample {{site.data.keyword.aios_short}} Python client notebooks that are part of the [{{site.data.keyword.aios_short}} tutorials](https://github.com/pmservice/ai-openscale-tutorials/blob/master/README.md){: external}.

## Before you begin
{: #cml-prereq}

You will need to have the training data of your model available in Db2 or {{site.data.keyword.cos_full}} to monitor bias for your model. Explainability and accuracy is not supported for Python functions. For more information about training data, see [Why does {{site.data.keyword.aios_short}} need access to my training data?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)

- Import and initiate {{site.data.keyword.aios_short}}

    ```python
    from ibm_ai_openscale import APIClient

    aios_credentials = {
      "instance_guid": "***",
      "url": "https://api.aiopenscale.cloud.ibm.com",
      "apikey": "***"
    }

    client = APIClient(service_credentials)
    ```
  Credentials can be found by following the steps shown in the "[Creating credentials](/docs/services/ai-openscale?topic=ai-openscale-cred-create)" topic.

- Create a schema name in your PostgreSQL database

- Set up a datamart

    ```python
    client.data_mart.setup(db_credentials=postgres_credentials, schema=schemaName)

    client.data_mart.get_details()
    ```


## Next steps
{: #cml-next}

- To continue with the {{site.data.keyword.aios_short}} client, see [Configuring the Accuracy or Quality monitor](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor).
- To continue with the Python command library, refer to the [Python client documentation](http://ai-openscale-python-client.mybluemix.net/){: external}.
