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

# {{site.data.keyword.aios_short}} の既知の問題と制約
{: #rn-12ki}

以下のリストには、{{site.data.keyword.aios_full}} の既知の問題および制約が記載されています。
{: shortdesc}

<p>&nbsp;</p>

## 制限
{: #wos-limitations}

- {{site.data.keyword.aios_short}} は、Python SDK を使用して、追加のエンジンを構成する場合に、複数の機械学習エンジンをサポートします。

- 現行リリースでサポートされているのは、1 つのデータベース、1 つの {{site.data.keyword.pm_full}} インスタンス、1 つの {{site.data.keyword.aios_short}} インスタンスのみです

- データベースと {{site.data.keyword.pm_full}} インスタンスは、同じ {{site.data.keyword.cloud_notm}} アカウントにデプロイする必要があります。

- Lite (無料) プランには、以下の月次制限があります。

    - モニター対象は 2 つのデプロイ済みモデル
    - 説明対象は 20 個のトランザクション
    - 50,000 件のペイロード・レコード (累積)
    - 50,000 件のフィードバック・レコード (累積)

- {{site.data.keyword.aios_short}} は PostgreSQL データベースまたは Db2 データベースを使用して、モデル関連データ (フィードバック・データ、評価ペイロード) や計算された指標を保管します。 Db2 の Lite プランは現在サポートされていません。

- {{site.data.keyword.aios_short}} のインスタンスあたり、デプロイ済みモデルは 1 ライセンスについて 20 個に制限されています。

- {{site.data.keyword.pm_full}} では、ペイロード・ロギングのために送信する画像分類モデルの評価入力データは、1 MB を超えてはなりません。タイムアウトの問題を避けるには、イメージは 125 x 125 ピクセルを超えてはならず、最初のものが完了してから 2 番目のイメージの説明が要求されるように、順次送信される必要があります。

- 無料のライト・プラン・データベースは GDPR に準拠していません。 モデルで個人情報 (PII) を処理する場合は、GDPR の規則に準拠している新しいデータベースを購入するか、GDPR の規則に準拠している既存のデータベースを使用しなければなりません。 

- 非構造化テキストのモデルの説明性は、空白文字や句読文字で単語を区切らない連続記述言語 (日本語、中国語、韓国語など) ではサポートされていません。



<p>&nbsp;</p>

## 共通の問題
{: #wos-common-issues}

以下の問題は、{{site.data.keyword.Bluemix}} 上の {{site.data.keyword.aios_full}} と {{site.data.keyword.wos4d_full}} の両方に共通の問題です。

<p>&nbsp;</p>

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


## {{site.data.keyword.wos4d_notm}} の既知の問題
{: #rn-16April2019ki}

以下の問題は、{{site.data.keyword.wos4d_full}} に固有のものです。

<p>&nbsp;</p>


### IBM SPSS Collaboration and Deployment Services (C&DS)
{: #rn-16April2019ki-icp-spss}

- **説明性のサポートの制限**

   - バイナリー・モデル、およびすべてのクラスの確率を返す SPSS マルチクラス・モデルでは、説明性がサポートされます。 
   - 最高のクラス確率のみを返す SPSS マルチクラス・モデルでは、説明性はサポートされません。


<p>&nbsp;</p>


- **IBM SPSS Collaboration and Deployment Services (C&DS) でデプロイメント ID に下線 (_) 文字を含めることができない**

    - サブスクリプションの `deployment_id` から下線 (_) 文字を削除してください。

<p>&nbsp;</p>




- **IBM SPSS Collaboration and Deployment Services (C&DS) (バイナリー形式のみ) では、追加のペイロード・リクエストを行う必要がある**

    - IBM SPSS Collaboration & Deployment Services のバイナリー・サブスクリプションの場合、[デプロイメント用のモニターの準備](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mo-config#mo-config)後かすべてのモニターの構成後に、別の[ペイロード・ロギング (評価) 要求](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-cdb-connect#cdb-scoring)を行わなければなりません。 そうすることにより、[説明性](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-ie-ov#ie-ov)の正確さが確保されます。

<p>&nbsp;</p>


- **IBM SPSS C&DS (バイナリー形式のみ) の訂正されたレコードのカウントが誤っていることがある**

    - IBM SPSS Collaboration & Deployment Services のバイナリー・サブスクリプションの場合、**「トランザクションの表示」**ボタンを使用して表示する際に、*「訂正されたレコード」* のカウントが正確でないことがあります。

<p>&nbsp;</p>

### 指標
{: #rn-16April2019ki-icp-metrics}

- **{{site.data.keyword.pm_full}} のパフォーマンスの指標が収集されない**

    - Cloud Pak for Data 環境では、{{site.data.keyword.pm_full}} のパフォーマンス指標は収集されません。

<p>&nbsp;</p>

- **説明性のサポートの制限**

    - モデルのビルド時に、評価に関する入力要求からのターゲット (ラベル) 列を組み込まないでください。 モデルで入力要求にターゲット列を組み込む必要がある場合は、バイアス検査、バイアス緩和、および説明性は機能しません。


<p>&nbsp;</p>


### Python 関数
{: #rn-16April2019ki-icp-python}

- **Python 関数がサポートされていない**

    - 現行リリースでは、Python 関数に対するバイアス検査、バイアス緩和、説明性はサポートされていません。

<p>&nbsp;</p>


### インストールおよび構成
{: #rn-16April2019ki-icp-install}


- **アンインストール・スクリプトで Kafka トピックが削除されない**

    - アンインストール・スクリプトを実行しても、インストール時に EventStream に作成された {{site.data.keyword.aios_short}} Kafka トピックが削除されません。

<p>&nbsp;</p>

### データベース
{: #rn-16April2019ki-icp-dbs}

- **Db2 Warehouse 使用時の行サイズの制限**

    - Db2 Warehouse には 1 MB の行サイズ制限があります。 複数 (30 より多い) のテキスト列 (VARCHAR ごとに 32000 バイト) があると、この制限を超過します。 この制限は Amazon SageMaker の使用時に最も目立ちます。SageMaker のネイティブ形式ではすべての列がストリング形式だからです。

       {{site.data.keyword.aios_short}} は、データベース・オブジェクトの作成にデフォルトの表スペースを使用するため、実際の制限はご使用のデータベース構成によって異なります。 この制限に関する追加情報については、[IBM Knowledge Center の Db2 の資料](https://www.ibm.com/support/knowledgecenter/SSEPGG_11.1.0/com.ibm.db2.luw.sql.ref.doc/doc/r0001029.html)を参照してください。





## ブラウザーのサポート
{: #abt-browser}

{{site.data.keyword.aios_short}} サービス・ツールでは、{{site.data.keyword.cloud_notm}} で必要とされるレベルと同じレベルのブラウザー・ソフトウェアが必要です。 詳しくは、{{site.data.keyword.cloud_notm}} の[前提条件](/docs/overview?topic=overview-prereqs-platform#browsers)トピックを参照してください。

<p>&nbsp;</p>


## Python クライアント
{: #abt-python}

[{{site.data.keyword.aios_short}} Python クライアント](http://ai-openscale-python-client.mybluemix.net/){: external}は、{{site.data.keyword.aios_short}} サービスを直接扱うことができる Python ライブラリーです。 {{site.data.keyword.aios_short}} クライアント UI の代わりに Python クライアントを使用すると、データマート・データベースの直接的な構成、機械学習エンジンのバインド、デプロイメントの選択とモニターが可能になります。 例えば、このように Python クライアントを使用する場合には、[{{site.data.keyword.aios_short}} サンプル・ノートブック](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks)を参照してください。

<p>&nbsp;</p>
## 次のステップ
{: #abt-next}

- サービスを[開始](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-gs-get-started)します。
- [API リファレンス資料](https://{DomainName}/apidocs/ai-openscale){: external}を参照します。

まだご不明な点がありますか? 

- [新機能](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-rn-relnotes)
- [IBM にお問い合わせください](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: external}。
