---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits

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
{:external: target="_blank" .external}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:faq: data-hd-content-type='faq'}

# Known issues and limitations for {{site.data.keyword.aios_short}} for {{site.data.keyword.Bluemix}}
{: #rn-12ki}

The following lists contains the known issues and limitation that are common for {{site.data.keyword.aios_full}} for {{site.data.keyword.Bluemix}} and {{site.data.keyword.wos4d_full}} and also those that are specific to  {{site.data.keyword.aios_full}} for {{site.data.keyword.Bluemix}}.
{: shortdesc}

<p>&nbsp;</p>

## Common issues
{: #wos-common-issues}

The following limitations and known issues are common to both {{site.data.keyword.aios_full}} on {{site.data.keyword.Bluemix}} and {{site.data.keyword.wos4d_full}}.

<p>&nbsp;</p>


### Common limitations
{: #wos-limitations}

- For {{site.data.keyword.pm_full}}, scoring input for image classification models that are sent for payload logging cannot exceed 1 MB. To avoid time out issues, images must not exceed 125 x 125 pixels and must be sent sequentially so that the explanation for the second image is requested when the first one is completed.


- Explainability for unstructured text models is not supported for continuous script languages, such as Japanese, Chinese, and Korean, which don't use whitespace or punctuation characters to separate words.



<p>&nbsp;</p>


### Drift configuration errors prevent configuration of drift monitor
{: #wos-common-issues-mismatchdatatype}

The flexibility of the model configuration screen can also lead to problems later on when you want to configure monitors, such as the drift detection monitor. Because you can choose the data types, you must ensure that your choices reflect what is original to the model. The following error may occur if the prediction column type is not properly selected:

```
"error": AIQDS2003E",
"message": "The model predictions '[0. 1.]' are different from class names in training data '['No' 'Yes']' for the subscription <<number>> in datamart <<datamart ID>> and service binding <<binding ID>>.
```

The following cases are the most-likely cause:

- The `class` label is of string type and `modeling_role` **prediction** is assigned to the **prediction** column as a double type because that is how the output data schema is defined.
- You select the **prediction** column of double type in the UI, which is not restricted.


### Payload formats
{: #wos-common-issues-payloadformat}

For proper processing of payload analytics, {{site.data.keyword.aios_short}} does not support column names with double quotation marks (") in the payload. This affects both scoring payload and feedback data in CSV and JSON formats.

<p>&nbsp;</p>



### Microsoft Azure ML Studio
{: #wos-common-issues-msazure}

- Of the two types of Azure Machine Learning web services, only the `New` type is supported by {{site.data.keyword.aios_short}}. The `Classic` type is not supported.

- __*Default input name must be used*__: In the Azure web service, the default input name is `"input1"`. Currently, this field is mandated for {{site.data.keyword.aios_short}} and, if it is missing, {{site.data.keyword.aios_short}} will not work.

  If your Azure web service does not use the default name, change the input field name to `"input1"`, then the code will work.

- If calls to Microsoft Azure ML Studio to list the machine learning models causes the response to time out, for example when you have many web services, you must increase timeout values. For example, if you are using the HAProxy load balancer, you may need to work around this issue by issuing the following commands:

   - Logging into the load balancer node and updating `/etc/haproxy/haproxy.cfg` to set the client and server timeout from `1m` to `5m`:

       ```bash
       timeout client           5m
       timeout server           5m
      ```

   - Running `systemctl restart haproxy` to restart the HAProxy load balancer.

If you are using a different load balancer, other than HAProxy, you may need to adjust timeout values in a similar fashion.
      {: note}

- Of the two types of Azure Machine Learning web services, only the `New` type is supported by {{site.data.keyword.aios_short}}. The `Classic` type is not supported.

- In the Azure web service, the default input name is `"input1"`. Currently, this field is mandated for {{site.data.keyword.aios_short}} and, if it is missing, Accuracy monitoring fails.

   If your Azure web service does not use the default name, change the input field name to `"input1"`.

<p>&nbsp;</p>


### Amazon SageMaker
{: #wos-common-issues-aws}

- __*BlazingText algorithm is not supported*__: The Amazon SageMaker BlazingText algorithm input payload format is not supported in the current release of {{site.data.keyword.aios_short}}.

<p>&nbsp;</p>


### Custom machine learning service instance
{: #wos-common-issues-custom}

- The [Python module](/docs/services/ai-openscale?topic=ai-openscale-as-module) does not currently have Explainability working for the Custom service instance. This is because the Custom service instance requires a numerical prediction in the response data, which is not included with the module script.

<p>&nbsp;</p>


- **Code snippets invalid**

    - Both cURL and Python code snippets provided for monitor configuration are invalid. Correct code snippets are provided here:

      *Payload logging*

      ```cURL
      # Generate an ICP access token by passing an ICP username as $USERNAME, and ICP password as $PASSWORD in the following request

      curl -k -X GET \
      -user "$USERNAME:$PASSWORD" \
      "https://{{icp_hostname}:{{icp_port}}/v1/preauth/validateAuth"

      # the previous CURL request will return an auth token under "accessToken", that you will use as {icp_token} in the following payload logging request 
      # TODO: manually define and pass:
      # request - input to scoring endpoint in supported by {{site.data.keyword.aios_short}} format - replace sample fields and values with proper ones
      # response - output from scored model in supported by {{site.data.keyword.aios_short}} format - replace sample fields and values with proper ones
      # - $SCORING_ID - ID of the scoring transaction
      # - $SCORING_TIME - Time (ms) taken to make prediction (for performance monitoring)

      SCORING_PAYLOAD='[{
        "scoring_id": "$SCORING_ID",
        "response_time": "$SCORING_TIME",
        "request": {
          "fields": ["AGE", "SEX", "BP", "CHOLESTEROL", "NA", "K"],
          "values": [[28, "F", "LOW", "HIGH", 0.61, 0.026]]
      },
      "response": {
        "fields": ["AGE", "SEX", "BP", "CHOLESTEROL", "NA", "K", "probability", "prediction", "DRUG"],
        "values": [[28, "F", "LOW", "HIGH", 0.61, 0.026, [0.82, 0.07, 0.0, 0.05, 0.03], 0.0, "drugY"]]
        },
        "binding_id": "{{binding_id}}",
        "subscription_id": "{{subscription_id}}",
        "deployment_id": "{{deployment_id}}"
      }]'

      curl -k -X POST https://{{icp_hostname}:{{icp_port}}/v1/data_marts/{{data_mart_id}}/scoring_payloads -d "$SCORING_PAYLOAD" \
      --header 'Content-Type: application/json' --header 'Accept: application/json' --header "Authorization: Bearer $ICP_TOKEN"
      ```

      *Feedback logging*

      ```cURL
      # Generate an ICP access token by passing an ICP username as $USERNAME, and ICP password as $PASSWORD in the following request

      curl -k -X GET \
      --user "$USERNAME:$PASSWORD" \
      "https://{{icp_hostname}:{{icp_port}}/v1/preauth/validateAuth"

      # the previous CURL request will return an auth token under "accessToken" key that you will use as {icp_token} in the following payload logging request
      # TODO: manually define and pass:
      # fields - list of fields names - replace sample values with proper ones
      # values - feedback data records - replace sample values with proper ones
      # - $SCORING_ID - ID of the scoring transaction
      # - $SCORING_TIME - Time (ms) taken to make prediction (for performance monitoring)

      FEEDBACK_DATA='{
        "fields": ["AGE", "SEX", "BP", "CHOLESTEROL", "NA", "K", "DRUG"],
        "values": [[28, "F", "LOW", "HIGH", 0.61, 0.026, "drugB"]],
        "binding_id": "{{binding_id}}",
        "subscription_id": "{{subscription_id}}"
      }'

      curl -k -X POST https://{{icp_hostname}:{{icp_port}}/v1/data_marts/{{data_mart_id}}/feedback_payloads -d "$FEEDBACK_DATA" \
      --header 'Content-Type: application/json' --header 'Accept: application/json' --header "Authorization: Bearer $ICP_TOKEN"
      ```

    - Java code snippet provided for debiasing endpoint is invalid. Correct code snippet is provided here:

      *Debias endpoint*

      ```java
      /**
      At runtime you need to replace values for the following

      <HOSTNAME> - Host Name eg: aiopenscale.test.cloud.ibm.com
      <PORT> - Server Port
      <DATA_MART_ID> - DataMart id
      <SERVICE_BINDING_ID> - Service Binding id
      <ASSET_ID> - Asset id or the model id
      <DEPLOYMENT_ID> - Deployment id
      <TOKEN> - Bearer token

      */
      import org.apache.http.HttpVersion;
      import org.apache.http.client.fluent.Request;
      import org.apache.http.entity.ContentType;

      String bearerToken = "Bearer <TOKEN>";
      String URL = "https://<HOSTNAME>:<PORT>/v1/data_marts/<DATA_MART_ID>/service_bindings/<SERVICE_BINDING_ID>/subscriptions/<ASSET_ID>/deployments/<DEPLOYMENT_ID>/online";

      String payload = "{ \"fields\": [ \"field1\", \"field2\", \"field3\" ], \"values\": [ [ \"field1Value1\", \"field2Value1\", \"field3Value1\" ], [ \"field1Value2\", \"field2Value2\", \"field3Value2\" ]] }";

      byte[] res = Request.Post(URL).addHeader("Authorization", bearerToken).useExpectContinue().version(HttpVersion.HTTP_1_1)
                .bodyString(payload, ContentType.APPLICATION_JSON).execute().returnContent().asBytes();
      ```

<p>&nbsp;</p>


### Browser support
{: #abt-browser}

The {{site.data.keyword.aios_short}} service tooling requires the same level of browser software as is required by {{site.data.keyword.cloud_notm}}. See the {{site.data.keyword.cloud_notm}} [Prerequisites](/docs/overview?topic=overview-prereqs-platform#browsers) topic for details.

<p>&nbsp;</p>


### Python client
{: #abt-python}

The [{{site.data.keyword.aios_short}} Python client](http://ai-openscale-python-client.mybluemix.net/){: external} is a Python library that allows you to work directly with the {{site.data.keyword.aios_short}} service. You can use the Python client, instead of the {{site.data.keyword.aios_short}} client UI, to directly configure the datamart database, bind your machine learning engine, and select and monitor deployments. For examples using the Python client in this way, see the [{{site.data.keyword.aios_short}} sample notebooks](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks).


## Issues specific to {{site.data.keyword.aios_short}}
{: #cloud-issues}

The following limitation and issues are specific to {{site.data.keyword.aios_short}} for {{site.data.keyword.Bluemix}}.

<p>&nbsp;</p>

### Limitations
{: #cloud-limitations}

- The current release only supports one database, one {{site.data.keyword.pm_full}} instance, and one instance of {{site.data.keyword.aios_short}}. 

- The database and {{site.data.keyword.pm_full}} instance must be deployed in the same {{site.data.keyword.cloud_notm}} account.

- {{site.data.keyword.aios_short}} uses a PostgreSQL or Db2 database to store model related data (feedback data, scoring payload) and calculated metrics. Lite Db2 plans are not currently supported.

- The free Lite plan database is not GDPR compliant. If your model processes personally identifiable information (PII), you must purchase a new database or use an existing database that does conform to GDPR rules.



<p>&nbsp;</p>
## Next steps
{: #abt-next}

- [Getting started](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted)
- View the [API Reference material](https://{DomainName}/apidocs/ai-openscale){: external}.
- [What's new in {{site.data.keyword.aios_short}}](/docs/services/ai-openscale?topic=ai-openscale-rn-relnotes)
- [Contact IBM](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: external}.
