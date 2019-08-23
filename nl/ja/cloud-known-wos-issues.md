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

# {{site.data.keyword.aios_short}} for {{site.data.keyword.cloud_notm}} の既知の問題と制約
{: #rn-12ki}

以下のリストには、{{site.data.keyword.aios_full}} for {{site.data.keyword.Bluemix}} と {{site.data.keyword.wos4d_full}} に共通する既知の問題と制約、および {{site.data.keyword.aios_full}} for {{site.data.keyword.Bluemix}} に固有の既知の問題と制約が記載されています。
{: shortdesc}

<p>&nbsp;</p>

## 共通の問題
{: #wos-common-issues}

以下の制約と既知の問題は、{{site.data.keyword.Bluemix}} 上の {{site.data.keyword.aios_full}} と {{site.data.keyword.wos4d_full}} に共通の問題です。

<p>&nbsp;</p>


### 共通の制約
{: #wos-limitations}

- {{site.data.keyword.pm_full}} では、ペイロード・ロギングのために送信する画像分類モデルの評価入力データは、(ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling service) MB を超えてはなりません。タイムアウトの問題を避けるには、イメージは 125 x 125 ピクセルを超えてはならず、最初のものが完了してから 2 番目のイメージの説明が要求されるように、順次送信される必要があります。


- 非構造化テキストのモデルの説明性は、空白文字や句読文字で単語を区切らない連続記述言語 (日本語、中国語、韓国語など) ではサポートされていません。



<p>&nbsp;</p>


### ドリフト構成エラーのためにドリフト・モニターを構成できない
{: #wos-common-issues-mismatchdatatype}

モデル構成画面の柔軟性は、後でドリフト検出モニターなどのモニターを構成する際の問題につながることもあります。 データ・タイプを選択できるので、選択したものがモデルのオリジナルのものを反映していることを確認する必要があります。 予測列のタイプを適切に選択していないと、次のエラーが発生する場合があります。

```
"error": AIQDS2003E",
"message": "The model predictions '[0. 1.]' are different from class names in training data '['No' 'Yes']' for the subscription <<number>> in datamart <<datamart ID>> and service binding <<binding ID>>.
```

最も可能性の高い原因は、以下のようなケースです。

- 出力データ・スキーマの定義に沿って、`class` ラベルが string タイプであり、**prediction** 列に `modeling_role` **prediction**が double タイプとして割り当てられている。
- 制限されていない double タイプの**prediction** 列を UI で選択した。


### ペイロードのフォーマット
{: #wos-common-issues-payloadformat}

ペイロード分析の正常な処理のために、{{site.data.keyword.aios_short}} は、二重引用符 (") を含む列名のペイロードをサポートしていません。これは、CSV 形式および JSON 形式の評価ペイロードとフィードバック・データにも該当します。

<p>&nbsp;</p>



### Microsoft Azure ML Studio
{: #wos-common-issues-msazure}

- 2 種類の Azure Machine Learning Web サービスのうち、{{site.data.keyword.aios_short}} では `New` タイプのみがサポートされています。 `Classic` タイプはサポートされていません。

- __*デフォルトの入力名を使用する必要があります*__: Azure Web サービスではデフォルトの入力名は `input1` です。 現時点ではこのフィールドは {{site.data.keyword.aios_short}} で必須であり、欠落している場合は {{site.data.keyword.aios_short}} が機能しません。

  Azure Web サービスでデフォルト名を使用していない場合は、入力フィールド名を`「input1」`に変更してください。これでコードが機能するようになります。

- Microsoft Azure ML Studio に対して機械学習モデルをリストする呼び出しをし、応答がタイムアウトする場合 (数多くの Web サービスがある場合など) は、タイムアウト値を増やす必要があります。 例えば、HAProxy ロード・バランサーを使用している場合、以下のコマンドを実行して、この問題を回避する必要が生じることがあります。

   - ロード・バランサー・ノードにログインし、`/etc/haproxy/haproxy.cfg` を更新して、以下のようにクライアントとサーバーのタイムアウトの設定を `1m` から `5m` に設定します。

       ```bash
       timeout client           5m
       timeout server           5m
      ```

   - `systemctl restart haproxy` を実行して、HAProxy ロード・バランサーを再始動します。

HAProxy 以外のロード・バランサーを使用している場合も、同様の方法でタイムアウト値を調整する必要が生じることがあります。
      {: note}

- 2 種類の Azure Machine Learning Web サービスのうち、{{site.data.keyword.aios_short}} では `New` タイプのみがサポートされています。 `Classic` タイプはサポートされていません。

- Azure Web サービスでは、デフォルトの入力名は `"input1"` です。 現時点ではこのフィールドは {{site.data.keyword.aios_short}} で必須であり、欠落している場合は正解率のモニターが失敗します。

   Azure Web サービスでデフォルト名を使用していない場合は、入力フィールド名を `"input1"` に変更してください。

<p>&nbsp;</p>


### Amazon SageMaker
{: #wos-common-issues-aws}

- __*BlazingText アルゴリズムはサポートされていません*__: Amazon SageMaker BlazingText アルゴリズム入力ペイロード・フォーマットは、{{site.data.keyword.aios_short}} の現行リリースではサポートされていません。

<p>&nbsp;</p>


### カスタム機械学習サービス・インスタンス
{: #wos-common-issues-custom}

- 現行の [Python モジュール](/docs/services/ai-openscale?topic=ai-openscale-as-module)では、カスタム・サービス・インスタンスに対して説明性が機能しません。 これは、カスタム・サービス・インスタンスでは応答データに数値による予測が必要ですが、このモジュール・スクリプトにはそれが含まれていないためです。

<p>&nbsp;</p>


- **コード・スニペットが無効**

    - モニター構成用に提供されている cURL と Python のコード・スニペットは両方とも無効です。 以下に正しいコード・スニペットを示します。

      *ペイロード・ロギング*

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

      *フィードバック・ロギング*

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

    - バイアス緩和エンドポイント用に提供されている Java コード・スニペットは無効です。 以下に、正しいコード・スニペットを示します。

      *バイアス緩和エンドポイント*

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


### ブラウザーのサポート
{: #abt-browser}

{{site.data.keyword.aios_short}} サービス・ツールでは、{{site.data.keyword.cloud_notm}} で必要とされるレベルと同じレベルのブラウザー・ソフトウェアが必要です。 詳しくは、{{site.data.keyword.cloud_notm}} の[前提条件](/docs/overview?topic=overview-prereqs-platform#browsers)トピックを参照してください。

<p>&nbsp;</p>


### Python クライアント
{: #abt-python}

[{{site.data.keyword.aios_short}} Python クライアント](http://ai-openscale-python-client.mybluemix.net/){: external}は、{{site.data.keyword.aios_short}} サービスを直接扱うことができる Python ライブラリーです。 {{site.data.keyword.aios_short}} クライアント UI の代わりに Python クライアントを使用すると、データマート・データベースの直接的な構成、機械学習エンジンのバインド、デプロイメントの選択とモニターが可能になります。 例えば、このように Python クライアントを使用する場合には、[{{site.data.keyword.aios_short}} サンプル・ノートブック](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks)を参照してください。


## {{site.data.keyword.aios_short}} に固有の問題
{: #cloud-issues}

以下の制約と問題は、{{site.data.keyword.aios_short}} for {{site.data.keyword.Bluemix}} に固有のものです。

<p>&nbsp;</p>

### 制限
{: #cloud-limitations}

- 現行リリースでサポートされるのは、1 つのデータベース、1 つの {{site.data.keyword.pm_full}} インスタンス、および 1 つの {{site.data.keyword.aios_short}} インスタンスのみです。 

- データベースと {{site.data.keyword.pm_full}} インスタンスは、同じ {{site.data.keyword.cloud_notm}} アカウントにデプロイする必要があります。

- {{site.data.keyword.aios_short}} は PostgreSQL データベースまたは Db2 データベースを使用して、モデル関連データ (フィードバック・データ、評価ペイロード) や計算された指標を保管します。 Db2 の Lite プランは現在サポートされていません。

- 無料のライト・プラン・データベースは GDPR に準拠していません。 モデルで個人情報 (PII) を処理する場合は、GDPR の規則に準拠している新しいデータベースを購入するか、GDPR の規則に準拠している既存のデータベースを使用しなければなりません。



<p>&nbsp;</p>
## 次のステップ
{: #abt-next}

- [入門](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted)
- [API リファレンス資料](https://{DomainName}/apidocs/ai-openscale){: external}を参照します。
- [{{site.data.keyword.aios_short}}](/docs/services/ai-openscale?topic=ai-openscale-rn-relnotes) の新機能
- [IBM にお問い合わせください](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: external}。
