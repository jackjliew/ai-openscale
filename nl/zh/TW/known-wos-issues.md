---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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

# {{site.data.keyword.aios_short}} 的已知問題和限制
{: #rn-12ki}

下列清單含有 {{site.data.keyword.aios_full}} 的已知問題和限制。
{: shortdesc}

<p>&nbsp;</p>

## 限制
{: #wos-limitations}

- {{site.data.keyword.aios_short}} 支援多個機器學習引擎，但前提是您要利用 Python SDK 來配置其他的引擎。

- 現行版本只支援一個資料庫、一個 {{site.data.keyword.pm_full}} 實例，以及一個 {{site.data.keyword.aios_short}} 實例

- 資料庫和 {{site.data.keyword.pm_full}} 實例必須部署在相同的 {{site.data.keyword.cloud_notm}} 帳戶中。

- Lite（免費）方案具有下列的每月限制：

    - 兩個受監視的所部署模型
    - 可解釋 20 項交易
    - 50,000 筆有效負載記錄（累加）
    - 50,000 筆回饋記錄（累加）

- {{site.data.keyword.aios_short}} 使用 PostgreSQL 或 Db2 資料庫，來儲存模型相關資料（回饋資料、評分有效負載）和計算後的度量。目前不支援「精簡 Db2」方案。

- 根據授權限制，每一個 {{site.data.keyword.aios_short}} 實例只能有 20 個所部署模型。

- 對於 {{site.data.keyword.pm_full}}，要傳送進行有效負載記載之影像分類模型的評分輸入，不能超過 1 MB。若要避免發生逾時問題，影像不得超過 125 x 125 像素，且必須循序傳送，如此才會在第一個影像完成時，要求取得第二個影像的解釋。

- 免費 Lite 方案資料庫不符合 GDPR 規章。如果您的模型會處理個人識別資訊 (PII)，您必須購買新的資料庫，或是使用符合 GDPR 規則的現有資料庫。 

- 若為日文、中文和韓文等之類的連續書寫型語言（亦即，不使用空格或標點符號字元來區隔單字），則不支援非結構化文字模型的可解釋性。



<p>&nbsp;</p>

## 常見問題
{: #wos-common-issues}

以下是位於 {{site.data.keyword.Bluemix}} 和 {{site.data.keyword.wos4d_full}} 上之 {{site.data.keyword.aios_full}} 的常見問題。

<p>&nbsp;</p>

### 有效負載格式
{: #wos-common-issues-payloadformat}

為了適當處理有效負載分析，{{site.data.keyword.aios_short}} 不支援帶有雙引號 (") 的直欄名稱出現在有效負載中。這會同時影響 CSV 和 JSON 格式的評分有效負載和回饋資料。

<p>&nbsp;</p>



### Microsoft Azure ML Studio
{: #wos-common-issues-msazure}

- Azure Machine Learning Web 服務有兩種類型，但 {{site.data.keyword.aios_short}} 只支援`新`類型。不支援`標準`類型。

- __*必須使用預設輸入名稱*__：在 Azure Web 服務中，預設輸入名稱是 `"input1"`。目前 {{site.data.keyword.aios_short}} 規定要使用此欄位，如果遺漏，{{site.data.keyword.aios_short}} 就無法運作。

  如果您的 Azure Web 服務不是使用預設名稱，請將輸入欄位名稱變更為 `"input1"`，這樣程式碼就會運作。

- 如果呼叫 Microsoft Azure ML Studio 以列出機器學習模型期間，會導致回應逾時，例如，您的 Web 服務太多，您必須增加逾時值。例如，如果您使用 HAProxy 負載平衡器，則需要發出下列指令，以暫行解決此問題：

   - 登入負載平衡器節點，並且更新 `/etc/haproxy/haproxy.cfg`，以便將用戶端與伺服器逾時值從 `1m` 設為 `5m`：

       ```bash
          timeout client           5m
          timeout server           5m
          ```

   - 執行 `systemctl restart haproxy`，重新啟動 HAProxy 負載平衡器。

如果您使用的是 HAProxy 以外的其他負載平衡器，可能需要採類似方式來調整逾時值。
      {: note}

- Azure Machine Learning Web 服務有兩種類型，但 {{site.data.keyword.aios_short}} 只支援`新`類型。不支援`標準`類型。

- 在 Azure Web 服務中，預設輸入名稱是 `"input1"`。目前 {{site.data.keyword.aios_short}} 規定要使用此欄位，如果遺漏，「精確度」監視就會失敗。

   如果您的 Azure Web 服務不是使用預設名稱，請將輸入欄位名稱變更為 `"input1"`。

<p>&nbsp;</p>


### Amazon SageMaker
{: #wos-common-issues-aws}

- __*不支援 BlazingText 演算法*__：在 {{site.data.keyword.aios_short}} 現行版本中，不支援 Amazon SageMaker BlazingText 演算法輸入有效負載格式。

<p>&nbsp;</p>


### 自訂機器學習服務實例
{: #wos-common-issues-custom}

- [Python 模組](/docs/services/ai-openscale?topic=ai-openscale-as-module)目前無法將「可解釋性」運用於「自訂」服務實例上。這是因為「自訂」服務實例要求回應資料中需有一項數值預測，但這並未隨附於模組 Script 中。

<p>&nbsp;</p>


- **程式碼 Snippet 無效**

    - 提供給監視器配置的 cURL 和 Python 程式碼 Snippet 都無效。這裡提供正確的程式碼 Snippet：

      *有效負載記載*

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

      *回饋記載*

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

    - 提供來為端點除去偏誤的 Java 程式碼 Snippet 無效。這裡提供正確的程式碼 Snippet：

      *為端點除去偏誤*

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


## {{site.data.keyword.wos4d_notm}} 的已知問題
{: #rn-16April2019ki}

以下是 {{site.data.keyword.wos4d_full}} 的特定問題。

<p>&nbsp;</p>


### IBM SPSS Collaboration and Deployment Services (C&DS)
{: #rn-16April2019ki-icp-spss}

- **「可解釋性」支援受限**

   - 二進位模型以及會傳回所有類別之機率的 SPSS 多類別模型支援可解釋性。 
   - 只會傳回勝出類別機率的 SPSS 多類別模型不支援可解釋性。


<p>&nbsp;</p>


- **在 IBM SPSS Collaboration and Deployment Services (C&DS) 中，部署 ID 不能包含底線 (_) 字元**

    - 將底線 (_) 字元從訂閱的 `deployment_id` 移除。

<p>&nbsp;</p>




- **IBM SPSS Collaboration and Deployment Services (C&DS)（僅適用於二進位類型）要求需發出額外的有效負載要求**

    - 對於 IBM SPSS Collaboration & Deployment Services 二進位訂閱，您必須在[準備部署的監視器](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mo-config#mo-config)之後，或在配置所有監視器之後，發出另一項 [有效負載記載（評分）要求](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-cdb-connect#cdb-scoring)。這可確保[可解釋性](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-ie-ov#ie-ov)是精確的。

<p>&nbsp;</p>


- **IBM SPSS C&DS（僅適用於二進位類型）更正後的記錄計數可能是錯的**

    - 對於 IBM SPSS Collaboration & Deployment Services 二進位訂閱，當使用**檢視交易**按鈕來檢視時，*更正後的記錄*計數不見得是精確的。

<p>&nbsp;</p>

### 度量
{: #rn-16April2019ki-icp-metrics}

- **不會收集 {{site.data.keyword.pm_full}} 效能度量**

    - 在 Cloud Pak for Data 環境中，不會收集來自 {{site.data.keyword.pm_full}} 的效能度量。

<p>&nbsp;</p>

- **「可解釋性」支援限制**

    - 在建置模型時，請勿包含輸入要求中的目標（標籤）直欄，來進行評分。如果模型需要輸入要求中得包含目標直欄，則偏誤檢查、除去偏誤和可解釋性將無法運作。


<p>&nbsp;</p>


### Python 函數
{: #rn-16April2019ki-icp-python}

- **不支援 Python 函數**

    - 在現行版本中，Python 函數不支援偏誤檢查、除去偏誤和可解釋性。

<p>&nbsp;</p>


### 安裝與配置
{: #rn-16April2019ki-icp-install}


- **解除安裝 Script 不會刪除 Kafka 主題**

    - 執行解除安裝 Script 時，並不會移除您在安裝期間建立於 EventStream 中的 {{site.data.keyword.aios_short}} Kafka 主題。

<p>&nbsp;</p>

### 資料庫
{: #rn-16April2019ki-icp-dbs}

- **使用 Db2 Warehouse 時的列大小限制**

    - Db2 Warehouse 的列大小限制是 1 MB。當有多個（超過 30 個）文字直欄時（每一個 VARCHAR 是 32000 個位元組），就會超過限制。當使用 Amazon Sagemaker 時，尤其要特別注意此限制。

       由於 {{site.data.keyword.aios_short}} 使用預設表格空間來建立資料庫物件，實際的限制取決於您的資料庫配置。如需此限制的其他相關資訊，請參閱 [IBM Knowledge Center Db2 說明文件](https://www.ibm.com/support/knowledgecenter/SSEPGG_11.1.0/com.ibm.db2.luw.sql.ref.doc/doc/r0001029.html)。





## 瀏覽器支援
{: #abt-browser}

{{site.data.keyword.aios_short}} 服務工具所需要的瀏覽器軟體層次，與 {{site.data.keyword.cloud_notm}} 所需的相同。如需詳細資料，請參閱 {{site.data.keyword.cloud_notm}} [必要條件](/docs/overview?topic=overview-prereqs-platform#browsers)主題。

<p>&nbsp;</p>


## Python 用戶端
{: #abt-python}

[{{site.data.keyword.aios_short}} Python 用戶端](http://ai-openscale-python-client.mybluemix.net/){: external}是一個 Python 程式庫，可讓您直接使用 {{site.data.keyword.aios_short}} 服務。您可以使用 Python 用戶端而非 {{site.data.keyword.aios_short}} 用戶端使用者介面，以直接配置資料集區資料庫、連結您的機器學習引擎，以及選取及監視部署。如需以此方式使用 Python 用戶端的相關範例，請參閱 [{{site.data.keyword.aios_short}} 樣本記事本](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks)。

<p>&nbsp;</p>
## 後續步驟
{: #abt-next}

- [開始使用](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-gs-get-started)此服務。
- 檢視 [API 參照資料](https://{DomainName}/apidocs/ai-openscale){: external}。

還有其他問題嗎？ 

- [新增功能](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-rn-relnotes)
- [聯絡 IBM](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: external}。
