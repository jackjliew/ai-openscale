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

# {{site.data.keyword.aios_short}} for {{site.data.keyword.cloud_notm}} 的已知问题和限制
{: #rn-12ki}

以下列表包含对于 {{site.data.keyword.aios_full}} for {{site.data.keyword.Bluemix}} 和 {{site.data.keyword.wos4d_full}} 常见以及特定于 {{site.data.keyword.aios_full}} for {{site.data.keyword.Bluemix}} 的已知问题和限制。
{: shortdesc}

<p>&nbsp;</p>

## 共同问题
{: #wos-common-issues}

以下限制和已知问题对于 {{site.data.keyword.aios_full}} on {{site.data.keyword.Bluemix}} 和 {{site.data.keyword.wos4d_full}} 均为常见。

<p>&nbsp;</p>


### 常见限制
{: #wos-limitations}

- 对于 {{site.data.keyword.pm_full}}，为有效内容日志记录发送的图像分类模型的评分输入不能超过 ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling serviceMB。要避免超时问题，图像不得超过 125 x 125 像素，并且必须顺序发送，以便在完成第一个图像后请求对第二个图像的解释。


- 对于不使用空格或标点符号分隔单词的连续脚本语言（例如日语、中文和朝鲜语），不支持非结构化文本模型的可解释性。



<p>&nbsp;</p>


### 漂移配置错误阻止配置漂移监视器
{: #wos-common-issues-mismatchdatatype}

当您希望配置监视器（例如漂移检测监视器）时，模型配置屏幕的灵活性后来也可能导致问题。由于您可以选择数据类型，因此必须确保选项反映模型的原始状况。如果未正确选择预测列类型，那么可能会发生以下错误：

```
"error": AIQDS2003E",
"message": "The model predictions '[0. 1.]' are different from class names in training data '['No' 'Yes']' for the subscription <<number>> in datamart <<datamart ID>> and service binding <<binding ID>>.
```

以下情况是最可能的原因：

- `class` 标签为字符串类型，而 `modeling_role` **预测**以双精度值类型分配到**预测**列，因为这是输出数据模型的定义方式。
- 在 UI 中选择双精度值类型的**预测**列，这不受限制。


### 有效内容格式
{: #wos-common-issues-payloadformat}

为适当处理有效内容分析，{{site.data.keyword.aios_short}} 不支持在有效内容中使用带有双引号 (") 的列名。这将影响 CSV 和 JSON 格式的评分有效内容和反馈数据。

<p>&nbsp;</p>



### Microsoft Azure ML Studio
{: #wos-common-issues-msazure}

- 在两种类型的 Azure Machine Learning Web Service 中，{{site.data.keyword.aios_short}} 仅支持 `New` 类型。不支持 `Classic` 类型。

- __*必须使用缺省输入名称*__：在 Azure Web Service 中，缺省输入名称为 `"input1"`。当前，{{site.data.keyword.aios_short}} 必需此字段，如果缺失，那么 {{site.data.keyword.aios_short}} 将无法正常运作。

  如果 Azure Web Service 不使用缺省名称，请将输入字段名称更改为 `"input1"`，然后代码将正常运作。

- 如果调用 Microsoft Azure ML Studio 以列出机器学习模型导致响应超时（例如，在具有许多 Web Service 时），那么必须增大超时值。例如，如果使用的是 HAProxy 负载均衡器，那么可能需要通过发出以下命令来解决此问题：

   - 登录到负载均衡器节点并更新 `/etc/haproxy/haproxy.cfg`，以将客户机和服务器超时从 `1m` 设置为 `5m`：

       ```bash
          timeout client           5m
          timeout server           5m
          ```

   - 运行 `systemctl restart haproxy` 以重新启动 HAProxy 负载均衡器。

如果使用的是除 HAProxy 以外的其他负载均衡器，那么可能需要以类似方式调整超时值。
      
      {: note}

- 在两种类型的 Azure Machine Learning Web Service 中，{{site.data.keyword.aios_short}} 仅支持 `New` 类型。不支持 `Classic` 类型。

- 在 Azure Web Service 中，缺省输入名称为 `"input1"`。当前，此字段是 {{site.data.keyword.aios_short}} 的必填字段，如果缺失，那么“准确性”监视将失败。

   如果 Azure Web Service 不使用缺省名称，请将输入字段名称更改为 `"input1"`。

<p>&nbsp;</p>


### Amazon SageMaker
{: #wos-common-issues-aws}

- __*不支持 BlazingText 算法*__：Amazon SageMaker BlazingText 算法输入有效内容格式在 {{site.data.keyword.aios_short}} 的当前发行版中不受支持。

<p>&nbsp;</p>


### 定制机器学习服务实例
{: #wos-common-issues-custom}

- [Python 模块](/docs/services/ai-openscale?topic=ai-openscale-as-module)当前不具有适用于定制服务实例的可解释性。这是因为定制服务实例需要在响应数据中进行数字预测，而模块脚本未随附该数据。

<p>&nbsp;</p>


- **代码片段无效**

    - 为监视器配置提供的 cURL 和 Python 代码片段均无效。以下提供了正确的代码片段：

      *有效内容日志记录*

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

      *反馈日志记录*

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

    - 为除偏端点提供的 Java 代码片段无效。以下提供了正确的代码片段：

      *除偏端点*

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


### 浏览器支持
{: #abt-browser}

{{site.data.keyword.aios_short}} 服务工具需要的浏览器软件级别与 {{site.data.keyword.cloud_notm}} 所需的相同。请参阅 {{site.data.keyword.cloud_notm}} [先决条件](/docs/overview?topic=overview-prereqs-platform#browsers)主题以获取详细信息。

<p>&nbsp;</p>


### Python 客户机
{: #abt-python}

[{{site.data.keyword.aios_short}} Python 客户机](http://ai-openscale-python-client.mybluemix.net/){: external}是一个 Python 库，允许您直接使用 {{site.data.keyword.aios_short}} 服务。您可以使用 Python 客户机而不是 {{site.data.keyword.aios_short}} 客户机 UI 来直接配置数据集市数据库，绑定机器学习引擎以及选择并监视部署。有关以此方式使用 Python 客户机的示例，请参阅 [{{site.data.keyword.aios_short}} 样本笔记本](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks)。


## 特定于 {{site.data.keyword.aios_short}} 的问题
{: #cloud-issues}

以下限制和问题特定于 {{site.data.keyword.aios_short}} for {{site.data.keyword.Bluemix}}。

<p>&nbsp;</p>

### 限制

{: #cloud-limitations}

- 当前发行版仅支持一个数据库、一个 {{site.data.keyword.pm_full}} 实例和一个 {{site.data.keyword.aios_short}} 实例。 

- 数据库和 {{site.data.keyword.pm_full}} 实例必须部署在同一 {{site.data.keyword.cloud_notm}} 帐户中。

- {{site.data.keyword.aios_short}} 使用 PostgreSQL 或 Db2 数据库来存储模型相关数据（反馈数据或评分有效内容）和计算的度量。当前不支持 Lite Db2 套餐。

- 免费 Lite 套餐数据库不符合 GDPR。如果模型处理个人可标识信息 (PII)，那么必须购买新数据库或使用符合 GDPR 规则的现有数据库。



<p>&nbsp;</p>
## 后续步骤
{: #abt-next}

- [入门](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted)
- 查看 [API 参考资料](https://{DomainName}/apidocs/ai-openscale){: external}。
- [{{site.data.keyword.aios_short}} 中的新增内容](/docs/services/ai-openscale?topic=ai-openscale-rn-relnotes)
- [联系 IBM](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: external}。
