---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: machine learning engines, frameworks, Microsoft Azure, Amazone SageMaker, custom ML engine 

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

# Integrating 3rd-party ML engines with {{site.data.keyword.aios_short}}
{: #fmrk-workaround}

{{site.data.keyword.aios_full}} integrates with external machine learning service engines, such as Microsoft Azure ML Studio and Amazon SageMaker.
{: shortdesc}

You can integrate {{site.data.keyword.aios_short}} with 3rd-party engines in the following ways:

- Engine binding level:

  Ability to list deployments and get deployment details.

- Deployment subscription level:

   {{site.data.keyword.aios_short}} needs to be able to score subscribed deployment in the required format, such as the {{site.data.keyword.pm_full}} format and receive the output in the same compatible format. {{site.data.keyword.aios_short}} must be configured to process both input and output formats.

- Payload logging:

   Each input and output to the deployed model triggered by a user’s application must be stored in a payload store. The format of the payload records follows the same specification as mentioned in the preceding section on deployment subscription levels. 

   {{site.data.keyword.aios_short}} uses those records to calculate bias, explanations and others. It is not possible for {{site.data.keyword.aios_short}} to automatically store transactions that are executed on the user site, which is outside the {{site.data.keyword.aios_short}} system. This is one of the ways that {{site.data.keyword.aios_short}} safeguards proprietary information. Use the {{site.data.keyword.aios_short}} Rest API or Python SDK to work with secure data.

## What is a custom machine learning engine?
{: #fmrk-workaround}

A custom machine learning engine provides the infrastructure and hosting capabilities for machine learning models and web applications. Custom machine learning engines that are supported by {{site.data.keyword.aios_short}} must conform to the following requirements:

- Expose two types of REST API endpoints:

   * discovery endpoint (GET list of deployments and details)
   * scoring endpoints (online and real-time scoring)

- All endpoints need to be compatible with the  swagger specification to be supported.

- Input payload and output to or from the deployment must be compliant with the JSON file format that is described in the specification.

At this stage only the `BasicAuth` or `none` formats are supported.
{: Note}

The following example shows the REST API endpoints specification:

![The REST API endpoints specification is displayed from the swagger document](images/wosdeployments.png)


The following example shows the format for an input payload:

![Input payload example is shown](images/wosinputdata.png)


## When is a custom machine learning engine the best choice for me?
{: #fmrk-workaround-choice}

A custom machine learning engine is the best choice when the following situations are true:

- You are not using any available out of the box products to serve your machine learning models. You have just developed your own system to do that. There is no and will be no direct support in {{site.data.keyword.aios_short}} for that.
- The serving engine you are using from a 3rd-party supplier is not supported by {{site.data.keyword.aios_short}} yet. In this case, consider developing a custom machine learning engine as a wrapper to your original or native deployments.

## Payload logging — what is it?
{: #fmrk-workaround-payload-logging-explained}

As mentioned in the preceding section, all transactions going to the deployed models must be logged as payload records in the {{site.data.keyword.aios_short}} data mart. The input and output payloads (requests and responses) need to be in the format required by {{site.data.keyword.aios_short}} as described in the REST API specification. To log the payload you must use the API.

### Logging the payload with Python SDK and REST API

For an example of full working code, see the [AI Openscale and Custom ML Engine](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb) sample notebook.

The following code sample shows how to log the payload by using the Python SDK:

```
records_list = [
   PayloadRecord(request=request_data, 
                 response=response_data,
                 response_time=response_time), 
   PayloadRecord(request=request_data,
                 response=response_data,
                 response_time=response_time)]
subscription.payload_logging.store(records=records_list)
```

The following code sample shows how to log the payload by using the REST API:

```
PAYLOAD_STORING_HREF_PATTERN ='{}/v1/data_marts/{}/scoring_payloads'
endpoint = PAYLOAD_STORING_HREF_PATTERN.format(
                                AIOS_CREDENTIALS['url'], 
                                AIOS_CREDENTIALS['data_mart_id'])
deployment_uid = subscription.get_details()['entity']['deployments'][0]['deployment_id']
payload = [{'binding_id': binding_uid, 
            'deployment_id': deployment_uid,
            'subscription_id': subscription.uid,
            'scoring_id': scoring_uid,
            'response': response_data,
            'request': request_data}]
headers = {'Authorization': 'Bearer '+ token}
req_response = requests.post(endpoint, 
                             json=payload,
                             headers = headers)
```

You can preview the content of your payload logging table either by directly connecting to the database or by using the Python SDK, which is shown in the following sample output. 

![Python SDK sample output of payload logging table](images/wosntbok.png)


## Automating payload logging
{: #fmrk-workaround-pyld-lg}

You can automate payload logging by using one of the following cases and options:

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

- scoring endpoint (user’s format) original scoring endpoint using user defined format of input and output
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

## Custom machine learning engine examples
{: #fmrk-workaround-cstmmlsengex}

Use the following examples to set up your own custom machine learning engine.

### Python and flask
{: #fmrk-workaround-pandflask}

The [Custom ML Engine example published on git](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix) is using python and flask to serve scikit-learn model.

The [README file](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix) describes how the app can be deployed locally for testing purposes as well as cf application on IBM Cloud. The implementation of REST API endpoints can be found in [app.py file](https://github.com/pmservice/ai-openscale-tutorials/blob/master/applications/custom-ml-engine-bluemix/app.py).

### Node.js
{: #fmrk-workaround-nodejs}

You can also find example of custom machine learning engine written in [Node.js here](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-nodejs).

### End2end code pattern
{: #fmrk-workaround-e2ecode}

[Code pattern](https://developer.ibm.com/patterns/monitor-custom-machine-learning-engine-with-ai-openscale) showing end2end example of custom engine deployment and integration with {{site.data.keyword.aios_short}}.

