---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

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
{: #ccust-custom}

{{site.data.keyword.aios_short}} ツールでの最初の手順は、サービス・インスタンスの指定です。サービス・インスタンスに AI モデルとデプロイメントが保管されます。
{: shortdesc}

## カスタム・サービス・インスタンスの接続
{: #co-config}

{{site.data.keyword.aios_short}} は、サービス・インスタンス内の AI モデルとデプロイメントに接続します。

1.  {{site.data.keyword.aios_short}} ツールのホーム・ページから、**「開始 (Begin)」**をクリックします。

    ![ホーム・ページ](images/gs-config-start.png)

1.  **「カスタム」**タイルを選択し、**「次へ」**をクリックします。

    ![カスタムの選択](images/connect-custom.png)

1.  いずれかのオプションを選択して、デプロイメントに接続します。

    ![カスタムの選択](images/connect-custom-deploy.png)

1.  「個々のスコアリング・エンドポイントの入力 (Enter individual scoring endpoints)」タイルを選択した場合は、以下のように資格情報を入力します。

    ![サービス資格情報の入力](images/connect-custom-cred.png)

1.  **「次へ」**をクリックします。

    - 「個々のスコアリング・エンドポイントの入力 (Enter individual scoring endpoints)」タイルを選択した場合は、以下のようにデプロイメント名とエンドポイントを指定しなければなりません。

      ![サービス資格情報の入力](images/connect-custom-endpoint.png)

      **「次へ」**をクリックします。

    - 「デプロイメントのリストの要求 (Request a list of deployments)」タイルを選択した場合は、以下のようにホスト名または IP アドレスとポート番号を指定しなければなりません。

      ![サービス資格情報の入力](images/connect-custom-apiendpoint.png)

      **「次へ」**をクリックします。

      続いて、以下のようにデプロイメントのリストから選択します。

      ![サービス資格情報の入力](images/connect-custom-apiendpoint2.png)

1.  選択したデプロイメントを検討します。

    ![サービス資格情報の入力](images/connect-custom-deploy2.png)

1.  **「次へ」**をクリックします。

## 動作内容
{: #ccust-works}

以下の画像は、カスタム環境のサポートを示しています。

![カスタムの動作内容](images/custom-how-works.png)

以下のリンクを参照することもできます。

[AIOS ペイロード・ロギング API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/ai-openscale#publish-scoring-payload){: new_window}

[カスタム・デプロイメント API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://aiopenscale-custom-deployement-spec.mybluemix.net/){: new_window}

[Python クライアント・バインディング SDK ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://ai-openscale-python-client.mybluemix.net/#bindings){: new_window}

[Working with Custom machine Learning engine ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: new_window}

[Python SDK for IBM Watson OpenScale ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://pypi.org/project/ibm-ai-openscale/){: new_window}

## モデルでモニターをサポートするための入力基準
{: #ccust-inp}

モデルでフィーチャー・ベクトルを入力として取る必要があります。フィーチャー・ベクトルとは基本的に、名前指定されたフィールドとその値の集合のことです (これらのフィールドの 1 つに対してバイアスのモニターが行われます)。

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

この例では、`“age”` が、公平性を評価するフィールドになります。

入力が入力フィーチャー・スペースから変換されたテンソル/マトリックスである場合 (テキストまたはイメージからのディープ・ラーニングでよくあるケース)、現行リリースでは、{{site.data.keyword.aios_short}} プラットフォームでそのモデルを処理することができません。この延長線上で考えると、入力がテキストまたはイメージのディープ・ラーニング・モデルに対してバイアスの検出と緩和の処理を行うことはできません。

また、説明可能性をサポートするには、トレーニング・データをロードする必要があります。

テキストに対する説明可能性の場合、フルテキストがフィーチャーの 1 つである必要があります。カスタム・モデルの場合のイメージに対する説明可能性は、現行リリースではサポートされていません。
{: note}

## モデルでモニターをサポートするための出力基準
{: #ccust-oup}

モデルが、そのモデル内のさまざまなクラスの予測確率に沿って、入力フィーチャー・ベクトルを出力する必要があります。

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

この例では、`"personal”` と `“camping”` が考えられるクラスで、各スコアリング出力内のスコアが両方のクラスに割り当てられます。予測確率が欠落していると、バイアス検出は作動しますが、自動バイアス除去は作動しません。

{{site.data.keyword.aios_short}} が REST を介して呼び出すことができるライブ・スコアリング・エンドポイントから、上記のスコアリング出力にアクセスできる必要があります。AzureML、SageMaker、WML の場合、{{site.data.keyword.aios_short}} はネイティブのスコアリング・エンドポイントに直接接続します (したがって、スコアリング仕様の実装を意識する必要はありません)。

## 次のステップ
{: #ccust-next}

{{site.data.keyword.aios_short}} で[データベースを指定](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-cdb-connect)する準備ができました。
