---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits, custom machine learning engine, custom

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

# カスタム ML フレームワーク
{: #frmwrks-custom}

カスタム機械学習フレームワークを使用して、ペイロード・ロギングとフィードバック・ロギングを実行し、{{site.data.keyword.aios_full}} でパフォーマンスの正確度、実行時のバイアス検出、説明性、および自動バイアス緩和機能を測定することができます。カスタム機械学習フレームワークには、{{site.data.keywor.pm_full}} との同等性が必要です。

{{site.data.keyword.aios_full}} では、以下のカスタム機械学習フレームワークが完全にサポートされています。
{: shortdesc}

表 1. フレームワークのサポート詳細

| フレームワーク | 問題のタイプ | データ・タイプ |
|:---|:---:|:---:|
| {{site.data.keyword.pm_full}} と同等 | 分類 | 構造化 |
{: caption="フレームワークのサポート詳細" caption-side="top"}

## {{site.data.keyword.aios_short}} へのカスタム機械学習エンジンの追加
{: #frmwrks-custom-add}

次のいずれかの方法を使用して、カスタム機械学習プロバイダーと連携するように {{site.data.keyword.aios_short}} を構成できます。

- 初めてカスタム機械学習プロバイダーを {{site.data.keyword.aios_short}} に追加する場合は、構成インターフェースを使用すると良いでしょう。 詳しくは、[カスタム機械学習インスタンスの指定](/docs/services/ai-openscale?topic=ai-openscale-co-connect)を参照してください。
- Python SDK を使用して、機械学習プロバイダーを追加することもできます。 複数のプロバイダーが必要な場合は、この方法を使用する必要があります。 この操作をプログラムで実行する方法については、[カスタム機械学習エンジンのバインド](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-cusbind)を参照してください。


## サンプル・ノートブック
{: #frmwrks-custom-smpl-ntbks}

- [Kubernetes クラスターを使用したカスタム機械学習エンジンの作成](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix){: external}
- [データマートの作成、モデル・デプロイメントのモニター、およびデータ分析](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}

## 詳細
{: #frmwrks-custom-mediumblogs}

[Watson OpenScale によるカスタム機械学習エンジンのモニター](https://developer.ibm.com/patterns/monitor-custom-machine-learning-engine-with-ai-openscale/){: external}

## カスタム機械学習エンジン
{: #fmrk-workaround-customengine}

カスタム機械学習エンジンは、機械学習モデルと Web アプリケーションのインフラストラクチャーとホスティング機能を提供します。 {{site.data.keyword.aios_short}} によってサポートされるカスタム機械学習エンジンは、以下の要件に準拠している必要があります。

- 次の 2 つのタイプの REST API エンドポイントを公開します。

   * ディスカバリー・エンドポイント (デプロイメントと詳細の GET リスト)
   * 評価エンドポイント (オンラインかつリアルタイムの評価)

- すべてのエンドポイントは、サポートされる swagger の仕様に準拠している必要があります。

- 入力ペイロードと、デプロイメントへの出力およびデプロイメントからの出力は、仕様で説明された JSON ファイル形式に準拠している必要があります。

この段階では、`BasicAuth` フォーマットまたは `none` フォーマットのみがサポートされます。
{: Note}

以下の例は、REST API エンドポイント仕様を示しています。

![swagger ドキュメントから表示される REST API エンドポイント仕様](images/wosdeployments.png)


以下の例は、入力ペイロードのフォーマットを示しています。

![入力ペイロードの例が示されます](images/wosinputdata.png)


## カスタム機械学習エンジンが最善の選択肢になる状況
{: #fmrk-workaround-enging-choice}

カスタム機械学習エンジンは、以下の状況が当てはまるときに最善の選択肢になります。

- 出来合いの製品を使用せずに、機械学習モデルを提供する場合。また、これを行うための独自のシステムを開発したばかりである場合。 {{site.data.keyword.aios_short}} は、これを直接的にサポートせず、将来サポートする予定もありません。
- ご使用のサード・パーティーのサプライヤーからのサービス提供エンジンが、まだ {{site.data.keyword.aios_short}} でサポートされていない場合。 この場合は、元のデプロイメントまたはネイティブ・デプロイメントに対するラッパーとして、カスタム機械学習エンジンを開発することを検討してください。

## カスタム ML サービス・インスタンスの指定
{: #co-connect}

{{site.data.keyword.aios_short}} ツールで最初に実行するステップは、サービス・インスタンスの指定です。 サービス・インスタンスは、AI モデルとデプロイメントの格納場所となります。
{: shortdesc}

## カスタム・サービス・インスタンスの接続
{: #co-config}

{{site.data.keyword.aios_short}} を、サービス・インスタンスの AI モデルとデプロイメントに接続します。 カスタム・サービスを接続できます。

1.  ナビゲーション・ペインの**「構成」**タブで**「機械学習プロバイダー (Machine learning providers)」**をクリックします。

   ![機械学習サービス・プロバイダーの選択画面に、サポートされる機械学習エンジンのタイルが表示されます](images/wos-machine-learning-providers-selection.png)

2. **「機械学習プロバイダーの追加 (Add machine learning provider)」**ボタンをクリックし、**「カスタム環境」**タイルをクリックします。

   ![カスタム機械学習プロバイダー構成画面に、資格情報、インスタンス名、および説明のフィールドが表示されています](images/ml-custom-provider.png)

3. カスタム機械学習プロバイダーの名前と説明を入力して、**「次へ」**をクリックします。 

4. デプロイメントへの接続を、[リストを要求する](/docs/services/ai-openscale?topic=ai-openscale-co-connect#co-config-request-list)ことで行うか、[評価エンドポイントを個々に入力する](/docs/services/ai-openscale?topic=ai-openscale-co-connect#co-config-scoring-endpoints)ことで行うかを選択します。

   ![「デプロイメントへの接続」画面に、オプション (デプロイメントのリストを要求するオプション、または個々の評価エンドポイントを入力するオプション) が表示されています](images/ml-custom-connect-deployments.png)
    
5. **「次へ」**をクリックします。

### デプロイメントのリストの要求
{: #co-config-request-list}

1. **「デプロイメントのリストの要求」**タイルを選択した場合は、資格情報と API エンドポイントを入力してから**「保存」**をクリックします。

   ![デプロイメント・リスト画面に、サービス資格情報と API エンドポイントを入力するフィールドが表示されています](images/connect-custom-cred.png)

2. 機械学習のセットアップを保存した後に、**「ダッシュボード」**に戻り、**「インサイト」**タブをクリックしてから**「ダッシュボードに追加」**ボタンをクリックします。

3. リストからデプロイメントを選択し、**「構成」**をクリックします。

モニターを構成する準備が整いました。

### 個々の評価エンドポイントの指定
{: #co-config-scoring-endpoints}

1. **「個々の評価エンドポイントの入力」**タイルを選択した場合は、API エンドポイントの資格情報を入力してから**「保存」**をクリックします。

2. 機械学習のセットアップを保存した後に、**「ダッシュボード」**に戻り、**「インサイト」**タブをクリックしてから**「ダッシュボードに追加」**ボタンをクリックします。

3. **「エンドポイントの追加 (Add Endpoint)」**ボタンをクリックします。

4. ドロップダウン・メニューで、カスタム環境を選択し、デプロイメント名と API エンドポイントを入力してから、**「保存」**をクリックします。

モニターを構成する準備が整いました。

### 処理の流れ
{: #co-works}

以下の画像は、カスタム環境のサポートを示しています。

![「カスタムの処理の流れ」チャートが表示されています。このチャートには、クライアント API と Watson OpenScale API で構成されるカスタム環境のボックスが表示されています。](images/custom-how-works.png)

以下のリンクも参照できます。

[{{site.data.keyword.aios_short}} ペイロード・ロギング API](https://{DomainName}/apidocs/ai-openscale#publish-scoring-payload){: external}

[カスタム・デプロイメント API](https://aiopenscale-custom-deployement-spec.mybluemix.net/){: external}

[Python クライアント・バインディング SDK](http://ai-openscale-python-client.mybluemix.net/#bindings){: external}

[Working with Custom machine Learning engine](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}

[Python SDK for IBM Watson OpenScale](https://pypi.org/project/ibm-ai-openscale/){: external}

- **モニターをサポートするためのモデルの入力基準**

  モデルでは入力として特徴量ベクトルを取る必要があります。実際にはこのベクトルは、名前付きフィールドとその値のコレクションです (ベクトル内の 1 つのフィールドがバイアスのモニター対象となります)。

  ```bash
  {
    "fields": [
        "name",
        "age",
        "position"
    ],
    "values": [
        [
            "john",
            33,
            "engineer"
        ],
        [
            "mike",
            23,
            "student"
        ]
    ]
  }
  ```

  この例では、`“age”`を公平性を評価するためのフィールドにすることもできます。

  入力がテンソル/行列の場合、つまり入力特徴量スペースから変換される場合 (多くの場合、テキストまたはイメージからのディープ・ラーニングではそのように処理されます)、対象モデルを現行リリースの {{site.data.keyword.aios_short}} プラットフォームで処理することはできません。 そのため、テキスト入力またはイメージ入力を使用するディープ・ラーニング・モデルを、バイアスの検出と緩和のために処理することもできません。

  また、説明性をサポートするため訓練データをロードする必要があります。

  テキストの説明性を確保するには、いずれかの特徴量がフルテキストでなければなりません。 カスタム・モデルのイメージに関する説明性は、現行リリースではサポートされていません。
  {: note}

- **モニターをサポートするためのモデルの出力基準**

  モデルでは、そのモデルの各種クラスの予測の確率とともに、入力特徴量ベクトルを出力する必要があります。

  ```bash
  {
    "fields": [
        "name",
        "age",
        "position",
        "prediction",
        "probability"
    ],
    "labels": [
        "personal",
        "camping"
    ],
    "values": [
        [
            "john",
            33,
            "engineer",
            "personal",
            [
                0.6744664422398081,
                0.3255335577601919
            ]
        ],
        [
            "mike",
            23,
            "student"
            "camping",
            [
                0.2794765664946941,
                0.7205234335053059
            ]
        ]
    ]
  }
  ```

  この例では、`"personal”`と`“camping”`が候補となるクラスで、それぞれの予測出力のスコアが両方のクラスに割り当てられます。 予測の確率がない場合、バイアスの検出は行われますが、自動バイアス修正は行われません。

  前述の予測出力は、{{site.data.keyword.aios_short}} が REST を介して呼び出すことが可能なライブ評価エンドポイントからアクセス可能でなければなりません。 AzureML、SageMaker、{{site.data.keyword.pm_full}} の場合、{{site.data.keyword.aios_short}} はネイティブの評価エンドポイントに直接接続します (そのため、評価の仕様の実装について考える必要はありません)。

## カスタム機械学習エンジンの例
{: #fmrk-workaround-cstmmlsengex}

以下の例を使用して、独自のカスタム機械学習エンジンをセットアップします。
{: shortdesc}

### Python と Flask
{: #fmrk-workaround-pandflask}

[Git で公開されたカスタム ML エンジンの例](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix){: external}では、Python と Flask を使用して、scikit-learn モデルを提供します。

[README ファイル](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix){: external}では、テスト目的でアプリケーションをローカルにデプロイする方法、および IBM Cloud 上の cf アプリケーションについて説明します。 REST API エンドポイントの実装は、[app.py ファイル](https://github.com/pmservice/ai-openscale-tutorials/blob/master/applications/custom-ml-engine-bluemix/app.py){: external}にあります。

### Node.js
{: #fmrk-workaround-nodejs}

[ここで、Node.js](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-nodejs){: external} で作成されたカスタム機械学習エンジンの例を確認することもできます。

### エンドツーエンドのコード・パターン
{: #fmrk-workaround-e2ecode}

[コード・パターン](https://developer.ibm.com/patterns/monitor-custom-machine-learning-engine-with-ai-openscale){: external}で、カスタム・エンジンのデプロイメントおよび {{site.data.keyword.aios_short}} との統合のエンドツーエンドの例を示します。

## カスタム機械学習エンジンのペイロード・ロギング
{: #cml-cusconfig}

### カスタム機械学習エンジンのバインド
{: #cml-cusbind}

- {{site.data.keyword.pm_full}} 以外のエンジンをカスタム、つまり単なるメタデータとしてバインドします。{{site.data.keyword.pm_full}} 以外のサービスとの直接的な統合はありません。 `client.data_mart.bindings.add` メソッドを使用して、複数の機械学習エンジンを {{site.data.keyword.aios_short}} にバインドできます。

    ```python
    custom_engine_credentials = {
    "url": "***",
    "username": "***",
    "password": "***"
    }

    binding_uid = client.data_mart.bindings.add('My custom engine', CustomMachineLearningInstance(custom_engine_credentials))

    bindings_details = client.data_mart.bindings.get_details()
    ```
  次のコマンドを使用してサービス・バインディングを表示できます。

    ```python
    client.data_mart.bindings.list()
    ```

    ![汎用 ML バインディング](images/ml-generic-bind.png)

### カスタム・サブスクリプションの追加
{: #cml-cussub}

- サブスクリプションを追加します

    ```python
    client.data_mart.subscriptions.add(CustomMachineLearningAsset(source_uid='action', binding_uid=binding_uid, prediction_column='predictedActionLabel'))
    ```

- サブスクリプション・リストを取得します

    ```python
    subscriptions = client.data_mart.subscriptions.get_details()

    subscriptions_uids = client.data_mart.subscriptions.get_uids()
    print(subscriptions_uids)
    ```

### ペイロード・ロギングの有効化
{: #cml-cusenlog}

- サブスクリプションでペイロード・ロギングを有効にします

    ```python
    subscription.payload_logging.enable()
    ```

- ロギングの詳細を取得します

    ```python
    subscription.payload_logging.get_details()
    ```

詳しくは、[ペイロード・ロギング](/docs/services/ai-openscale?topic=ai-openscale-cml-connect)を参照してください。

### 評価とペイロード・ロギング
{: #cml-cusscore}

- モデルを評価します。 完全なサンプルについては、[IBM {{site.data.keyword.aios_full}} & カスタム ML エンジン・ノートブック](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}を参照してください。

- ペイロード・ロギング・テーブルにリクエストと応答を格納します

    ```python
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time), PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

    subscription.payload_logging.store(records=records_list)
    ```
    **注**: Python 以外の言語の場合、REST API を使用してペイロード・ロギングを直接実行することもできます。

    ```json
    token_endpoint = "https://iam.cloud.ibm.com/identity/token"
    headers = {
            "Content-Type": "application/x-www-form-urlencoded",
            "Accept": "application/json"
    }

    data = {
            "grant_type":"urn:ibm:params:oauth:grant-type:apikey",
            "apikey":aios_credentials["apikey"]
    }

    req = requests.post(token_endpoint, data=data, headers=headers)
    token = req.json()['access_token']
    ```

    ```json
    import requests, uuid

    PAYLOAD_STORING_HREF_PATTERN = '{}/v1/data_marts/{}/scoring_payloads'
    endpoint = PAYLOAD_STORING_HREF_PATTERN.format(aios_credentials['url'], aios_credentials['data_mart_id'])

    payload = [{
      'binding_id': binding_uid,
      'deployment_id': subscription.get_details()['entity']['deployments'][0]['deployment_id'],
      'subscription_id': subscription.uid,
      'scoring_id': str(uuid.uuid4()),
      'response': response_data,
      'request': request_data
    }]

    headers = {"Authorization": "Bearer " + token}
    req_response = requests.post(endpoint, json=payload, headers = headers)
    print("Request OK: " + str(req_response.ok))
    ```


## 次のステップ
{: #fmrk-workaround-nxt-steps-over}

{{site.data.keyword.aios_short}} で、[モニターを構成](/docs/services/ai-openscale?topic=ai-openscale-mo-config)する準備が整いました。

[カスタム機械学習の例](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-cstmmlsengex)のいずれかを使用して、独自のソリューションを実装します。
