---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: Amazon SageMaker, machine learning, services, AWS

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

# Specifying an Amazon SageMaker ML service instance
{: #csm-connect}

Your first step in the {{site.data.keyword.aios_short}} tool is to specify an Amazon SageMaker service instance. Your Amazon SageMaker service instance is where you store your AI models and deployments.
{: shortdesc}

You can also add your machine learning provider by using the Python SDK. For more information on performing this programmatically, see [Bind your Amazon SageMaker machine learning engine](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind).

## Connect your Amazon SageMaker service instance
{: #csm-config}

{{site.data.keyword.aios_short}} connects to AI models and deployments in an Amazon SageMaker service instance.

1.  From the **Configure** tab, click **Machine learning provider**.

    ![the select your machine learning service provider screen is shown with tiles for the supported machine learning engines](images/wos-machine-learning-providers-selection.png)

1.  Click the **Amazon SageMaker** tile.

    ![Enter Amazon SageMaker service credentials](images/connect-sage-cred.png)

1.  Enter and save your credentials:

    - Access Key ID: Your AWS access key ID, `aws_access_key_id`, which verifies who you are and authenticates and authorizes calls that you make to AWS.
    - Secret Access Key: Your AWS secret access key, `aws_secret_access_key`, which is required to verify who you are and to authenticate and authorize calls that you make to AWS.
    - Region: Enter the region where your Access Key ID was created. Keys are stored and used in the region in which they were created and cannot be transferred to another region. 

1.  {{site.data.keyword.aios_short}} lists your deployed models; select the ones you want to monitor.

### Next steps
{: #csm-next}

{{site.data.keyword.aios_short}} is now ready for you to [configure monitors](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
