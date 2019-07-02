---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

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

# Automating payload logging
{: #fmrk-workaround-pyld-lg}

Automatic payload logging exists between {{site.data.keyword.aios_full}} and {{site.data.keyword.pm_full}} when they are provisioned in the same {{site.data.keyword.Bluemix_notm}} account. You can also automate payload logging for other machine learning providers, or for an {{site.data.keyword.pm_full}} instance that is not in the same account, by using one of the following cases and options:
{: shortdesc}

### Case 1: Keep the original format of scoring input and output (different than one required by {{site.data.keyword.aios_short}})
{: #fmrk-workaround-case1}

If your applications use an original payload format that cannot be changed, choose one of the following options:

- Option 1: Custom machine learning engine scoring endpoint should accept both payload formats. 

   Depending on the payload format: {{site.data.keyword.aios_short}} ({{site.data.keyword.pm_full}}-like) or user’s one return the output in corresponding format. If the format is user’s one convert it to {{site.data.keyword.aios_short}} one and store as payload record in payload logging table. If the scoring input format is {{site.data.keyword.aios_short}} one, do not store the payload (this payload is coming from {{site.data.keyword.aios_short}} not from user).

   For more information, see [Using two payload formats](/docs/services/ai-openscale?topic=ai-openscale-integrating-3rd-party-ml-engines-with-watson-openscale#fmrk-workaround-notsuppt).

- Option 2: If for some reasons embedding such logic in a single REST API endpoint is not possible, you can define two endpoints. 

   One is used by your application, however, you must add payload logging and convert it to the expected format. The second endpoint is used by {{site.data.keyword.aios_short}} to make required calculations, such as bias and explainability. No payload logging is required for this enpoint. During {{site.data.keyword.aios_short}} configuration, the second endpoint should be pointed to the one with compatible formats.

   For more information, see [Using two endpoints](/docs/services/ai-openscale?topic=ai-openscale-integrating-3rd-party-ml-engines-with-watson-openscale#fmrk-workaround-opt2-cs1).

- Option 3: Move the payload logging module to the original endpoint or downstream application. 

   If your application supports this option, only one endpoint on the custom machine learning engine needs to be developed: the one for {{site.data.keyword.aios_short}}.

### Case 2: Work with the format of payload required by {{site.data.keyword.aios_short}}
{: #fmrk-workaround-case2}

In such case there is no need to make any conversion from user’s format (scoring input/output) to the one required by {{site.data.keyword.aios_short}}.

Because we do not want to have the internal scoring requests logged as user payload (calculations done by {{site.data.keyword.aios_short}}), either you must develop two endpoints or you must code extra logic for a single endpoint.

- Option 1: Two endpoints. It is almost the same as option 2 in Case 1. The only difference is that there is no need to make any format conversions since those are already aligned.

- Option 2: Single endpoint. There is a need to detect if the scoring request is coming from user’s application. That can be achieved by sending some extra information in scoring payload (aka metadata). If such metadata is detected the payload should be logged.

## Using two payload formats
{: #fmrk-workaround-notsuppt}

Let’s say that I am using XYZ offering to serve my models. XYZ is not supported by {{site.data.keyword.aios_short}} at this stage.

I have many downstream applications consuming my deployments on XYZ and I cannot change the format of scoring payload. However; I can modify the scoring endpoint logic.

### Steps

1. Develop a custom machine learning engine that wraps XYZ deployment.
2. Implement the scoring endpoint on the custom machine learning engine to support the payload formats for both XYZ and {{site.data.keyword.aios_short}}.
3. Add the logic in the scoring endpoint on your custom machine learning engine to detect the format of the payload.
4. If the payload is coming from downstream apps, convert it to the {{site.data.keyword.aios_short}} format and log it as payload records in {{site.data.keyword.aios_short}}.
5. Switch downstream apps scoring endpoints to the new one you created.

If the URL of the scoring endpoint needs to remain the same, use URL re-direction, which is also known as a proxy.

## Using two endpoints
{: #fmrk-workaround-opt2-cs1}

If the format of your payload cannot be changed, for example, if it would cause your downstream applications to break, you must use separate endpoints. This approach consists of the following components:

- scoring endpoint (in the user’s format) with the original scoring endpoint using user-defined format for both input and output
- custom ml engine with perturbation endpoint ({{site.data.keyword.aios_short}} format) and discovery endpoint. Perturbation endpoint wraps original scoring endpoint plus makes conversions from {{site.data.keyword.aios_short}} format to user’s one and from user’s output to {{site.data.keyword.aios_short}} one. This is required for {{site.data.keyword.aios_short}} to make correct scoring request and understand the output.
- scoring endpoint wrapper with payload logging capability. This wrapper is consumed by downstream application instead of original scoring endpoint. Its logic has been extended with payload logging capability. Each time scoring request is executed the input and output are being converted to {{site.data.keyword.aios_short}} format and logged.

The following flowchart shows the custom machine learning engine solution in which the custom machine learning engine handles the perturbation and discovery endpoints and translates it to your format:

![REST API endpoints specification](images/woscustommlworkflow.png)

### Steps
{: #fmrk-workaround-smple-cd}

1. Use a notebook to create a scoring endpoint for the credit risk model (scikit-learn) deployment on the Microsoft Azure Machine Learning Service. For more information, see [this sample notebook](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/azure/Credit%20model%20with%20Azure%20ML%20Service%20and%20scikit-learn.ipynb).
2. Create a custom machine learning engine and deploy it on Microsoft Azure Cloud as a Flask application. Create the perturbation and discovery endpoints. For more information, see [these deployment instructions](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-azure).
3. Configure {{site.data.keyword.aios_short}} to work with the custom machine learning engine. For more information, see  [this sample notebook](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/azure/OpenScale%20and%20Custom%20ML%20Engine%20configuration.ipynb).
4. Create a scoring endpoint wrapper that automates payload logging on the Microsoft Azure Machine Learning Service. For more information, see [this sample notebook](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/azure/Credit%20scoring%20endpoint%20wrapper%20with%20payload%20logging.ipynb).

Pay special attention to the following items:

- Credentials: To make the tutorial easier to follow, the {{site.data.keyword.aios_short}} credentials are hard-coded within the code (scoring endpoint wrapper). You must update these values to your actual credentials.
- Python SDK vs. REST API: The tutorial uses the Python SDK to log the payload. You could also use the REST API to do this, however you must generate or refresh the token on your own. 
- {{site.data.keyword.cloud_notm}} vs. Cloud Pak for Data: If you are using {{site.data.keyword.wos4d_notm}}, the credentials are in a different format [here is the sample notebook](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine%20-%20ICP.ipynb). The {{site.data.keyword.aios_short}} client class is also different. It uses the `APIClient4ICP` client class.
- Payload logging as separate endpoint/package — extraction of payload logging & conversion methods to separate package or endpoint. In that way it could be re-used if you would like to inject batch of payloads outside scoring endpoint wrapper.

