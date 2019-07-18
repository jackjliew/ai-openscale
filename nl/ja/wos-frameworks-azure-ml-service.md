---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits, azure

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

# Microsoft Azure ML Service フレームワーク
{: #frmwrks-azure-service}

{{site.data.keyword.aios_full}} は、以下の Microsoft Azure Machine Learning Service フレームワークを完全にサポートしています。
{: shortdesc}

表 1. フレームワークのサポート詳細

| フレームワーク | 問題のタイプ | データ・タイプ |
|:---|:---:|:---:|
| ネイティブ | 分類 | 構造化 |
| scikit-learn | 分類 | 構造化 |
| scikit-learn | 回帰 | 構造化 |
{: caption="フレームワークのサポート詳細" caption-side="top"}

## {{site.data.keyword.aios_short}} への Microsoft Azure ML Service の追加
{: #frmwrks-azureservice-addsrvc}

次のいずれかの方法を使用して、Microsoft Azure ML Service と連携するように {{site.data.keyword.aios_short}} を構成できます。

- 初めて機械学習プロバイダーを {{site.data.keyword.aios_short}} に追加する場合は、構成インターフェースを使用すると良いでしょう。 詳しくは、[Microsoft Azure ML Service インスタンスの指定](/docs/services/ai-openscale?topic=ai-openscale-connect-azureservice)を参照してください。
- Python SDK を使用して、機械学習プロバイダーを追加することもできます。 複数のプロバイダーが必要な場合は、この方法を使用する必要があります。 この操作をプログラムで実行する方法については、[Microsoft Azure 機械学習エンジンのバインド](/docs/services/ai-openscale?topic=ai-openscale-cml-azsrvconfig#cml-azsrvbind)を参照してください。


{{site.data.keyword.aios_short}} は、Azure ML Service との対話のために必要なさまざまな REST エンドポイントを呼び出します。呼び出しを行うには、Azure Machine Learning Service {{site.data.keyword.aios_short}} をバインドする必要があります。

1. Azure Active Directory のサービス・プリンシパルを作成します。
2. UI または {{site.data.keyword.aios_short}} Python SDK を使用して Azure ML Service サービス・バインディングを追加するときに、この資格情報の詳細を指定します。

## JSON 要求ファイルおよび応答ファイルの要件
{: #frmwrks-azureservice-JSON}

{{site.data.keyword.aios_short}} で Azure ML Service を使用するには、作成する Web サービス・デプロイメントが特定の要件を満たしている必要があります。作成する Web サービス・デプロイメントが、以下に説明する要件に従って、JSON 要求を受け入れ JSON 応答を返す必要があります。

### Web サービスの JSON 要求に求められる形式
{: #frmwrks-azureservice-JSON-sample-request}

- REST API 要求の本体は、JSON オブジェクトの JSON 配列 1 つを指定した JSON 文書でなければなりません。
- JSON 配列の名前は `"input"` でなければなりません。
- 各 JSON オブジェクトには、単純なキーと値のペアだけを指定できます。その値は、文字列、数値、`true`、`false`、または `null` でなければなりません。
- 値を JSON オブジェクトや配列にすることはできません
- 非 `null` の値があるかどうかには関係なく、配列内の各 JSON オブジェクトに常に同じキー (したがって同じ数のキー) を指定する必要があります。


以下のサンプル JSON ファイルは前述の要件を満たしているので、ユーザー独自の JSON 要求ファイルを作成するためのテンプレートとして使用できます。


```JSON
{
  "input": [
    {
      "field1": "value1",
      "field2": 31,
      "field3": true,
      "field4": 2.3
    },
    {
      "field1": "value2",
      "field2": 15,
      "field3": false,
      "field4": 0.1
    },
    {
      "field1": null,
      "field2": 5,
      "field3": true,
      "field4": 6.1
    }
  ]
}
```


### Web サービスの JSON 応答に求められる形式
{: #frmwrks-azureservice-JSON-sample-response}

JSON 応答ファイルを作成するときには、以下の点に注意してください。

- REST API 応答の本体は、JSON オブジェクトの JSON 配列 1 つを指定した JSON 文書でなければなりません。
- JSON 配列の名前は `"output"` でなければなりません。
- 各 JSON オブジェクトには、キーと値のペアだけを指定できます。その値は、文字列、数値、`true`、`false`、`null`、または、他の JSON オブジェクトや配列を含んでいない配列でなければなりません。
- 値を JSON オブジェクトにすることはできません
- 非 `null` の値があるかどうかには関係なく、配列内の各 JSON オブジェクトに常に同じキー (同じ数のキー) を指定する必要があります。
- 分類モデルの場合: Web サービスは、各クラスの確率を含む配列を返す必要があります。確率の順序は、配列内のすべての JSON オブジェクトで一貫していなければなりません。
  - 例: 信用リスクを予測する二項分類モデルでクラス `Risk` またはクラス `No Risk` に分類する場合
  - "output" 配列で返されるあらゆる結果において、オブジェクト内のキーと値のペアに含まれている確率の順序が、以下の形式で固定されていなければなりません。
  
  <code>"output": [{"Scored Probabilities": [<i>"Risk" probability,"No Risk" probability</i>]}, {"Scored Probabilities": [<i>"Risk" probability,"No Risk" probability</i>]}]</code>

Azure ML Studio および Service の両方で使用される Azure ML ビジュアル・ツールとの整合性のために、以下のキー名を使用することをお勧めします (ただし必須ではありません)。

- モデルの予測値を示す出力キーのキー名 `"Scored Labels"`
- 各クラスの確率を含む配列を示す出力キーのキー名 `"Scored Probabilities"`

以下のサンプル JSON ファイルは、前述の要件を満たしているので、ユーザー独自の JSON 応答ファイルを作成するためのテンプレートとして使用できます。


```JSON
{
  "output": [
    {
      "Scored Labels": "No Risk",
      "Scored Probabilities": [
        0.8922524675865824,
        0.10774753241341757
      ]
    },
    {
      "Scored Labels": "No Risk",
      "Scored Probabilities": [
        0.8335192848546905,
        0.1664807151453095
      ]
    }
  ]
}
```

## サンプル・ノートブック
{: #frmwrks-azureservice-smpl-ntbks}

以下のノートブックは、Microsoft Azure ML Service と連携する方法を示しています。

- [データマートの作成、モデル・デプロイメントのモニター、およびデータ分析](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}
- [MS Azure Service model scoring examples](https://dataplatform.cloud.ibm.com/analytics/notebooks/v2/0d4ebd8d-87cb-4c38-8ba8-37f5623df131/view?access_token=fcb2c411aed913bf94f86f434184db67aef1a6b304824b86b4ad63686e4890be){: external}

## 詳細
{: #frmwrks-azureservice-mediumblogs}

- [How does Azure Machine Learning service differ from Studio?](https://docs.microsoft.com/en-us/azure/machine-learning/service/overview-what-is-azure-ml#how-does-azure-machine-learning-service-differ-from-studio){: external}
