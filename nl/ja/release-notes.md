---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-16"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# リリース情報
{: #rn-relnotes}

この文書では、{{site.data.keyword.aios_full_notm}} に関する新しいフィーチャーと既知の問題について略述します。
{: shortdesc}

## 2019 年 4 月 16 日
{: #rn-16April2019}

以下の新しいフィーチャーとサービスに対する変更が使用可能になります。

### 新しいフィーチャーと変更
{: #rn-16April2019nf}

前回のリリース以降に追加または拡張された {{site.data.keyword.aios_short}} フィーチャーには、以下のものが含まれます。

- __*UI の更新*__: サブスクリプションの作成時に、JSON ファイルをインポートして、すべてのモニターとフィーチャーをプログラマチックに構成できます。構成ファイルをエクスポートすることもできます。詳細については、[JSON ファイルを使用したデプロイメント・サブスクリプションの構成](/docs/services/ai-openscale?topic=ai-openscale-cf-ov)のトピックを参照してください。

- __*新しい信用リスク・モデル*__: すべてのスコアリング・エンジンに関する新しい信用リスク・モデルの例/チュートリアルがサポートされています。詳細については、[入門](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-gs-get-started#gs-get-started)と[追加リソース](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-arsc-ov#arsc-ov)のトピックを参照してください。

- __*バイアス除去の計算*__: 実動モデルと {{site.data.keyword.aios_short}} で作成されたバイアス除去モデルの間で切り替えることができます。詳細については、[実動モデルとバイアス除去モデル](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart#itc-prdb)と[バイアス除去機能の理解](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mf-monitor#mf-debias)を参照してください。

- __*UI ベースの「ファスト・パス」デモ*__: 初めて {{site.data.keyword.aios_short}} UI にログインする際に、デモ・シナリオを実行して、{{site.data.keyword.aios_short}} がモデルをモニターする方法を即時に参照するオプションが備えられました。引き続き技術ユーザーは、{{site.data.keyword.aios_short}} やその他のサービスの構成を自動化したりサンプル・データを提供したりする Python モジュールのインストールを代わりに選択できます。詳細については、[入門](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-gs-get-started#gs-get-started)のトピックを参照してください。

### 既知の問題
{: #rn-16April2019ki}

- **Db2 使用時の行サイズの制限**

    - Db2 には 1 MB の行サイズ制限があります。複数 (30 より多い) のテキスト列 (VARCHAR ごとに 32000 バイト) があると、この制限を超過します。この制限は AWS SageMaker の使用時に最も目立ちます。SageMaker のネイティブ形式ではすべての列がストリング形式だからです。この問題を回避するには、列を適切な形式に変換します。

       {{site.data.keyword.aios_short}} は常にデフォルトのテーブル・スペースを使用してデータベース・オブジェクトを作成するので、実際の制限はデータベース構成に依存する可能性があることに注意してください。この制限に関する追加情報については、[IBM Knowledge Center の Db2 の資料](https://www.ibm.com/support/knowledgecenter/SSEPGG_11.1.0/com.ibm.db2.luw.sql.ref.doc/doc/r0001029.html)を参照してください。

- **IBM SPSS C&DS (バイナリー形式のみ) では、追加のペイロード要求を行う必要がある**

    - IBM SPSS Collaboration & Deployment Services のバイナリー・サブスクリプションの場合、[デプロイメント用のモニターの準備](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mo-config#mo-config)後かすべてのモニターの構成後に、別の[ペイロード・ロギング (スコアリング) 要求](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-cdb-connect#cdb-scoring)を行わなければなりません。そうすることにより、[説明可能性](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-ie-ov#ie-ov)の正確さが保証されます。

- **IBM SPSS C&DS (バイナリー形式のみ) の訂正されたレコードのカウントが誤っていることがある**

    - IBM SPSS Collaboration & Deployment Services のバイナリー・サブスクリプションの場合、**「トランザクションの表示 (View Transactions)」**ボタンを使用して表示する際に、*「訂正されたレコード (Corrected Records)」*のカウントが正しくないことがあります。

- **WML のパフォーマンス・メトリックが収集されない**

    - {{site.data.keyword.icpfull_notm}} 環境で、Watson Machine Learning (WML) からのパフォーマンス・メトリックは収集されません。

## 2019 年 2 月 12 日
{: #rn-12February2019}

以下の新しいフィーチャーとサービスに対する変更が使用可能になります。

### 新しいフィーチャーと変更
{: #rn-12February2019nf}

前回のリリース以降に追加または拡張された {{site.data.keyword.aios_short}} フィーチャーには、以下のものが含まれます。

- __*UI の更新*__: {{site.data.keyword.aios_short}} ユーザー・インターフェースに複数の改善が加えられました。その中には、[オンデマンドで公平性と正確度を確認する](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdep)ボタンや、[公平性の詳細グラフ](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra)からトランザクションのリストを表示する機能が含まれます。

- __*説明可能性の機能強化*__: 陽性 (PP) 値と陰性 (PN) 値において、すべての数値の精度/位取りが同じになりました。

- __*IBM SPSS Collaboration & Deployment Services のサポート*__: IBM SPSS C&DS が、サポートされている機械学習サービス・インスタンスの 1 つになりました。[IBM SPSS Collaboration & Deployment Services インスタンスの指定](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-cspss-spss)を参照してください。

- __*Db2 SSL のサポート*__: {{site.data.keyword.aios_short}} は、Db2 の資格情報を使用した自己署名証明書 (Base 64 エンコード) の引き渡しをサポートしています。

### 既知の問題
{: #rn-12February2019ki}

- **Python 関数がサポートされていない**

    - 現行リリースでは、Python 関数に対するバイアス検査、バイアス除去、説明可能性はサポートされていません。

- **説明可能性のサポートの制限**

    - モデルのビルド時に、スコアリングに関する入力要求からのターゲット (ラベル) 列を組み込まないでください。モデルで入力要求にターゲット列を組み込む必要がある場合は、バイアス検査、バイアス除去、説明可能性は作動しません。

    - Watson Machine Learning (WML) 上でイメージ・ベースのモデルをデプロイできないので、説明可能性サービスではイメージ・ベースのモデルをサポートしていません。これは WML の制限です。

- **カスタム ML サービス・インスタンス**

    - [Python モジュール](/docs/services/ai-openscale?topic=ai-openscale-as-module)では、カスタム・サービス・インスタンスに関する説明可能性は現在作動しません。その理由は、説明を生成するには、カスタム・サービス・インスタンスでは応答データ内に数値の予測がある必要がありますが、モジュール・スクリプトを使用して数値を組み込むことができないからです。カスタム・アプリケーションのソースのモデルがスコアリング応答内で数値以外の予測を戻す場合、カスタム・サービス・インスタンスに対する説明可能性はサポートされません。

- **Microsoft Azure**

    - 一部のクラスターでは、大量の Web サービスがある場合に、Azure 用の Web サービス・メタデータの入手に関する問題があります。この問題が発生すると、Azure からのデプロイメント応答が空のように見えます。

      この原因は、このメタデータの入手に要する時間がタイムアウト値を超えていることにあります。例えば、HAProxy ロード・バランサーを使用している場合、以下のようにして、この問題を回避する必要が生じることがあります。

        - ロード・バランサー・ノードにログインし、`/etc/haproxy/haproxy.cfg` を更新して、以下のようにクライアントとタイムアウトのタイムアウトの設定を `1m` から `5m` に変更します。

          ```bash
          timeout client           5m
          timeout server           5m
          ```

        - `systemctl restart haproxy` を実行して、HAProxy ロード・バランサーを再始動します。

      HAProxy 以外のロード・バランサーを使用している場合も、同様の方法でタイムアウト値を調整する必要が生じることがあります。
      {: note}

## 2018 年 12 月 14 日
{: #rn-14December2018}

以下の新しいフィーチャーとサービスに対する変更が使用可能になります。

### 新しいフィーチャーと変更
{: #rn-14December2018nf}

- **GA のリリース**

    - {{site.data.keyword.aios_full_notm}} の一般出荷版 (GA) がリリースされました。このリリースには、以下のフィーチャーが含まれています。

        - __*リリース*__: {{site.data.keyword.aios_short}} は IBM Cloud Standard (有料) プランとして入手したり、IBM Cloud Private for Data V1.2 上で入手したりできます

          IBM Neural Network Synthesizer (NeuNetS) もベータ版として入手可能です (パブリック・クラウドのみ)。詳細については、[NeuNetS の資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://dataplatform.cloud.ibm.com/ml/neunets) を参照してください。

        - __*拡張された UI*__: {{site.data.keyword.aios_short}} UI に実行時ヒストグラム分布が組み込まれるようになり、ヒストグラムからのモデル ID とバージョン管理の切り替え、およびトランザクション ID テーブルもあります。

        - __*バイアス*__: `float` と `double` のタイプの保護属性、線形回帰モデルでのバイアス検出、バイアスの修復のサポート

        - __*説明可能性*__: 回帰モデル、Python 関数、LIME (Local Interpretable Model-Agnostic Explanations) やアルゴリズムと連動する IBM Explainer のサポート

        - __*データ・ストア*__: Watson Machine Learning に依存しない品質モニタリングと、Db2 サポート

### 既知の問題
{: #rn-14December2018ki}

- **Microsoft Azure**

    - {{site.data.keyword.aios_short}} では、2 つある Azure Machine Learning Web サービスのタイプのうちの 1 つである `New` タイプのみサポートされています。`Classic` タイプはサポートされていません。

    - Azure Web サービスでは、デフォルトの入力名は `"input1"` です。現在このフィールドは {{site.data.keyword.aios_short}} 用に定められており、欠落していると正確度のモニターが失敗します。

      Azure Web サービスでデフォルトの名前が使用されない場合は、入力フィールドの名前を `"input1"` に変更すると、コードが機能します。

- **AWS SageMaker**

    - {{site.data.keyword.aios_short}} 内で `binding_id` に関連付けられた AWS SageMaker エンジン内に無効な AWS SageMaker モデルが存在する場合、サービスが `NullPointerException` を戻すことがあります。

      この問題は、デプロイメントを選択する際に無効なモデルが含まれるモデル・デプロイメントのリストを試行する場合や、無効なモデルが存在している際に Python API クライアントからモデル・デプロイメントのリストを試行する場合に発生することもあります。

    - AWS SageMaker BlazingText アルゴリズムの入力ペイロードの形式は、{{site.data.keyword.aios_short}} の現行リリースではサポートされていません。

- **コード・スニペットが無効**

    - モニター構成用に提供されている cURL と Python のコード・スニペットは両方とも無効です。以下に正しいコード・スニペットを示します。

      *ペイロード・ロギング*

      ```cURL
      # Generate an ICP access token by passing an ICP username as $USERNAME, and ICP password as $PASSWORD in the request below

      curl -k -X GET \
      -user "$USERNAME:$PASSWORD" \
      "https://{{icp_hostname}:{{icp_port}}/v1/preauth/validateAuth"

      # the above CURL request will return an auth token under "accessToken", that you will use as {icp_token} in the payload logging request below
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
      # Generate an ICP access token by passing an ICP username as $USERNAME, and ICP password as $PASSWORD in the request below

      curl -k -X GET \
      --user "$USERNAME:$PASSWORD" \
      "https://{{icp_hostname}:{{icp_port}}/v1/preauth/validateAuth"

      # the above CURL request will return an auth token under "accessToken" key that you will use as {icp_token} in the payload logging request below
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

    - バイアス除去エンドポイント用に提供されている Java コード・スニペットは無効です。以下に、正しいコード・スニペットを示します。

      *バイアス除去エンドポイント*

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

## 2018 年 9 月 17 日
{: #rn-17September2018}

### 新しいフィーチャーと変更
{: #rn-17September2018nf}

- **ベータ・プレビューのリリース** - {{site.data.keyword.aios_full_notm}} のベータ・プレビューがリリースされました。
