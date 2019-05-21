---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

keywords: machine learning, services, ml, custom 

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# カスタム ML サービス・インスタンスの指定
{: #co-connect}

{{site.data.keyword.aios_short}} ツールで最初に実行するステップは、サービス・インスタンスの指定です。サービス・インスタンスは、AI モデルとデプロイメントの格納場所となります。
{: shortdesc}

## カスタム・サービス・インスタンスの接続
{: #co-config}

{{site.data.keyword.aios_short}} を、サービス・インスタンスの AI モデルとデプロイメントに接続します。

1.  {{site.data.keyword.aios_short}} ツールのホーム・ページで、**「開始」**をクリックします。

    ![ホーム・ページ](images/gs-config-start.png)

2.  **「カスタム」**タイルを選択し、**「次へ」**をクリックします。

    ![カスタムの選択](images/connect-custom.png)

3.  いずれかのオプションを選択してデプロイメントに接続します。

    ![カスタムの選択](images/connect-custom-deploy.png)

4.  「個々の予測エンドポイントの入力」タイルを選択した場合、資格情報を指定します。

    ![サービス資格情報の入力](images/connect-custom-cred.png)

5.  **「次へ」**をクリックします。

    - 「個々の予測エンドポイントの入力」タイルを選択した場合、デプロイメント名とエンドポイントを指定する必要があります。

      ![サービス資格情報の入力](images/connect-custom-endpoint.png)

      **「次へ」**をクリックします。

    - 「デプロイメントのリストのリクエスト」タイルを選択した場合、ホスト名または IP アドレス、およびポート番号を指定する必要があります。

      ![サービス資格情報の入力](images/connect-custom-apiendpoint.png)

      **「次へ」**をクリックします。

      次に、デプロイメントのリストから選択します。

      ![サービス資格情報の入力](images/connect-custom-apiendpoint2.png)

6.  選択したデプロイメントを確認します。

    ![サービス資格情報の入力](images/connect-custom-deploy2.png)

7.  **「次へ」**をクリックします。

### 処理の流れ
{: #co-works}

このイメージは、カスタム環境サポートを示しています。

![カスタムの処理の流れ](images/custom-how-works.png)

以下のリンクも参照できます。

[AIOS ペイロード・ロギング API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/ai-openscale#publish-scoring-payload){: new_window}

[カスタム・デプロイメント API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://aiopenscale-custom-deployement-spec.mybluemix.net/){: new_window}

[Python クライアント・バインディング SDK ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://ai-openscale-python-client.mybluemix.net/#bindings){: new_window}

[Working with Custom machine Learning engine ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: new_window}

[Python SDK for IBM Watson OpenScale ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://pypi.org/project/ibm-ai-openscale/){: new_window}

- **モニターをサポートするためのモデルの入力基準**

  モデルでは入力として項目ベクトルを取る必要があります。実際にはこのベクトルは、名前付きフィールドとその値のコレクションです (ベクトル内の 1 つのフィールドがバイアスのモニター対象となります)。

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

  入力がテンソル/行列の場合、つまり入力項目スペースから変換される場合 (多くの場合、テキストまたはイメージからのディープ・ラーニングではそのように処理されます)、対象モデルを現行リリースの {{site.data.keyword.aios_short}} プラットフォームで処理することはできません。そのため、テキスト入力またはイメージ入力を使用するディープ・ラーニング・モデルを、バイアスの検出と緩和のために処理することもできません。

  また、説明性をサポートするためトレーニング・データをロードする必要があります。

  テキストの説明性を確保するには、いずれかの項目がフルテキストでなければなりません。カスタム・モデルのイメージに関する説明性は、現行リリースではサポートされていません。
  {: note}

- **モニターをサポートするためのモデルの出力基準**

  モデルでは、そのモデルの各種クラスの予測の確率とともに、入力項目ベクトルを出力する必要があります。

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

  この例では、`"personal”`と`“camping”`が候補となるクラスで、それぞれの予測出力のスコアが両方のクラスに割り当てられます。予測の確率がない場合、バイアスの検出は行われますが、自動バイアス修正は行われません。

  前述の予測出力は、{{site.data.keyword.aios_short}} が REST を介して呼び出すことが可能なライブ・予測エンドポイントからアクセス可能でなければなりません。AzureML、SageMaker、WML の場合、{{site.data.keyword.aios_short}} はネイティブの予測エンドポイントに直接接続します (そのため、お客様が予測仕様を実装する必要はありません)

### 次のステップ
{: #co-next}

{{site.data.keyword.aios_short}} で[データベースを指定する](/docs/services/ai-openscale?topic=ai-openscale-connect-db)準備が整いました。