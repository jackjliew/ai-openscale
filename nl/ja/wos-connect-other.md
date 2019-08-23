---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: machine learning, services, ml, custom 

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

# カスタム ML サービス・インスタンスの指定
{: #co-connect}

{{site.data.keyword.aios_short}} ツールで最初に実行するステップは、サービス・インスタンスの指定です。 サービス・インスタンスは、AI モデルとデプロイメントの格納場所となります。
{: shortdesc}

## カスタム・サービス・インスタンスの接続
{: #co-config}

{{site.data.keyword.aios_short}} を、サービス・インスタンスの AI モデルとデプロイメントに接続します。 カスタム・サービスを接続できます。

1. **「構成」**タブで、**「機械学習プロバイダー (Machine learning provider)」**をクリックします。ご使用の環境によっては、以下のプロバイダーの一部が表示されないことがあります。

   ![機械学習サービス・プロバイダーの選択画面に、サポートされる機械学習エンジンのタイルが表示されます](images/wos-machine-learning-providers-selection.png)

2. **「カスタム環境」**タイルを選択します。

   ![カスタム機械学習プロバイダー構成画面に、資格情報、インスタンス名、および説明のフィールドが表示されています](images/ml-custom-provider.png)

1.  資格情報を入力して保存します。

    - ユーザー名: カスタム機械学習プロバイダーのユーザー名。
    - パスワード: カスタム機械学習プロバイダーのパスワード。
    - サービス・プロバイダー・インスタンス名: このサービス・プロバイダーに割り当てられている特定の名前。
    - 説明: (オプション) このサービス・プロバイダー・インスタンスの簡単な説明。実動環境とテスト環境を運用している場合、その情報を含めることをお勧めします。

4. デプロイメントへの接続を、[リストを要求する](/docs/services/ai-openscale?topic=ai-openscale-co-connect#co-config-request-list)ことで行うか、[評価エンドポイントを個々に入力する](/docs/services/ai-openscale?topic=ai-openscale-co-connect#co-config-scoring-endpoints)ことで行うかを選択します。

   ![カスタムの選択](images/ml-custom-connect-deployments.png)
    
5. **「次へ」**をクリックします。

### デプロイメントのリストの要求
{: #co-config-request-list}

1. **「デプロイメントのリストの要求」**タイルを選択した場合は、資格情報と API エンドポイントを入力してから**「保存」**をクリックします。

   ![サービス資格情報の入力](images/connect-custom-cred.png)

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

![カスタムの処理の流れ](images/custom-how-works.png)

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

### 次のステップ
{: #co-next}

{{site.data.keyword.aios_short}} で、[モニターを構成](/docs/services/ai-openscale?topic=ai-openscale-mo-config)する準備が整いました。
